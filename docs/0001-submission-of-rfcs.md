- Start Date: 2021-12-14
- RFC PR: [#2](https://github.com/oarepo/rfcs/pull/2)
- Authors: @mirekys
- State: Being implemented
- Implemented in:
  - https://github.com/oarepo/rfcs/issues/3
  - https://github.com/oarepo/rfcs/issues/4

# Submission of rfcs

## Summary

Defines a process to handle change requests for OARepo platform from multiple parties.

## Motivation

- As a software engineer I would like to propose a change to the OARepo platform APIs,
so that I can integrate with my 3rd party software.

- As a data steward, I would like to add a new approvement mechanism to my repository
application based on the OARepo platform, so that I can conform to rules enforced by
my institution.

## Detailed design

### When to write a RFC?

You need to write a RFC to make changes to OARepo modules functionality. A change could be:

- Adding/removing larger features and/or modules.
- Changing existing features/APIs.
- Changes of design patterns, idiomatic usage or conventions.

### Step 1: Request an RFC

##### Change requestor

- [Open an issue](https://github.com/oarepo/rfcs/issues/new/choose).
  - Document the 1) Motivation 2) Summary of proposed changes and 3) Resources

##### [Platform architects](https://github.com/orgs/oarepo/teams/architects):

- Label and assign the issue
  - All new RFCs should have the "Proposal: Pending" label and a label for the product (e.g. "NR").
- Review the request
- **If rejected**:
  - Add a justification to the comments of the issue.
  - Change the label to "Proposal: Rejected".
  - Close the issue.
- **If accepted**
  - Change the label to "Proposal: Accepted".
  - Create a RFC draft document in a new branch by running a `new-rfc` GitHub Action:
    1. Action should take issue number (e.g. 10) as user input
    2. Creates & checkouts new branch in format `rfc-10`
    3. Copies `0000-template.md` to `docs/0010-your-rfc-issue-title-slugified.md`
    4. Fills the RFC document header with current date to `Start Date`, current issue author to `Authors`, and replaces `<RFC title>` with issue title.
    5. Creates a Pull Request from `rfc-10` to `main` branch
    6. Fills the RFC document header with link to the created PR
    7. Links the issue with the PR
  - Assign the point-of-contact architect (person responsible for drafting the RFC document)

### Step 2: Write the RFC

Following is optional. It is just advices for writing the RFC in an collaborative and efficient manner:

- Choose an editor (person) being responsible for this phase (e.g. the architect or another OARepo team member)
- **Brainstorming phase:**
  - Fill the template with unstructured bullet points and high-level outline.
  - Try to clearly define scope - what's included, and what's excluded.
  - Try to identify multiple options for solutions.
  - What issues should be addressed?
  - Identify possible stakeholders, and include them in the discussions.
- **Reading phase (moderated by editor):**
  - Add a "Questions" subsection to each section.
  - Read the RFC and add questions/comments to the questions sections (prefix each question with ``<name>: ...``). Be clear purpose and support it with examples.
  - Purpose is to identify sections that needs further discussion.
- **Discussion phase (moderated by editor):**
  - Expect discussion on semantics, naming and scope to possibly be long discussions (i.e. take these discussions first, subsequent discussions will be much faster).
  - Identify discussions points and list them in the document
  - Meet live to discuss discussion points
    - Moderator takes notes as bullet points for each discussion point/question.
    - Moderator must ensure everybody is explicitly asked about their opinion.
    - Conclusion:
      - Ask for preferred solution: Once sufficient discussion has taken place, the moderator asks each person
        for their preferred solution. Goal is to identify if there is consensus or disagreement.
      - Propose conclusion: The moderator looks for a consensus solution an proposes this solution.
      - Ask explicitly everyone if they agree
      - If consensus is not possible, the conclusion can be TBD and perhaps needs more research, and/or ask for input from non-designated architects.
  - Meet live to discuss all questions
    - Use same procedure as for discussion points.
- **Cleaning phase:**
  - Clean up the RFC document - it should be readable and coherent for a third-party which was not part of the discussions.
  - Write up the summary focusing on explaining a third-party about the gist of the RFC.
- **Reviewing phase:**
  - Ask for input from the non-designated architects and other stakeholders.

You can jump around between phases.

**Disagreement resolution**

> Fight for what you believe, but gracefully accept defeat.

Please do your outmost to not have unresolvable disagreements! The more senior your are, the more responsible you are to not have unresolvable disagreements.

In case all attempts to reach consensus have failed, and really only as a very very last resort, the architects can resolve the conflict by taking a decision. This decision should be properly documented.

### Step 3: Review the RFC

##### [Q/A Team](https://github.com/orgs/oarepo/teams/qa)

- Comment on quality of the RFC, not the chosen solutions (this was already done in step 2)!
- Can the RFC be understood by an experienced third-party that didn't participate in the discussions?
- Is the RFC coherent?
- Are the unresolved questions properly documented?
- Set RFC status to `Ready`

##### [OARepo platform Managers](https://github.com/orgs/oarepo/teams/managers)

- Are there sufficient resources to implement the RFC?

### Step 4: Merge the RFC

##### [Platform architects](https://github.com/orgs/oarepo/teams/architects):

As soon as the RFC has reached sufficient quality level and consensus it can be merged into this RFC repository. The RFC does not need to be fully completed to be merged, as long as unresolved questions have been listed in the RFC.

### Step 5: Start RFC implementation

##### [Platform architects](https://github.com/orgs/oarepo/teams/architects):

- Create implementation issues in repositories affected by the RFC, assign developers
- Update RFC document's `Implemented in:` header with links to issues
- Set RFC status to `Being implemented`

### Step 6. Finish RFC implementation

When all implementation issues are resolved and closed:

##### [Q/A Team](https://github.com/orgs/oarepo/teams/qa)

- Check that user stories from the **Motivation** section are fullfilled by the implementation

##### [Platform architects](https://github.com/orgs/oarepo/teams/architects):

- Set RFC status to `Implemented`

### RFC States overview

- **Draft**: The RFC has reached sufficient quality to be merged, some discussions has happened, but there's open questions
and it's not ready yet to be implemented.
- **Ready**: The design is ready, enough discussions has happened to reach a reasonable consensus and quality of RFC is good.
- **Being implemented**: The RFC implementation has started.
- **Implemented**: The RFC has been implemented in the community or code.

## Drawbacks

Extra 'paperwork' needed to implement new features, incorporate changes to the platform.

## Alternatives

1. Ignore any documentation :)
2. Use some collaborative document management system outside of GitHub

## Resources/Timeline

Implementation of `new-rfc` GitHub action needed for described workflows will be done by @tomash ASAP.
