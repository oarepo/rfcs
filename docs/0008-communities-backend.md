- Start Date: 2022-02-01
- RFC PR: [#9](https://github.com/oarepo/rfcs/pull/9)
- Authors: Miroslav Bauer
- State: DRAFT


# Communities backend

[TOC]

## Summary

This PR introduces into OARepo the concept of "Communities", in order to facilitate the concept of grouping records for organization and management purposes. Communities are not meant to be just named collections of records, but also introduce a layer of collaborative features which can be used to serve more complex curation workflows in a repository. It can also be used to restrict access to records just to the Community members, when needed.

The scope of this RFC is the backend Invenio module `oarepo-communities` to allow CRUD+search operations on Communities and Community-aware records through the programmatic and REST APIs, to configure Community curation workflows and roles permissions.

It explores and defines ways, in which the existing [invenio-communities](https://github.com/inveniosoftware/invenio-communities) module and other related Invenio modules can be used to implement our use-cases.

## Motivation

#### 1. General user

> As a user from the general public:

- **a.** I want to be able to search for existing Communities, in order to discover and filter new institutions/projects/events/topics, that I may be interested in.
- **b.** I want to list, search and view records published (marked as visible to general public) in a Community of my interest.
- **c.** I want to list, search and view published records independently on Community it was published in (across all the Communities).
- **d.** When I download record metadata, I want to see, in which Community the record was published.

_NOTE: Any of the following roles are also considered as general users._

#### 2. Community owner

> As an owner of the Community:

- **a.** I want to be able to make changes to my Community's profile page, in order to correct/add information, so that they can quickly appear publicly for other users to see.
- **b.** I want to receive a persistent, unique identifier/slug (when used in record landing page URLs, it **MUST NEVER** change) for my Community, so that I can reliably store and depend on it on my side, in order to use it in any form of permanent API and UI URLs.
- **c.** I want to list and query all Community members and their corresponding Community roles **_#TODO:_** is this the proper role?

#### 3. Community member

> As a member of the Community:

- **a.** I want to submit my work as a repository record associated with my Community.
- **b.** As a member, I want to list and query my submitted records and filter it depending on submission / curation state (e.g. draft, waiting for approval, approved, published,...).
- **c.** I want to publish my record so that it can be discoverable and accessible either by:
  - other community members
  - general public.
- **d.** I want to list, query and view records published (marked as visible to Community or general public) by other Community members.
- **e.** where curation policy requires approval before publishing, I have to request such approval from Community curators and publishers (where applicable by policy).
- **f.** I want to list and view all the requests that I made (e.g. for record approval, doi registration,...) and it's status (e.g. whether it was accepted or rejected or any feedback from people involved in handling the request).
- **g.** I may want to get notified, when any of my requests changes it's state.
- **h.** I may want to discuss with people reviewing my requests by adding comments to it.

#### 4. Community curator

As a curator:

- **a.** I want to be notified, when a new record approval request appears in a Community
- **b.** I want to list and view all pending record approval requests in my Community, that needs to be reviewed.
- **c.** I want to review record approval requests together with related record and either:
  - accept them. Related record becomes visible to other members or general public (depending on Community's curation policy).
  - reject them, and provide optional feedback explaining why it was rejected, or if any changes to the related record are requested.
  - discuss with the request author by adding comments to the request

#### 5. Community publisher
_NOTE: This user role is relevant only to Communities having curation policy that requires additional approvement step before the record is made visible to general public._

As a Community publisher:

- **a.** I want to be notified, when a Community record approved by curators is requested to be published to general public.
- **b.** I want to list and view all pending record publication requests in my Community, that needs to be reviewed.
- **c.** I want to review record publication requests together with related record, and either:
  - accept them. Related record becomes visible to general public.
  - reject them, and provide optional feedback explaining why it was rejected.
  - discuss with the request author by adding comments to the request.

#### 6. System user

System user can be added to Community as a special kind of Community member. Such user may be subject to a different set of curation policy rules, record submission workflows, and record permission policies, than standard Community members.

For example, system users can be used in background processes for automatical harvest of records from another repository instance into Community.

> System user:

- **a.** Uses Rest APIs or record service directly for Community record submission

#### 7. Repository site administrator

> As a repository site administrator:

- **a.** I create Communities, designate Community owners
- **b.** I manage mappings of external user groups (from Perun AAI system) to repository site user groups
- **c.** I create and manage system users.

## Detailed design

To address the described use-cases, we consider the following existing Invenio modules:

- [invenio-communities](https://github.com/inveniosoftware/invenio-communities) for Community base support (APIs, models, services...)
- [invenio-requests](https://github.com/inveniosoftware/invenio-requests) to implement user requests for record approval, doi assignment,...
- [invenio-users-resources](https://github.com/inveniosoftware/invenio-users-resources) to manage user roles and groups
- [invenio-admin](https://github.com/inveniosoftware/invenio-admin) for Community administration interface, creation of system users, management of external group mappings

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
