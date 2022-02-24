# OARepo Loose validation 

### Motivation

For needs of processing harvested data from external sources, it is necessary to be able to store invalid records. Relevant error messages must be indexed for subsequent work to enable their aggregation and retrieval. Invalid records also need to be marked as non-valid. 
### Summary

Within the loosely validated models both valid and non-valid records are stored. Errors in data can be of two types:

- Structural errors (wrong data type, non-existent field…)
- Non-structural errors (too many characters in string, not enough values in object…)

#### In case of structural error
Problematic field will be erased from record and its value will be stored in field for non-valid values with information about original field. Respective error message will be stored in field for error messages with information about original field. Record will be labeled as non-valid.

#### In case of non-structural error
Problematic field will be stored as it is. Respective error message will be stored in field for error messages with information about original field. Record will be labeled as non-valid.

### Detailed design
#### oarepo:validity field
Field added to top-level of JSON schema, elastic search mapping and marshmallow schema.  It is used to store non-valid values and error messages.
##### JSON schema
```
{
  "oarepo:validity": {
    "type": "object",
    "properties": {
      "valid": {
        "type": "boolean"
      },
      "errors": {
        "type": "array",
        "items": {
          "type": "object",
          "properties": {
            "path": {
              "type": "string",
            },
            "message": {
              "type": "string",
            }
          }
        }
      },
      "invalid_fields": {
        "type": "array",
        "items": {
          "type": "object",
          "properties": {
            "path": {
              "type": "string",
            },
            "content": {
              
            }
          }
        }
      }
    }
  }
}
```
##### Elasticsearch mapping
```
{
  "oarepo:validity": {
    "type": "object",
    "properties": {
      "valid": {
        "type": "boolean"
      },
      "errors": {
        "type": "nested",
        "properties": {
          "path": {
            "type": "keyword"
          },
          "message": {
            "type": "keyword"
          }
        }
      },
      "invalid_fields": {
        "type": "object",
        "properties": {
          "path": {
            "type": "keyword"
          },
          "content": {
            "type": "flattened"
          }
        }
      }
    }
  }
}
```
##### Marshmallow schema
```
class InvalidSchema(Schema):
    path = ma_fields.String()
    content = ma_fields.Raw()

class ValiditySchema(Schema):
    valid = ma_fields.Bool(required=True)
    errors = ma_fields.List(ma_fields.Nested(ErrorsSchema))
    invalid_fields = ma_fields.List(ma_fields.Nested(InvalidSchema))

class RecordMetadataSchema(Schema):
    _validity = ma_fields.Nested(ValiditySchema(), data_key='oarepo:validity', attribute='oarepo:validity', required=True)

```
#### Record model
#### JSON schema
JSON schema will be as little restrictive as possible. Fields will have no constraints defined and all validation will be handled by Marshmallow. I.e.: Fields in JSON schema can only have defined their names and types (and in case of objects their property names and types). Additional properties are allowed.
#### Marshmallow
Marshmallow schema fields contain all defined model restrictions. Base record schema is inherited from modified [Marshmallow base schema](https://github.com/marshmallow-code/marshmallow/blob/dev/src/marshmallow/schema.py) which will be defined in oarepo-loose-validity library and will provide the entire validation logic.
#### Error analysis
The type of error will be detected through the content of respective error message. Basic error messages are defined [here](https://github.com/marshmallow-code/marshmallow/blob/dev/src/marshmallow/validate.py). It is also possible to define own validation rules and errors. Because of that it needs to be decided how to distinguish structural errors from non-structural.
Options:

1) Do it by using regular expressions where primarily everything is taken as a structural error unless the error message falls within the list of specified non-structural error messages. In case of custom error messages add information that it is non-structural error (for example add suffix “Loose validation”)
2) Specify all non-structural errors inside application config (needs to be as regex because of errors of type “less then XY” etc.)
3) Something else?

### Example
#### Data Schema
```
class AuthorSchema(Schema):
    first_name = ma_fields.String(validate=[ma_valid.Length(min=5, max=None)])
    last_name = ma_fields.String(validate=[ma_valid.Length(min=5, max=None)])
    
class RecordMetadataSchema(Schema):

    title = ma_fields.String(validate=[ma_valid.Length(min=5, max=10)], required=True)
    authors = ma_fields.Nested(AuthorSchema)

    _validity = ma_fields.Nested(ValiditySchema(), data_key='oarepo:validity', attribute='oarepo:validity', required=True)
```
#### Harvested data
```
{
  "metadata": {
    "title": "jej",
    "authors": {
      "first_name": "yxyxy",
      "last_name": "xyxyx",
      "something": "wrong"
    }
  }
}
```
#### Stored data
```
{
  "updated": "1970-10-19",
  "id": "hmb7c-ryf20",
  "created": "1970-10-19",
  "metadata": {
    "oarepo:validity": {
      "valid": false,
      "errors": [{"path":  "metadata.title", "message":  "Length must be between 5 and 10."}, 
                {"path":  "metadata.title.something", "message": "Unknown field."}]
      "invalid_fields": [{"path":  "metadata.title.something", "content":  "wrong"}]
    },
    "authors": {
      "last_name": "yxyxy",
      "first_name": "xyxyx"
    },
    "title": "jej"
  },
  "links": {
    "self": "/validity_example/hmb7c-ryf20"
  }
}
```
###Diskuze

 - oarepo:validity pole bude jako system field - tzn nebude na úrovni metadat, ale jako samostaný atribut v tabulce
 - Chybové hlášky řešit pomocí loose validation obalu + generování vlastních zpráv z důvodu problému například s chybami typu "špatný format data"
 - Kam patří taxonomické chyby? Pokud to má správnou strukturu, tak to jde uložit - tzn nestrukturální chyba i když hodnota není ve slovníku
 -  když chybí povinná věc, jedná se o nestrukturální chyby
 - oarepo:validity přejmenovat na oarepo:metadataValidity, aby bylo jasné, že se jedná o validační chyby v metadatech a ne v dokumentech
 - Je potřeba udělat plugin do model builderu v samostatné knihovně a připojit skrze `oarepo:use : [loose-validity]
 - v ui je potřeba počítat s tím, že žádná věc nemusí být vyplněna
 - do budoucna zavést i striktní chyby které nikdy nemohou být uloženy (například pro potřeby uživatelského formuláře)