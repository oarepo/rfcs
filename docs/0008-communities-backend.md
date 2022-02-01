- Start Date: 2022-02-01
- RFC PR: [#9](https://github.com/oarepo/rfcs/pull/9)
- Authors: Miroslav Bauer
- State: DRAFT


# Communities backend

[TOC]

## Summary

This PR introduces into OARepo the concept of "Communities", in order to facilitate the concept of grouping records for organization and management purposes. Communities are not meant to be just named collections of records, but also introduce a layer of collaborative features which can be used to serve more complex curation workflows in a repository. It can also be used to restrict access to records just to the Community members, when needed.

The scope of this RFC is the backend invenio module `oarepo-communities` to allow CRUD+search operations on Communities and Community-aware records through the programmatic and REST APIs, to configure Community curation workflows and roles permissions.

## Motivation

#### 1. General user
- **a.**  As a user, I want to be able to search for existing Communities, in order to discover and filter new institutions/projects/events/topics, that I may be interested in.
- **b.** As a user, I want to be able to browse and search for records published in a Community of my interest.
#### 2. Community owner
- **a.** As a Community owner, I want to be able to make changes to my Community's profile page, in order to correct/add information, so that they can quickly appear publicly for other users to see.
- **b.** As a Community owner, I want to be able to have a persistent, unique identifier/slug for my Community, so that I can reliably store and depend on it on my side, in order to use it in REST API
- **c.** As a Community owner, I want to list and query all Community members and their corresponding Community roles
#### 3. Community member
- **a.** As a member, I want to submit my work as a repository record associated with my Community.
- **b.** As a member, I want to list and query my submitted records and filter it depending on submission / curation state (e.g. draft, waiting for approval, approved, published,...).
- **c.** As a member, I want to publish my record so that it can be discoverable and accessible either by:
  - other community members
  - general public. 
- **c.** As a member of Community, where curation policy requires approval before publishing, I need to be able to request such approval by Community curators.
- **d.** As a member, I want to be able to list and check all the requests that I made (e.g. for record approval, doi registration,...) and it's status (e.g. whether it was accepted or rejected or any feedback from people involved in handling the request).

#### 4. Community curator


#### 5. Community publisher


#### 6. Repository system administrator

## Detailed design

> This is the bulk of the RFC.

> Explain the design in enough detail for somebody familiar with the framework to understand, and for somebody familiar with the implementation to implement. This should get into specifics and corner-cases, and include examples of how the feature is used. Any new terminology should be defined here.

## Example

> Show a concrete example of what the RFC implies. This will make the consequences of adopting the RFC much clearer.

> As with other sections, use it if it makes sense for your RFC.

## How we teach this

> What names and terminology work best for these concepts and why? How is this idea best presented? As a continuation of existing Invenio patterns, or as a wholly new one?

> Would the acceptance of this proposal mean the Invenio documentation must be re-organized or altered? Does it change how Invenio is taught to new users at any level?

> How should this feature be introduced and taught to existing Invenio users?

## Drawbacks

> Why should we *not* do this? Please consider the impact on teaching Invenio, on the integration of this feature with other existing and planned features, on the impact of the API churn on existing apps, etc.

> There are tradeoffs to choosing any path, please attempt to identify them here.

## Alternatives

> What other designs have been considered? What is the impact of not doing this?

> This section could also include prior art, that is, how other frameworks in the same domain have solved this problem.

## Unresolved questions

> Optional, but suggested for first drafts. What parts of the design are still TBD? Use it as a todo list for the RFC.

## Resources/Timeline

> Which resources do you have available to implement this RFC and what is the overall timeline?
