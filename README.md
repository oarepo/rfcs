# OARepo RFCs

The OARepo RFC process (Request For Comments) is a **communication tool** inspired
with [Invenio RFCs](https://github.com/oarepo/rfcs) with
the purpose to:

- coordinate the design process
- document design decisions
- produce consensus among OArepo stakeholders

The RFCs are not meant to be a heavy long process, but rather an agile process
to aid communication between geographically dispersed teams as well as to
document OARepo development so that we can avoid knowledge loss when people
leave and ease knowledge transfer when people joins.

OARepo RFCs is not an official approval process which you might known from
other RFC processes.

### TL;DR

- [Request a new RFC](https://github.com/oarepo/rfcs/issues/new/choose)

#### Quick links

- [Pending RFC requests](https://github.com/oarepo/rfcs/labels/Proposal%3A%20Pending)
- [Work-In-Progress RFCs](https://github.com/oarepo/rfcs/labels/Proposal%3A%20Accepted)
- [Completed RFCs](https://github.com/oarepo/rfcs/tree/main/docs)

### Process overview

1. **[Request RFC](#step-1-request-an-rfc) (focus on scope):** Before starting to write a new RFC, you first have to request the approval of OARepo architects by [opening an issue](https://github.com/oarepo/rfcs/issues/new/choose). This is to aid scoping the RFC, avoid duplication as well as save everyone time..
2. **[Write RFC](#step-2-write-the-rfc) (focus on content):** If the request is accepted by architects, you start collaborative writing of the RFC using the [template](https://github.com/oarepo/rfcs/blob/master/0000-template.md). This part of the process focuses on the *content*, and an architect is assigned to support you in writing the RFC. The goal is that most discussions and alignment on a solutions happens in the writing phase.
3. **[Review RFC](#step-3-review-the-rfc) (focus on quality):** Once the RFC is complete, you submit a pull-request with the new RFC for final review. The review focuses on quality of RFC, not the content of the RFC (should already have been agreed upon in the writing phase).
4. **[Merge RFC](#step-4-merge-the-rfc):** RFC is merged into repository (RFCs does not need to be complete to be merged, as long as unresolved questions have been listed in the RFC and quality has passed the review).
5. **[Start implementing RFC](#step-5-start-rfc-implementation):**
6. **[Finish RFC implementation](#step-5-start-rfc-implementation):**

---

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


The OARepo RFC process owes it's initial inspiration to the
[Invenio RFC process](https://github.com/inveniosoftware/rfcs).
