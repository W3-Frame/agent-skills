# Feature documentation guide

Use this guide to document a product's intended capabilities and track their state. It applies to planned, in-progress, and implemented work. The resulting documentation depends on the project's product decisions and evidence: do not infer requirements, implementation, or acceptance from this guide alone.

## Concepts

- **Module:** a functional domain grouping related capabilities, such as task management. A submodule may group related features when useful.
- **Feature:** a specific capability that enables a user or another system to achieve an identifiable, observable result. It has a clear scope and is testable independently of its technical implementation.
- **User story (US):** a need stated from an actor's perspective: **As** an actor, **I want** a capability, **so that** I achieve a meaningful outcome. A feature contains one or more stories, each with its own identifier.
- **Acceptance criterion (AC):** a verifiable condition describing an expected result or rule for a story. Each criterion has its own identifier and checkbox.

For example, **Task management** is a module; **Create a task** is a feature; the story explains who needs to create it and why; its criteria describe the observable behavior, including relevant rules and failures.

## Folder layout

```text
docs/features/
├── README.md          # Catalogue of modules and features
├── GUIDE.md           # This reusable guide
├── tasks.md           # One file for the task-management module
└── <module>.md        # One file for each additional module
```

The catalogue lists each module and feature, its intended scope and state, and links to its definition. A module file contains the shared product model, status and test coverage overviews, followed by its features and stories. Submodules are groupings within a module, not additional required files.

In the catalogue, use a module table (`Module | Scope`) followed by feature tables (`ID | Feature | Intended scope | Status`). Link each module and feature to its definition in the corresponding module file. Label proposed and undecided scope explicitly.

A feature is defined once regardless of access channel. If a capability is available through an interface, an API, or an agent, specify the applicable channels and verification without duplicating the product feature.

## Identifiers

Give each module a unique prefix. Assign features `FEAT-<MODULE>-<NUMBER>`, for example `FEAT-TASK-001`, and stories `US-<MODULE>-<NUMBER>`, for example `US-TASK-001`. Number features and stories independently across the module, using at least three digits. Criteria belong to a story and use `AC-US-<MODULE>-<STORY-NUMBER>-<CRITERION>`, for example `AC-US-TASK-001-01`.

Allocate each new story the next unused story number in its module, regardless of its feature. For example, if stories in Task Management already use numbers through `US-TASK-016`, a second story for `FEAT-TASK-001` receives `US-TASK-017`. Nest or link stories under their feature to show their relationship; matching numbers do not establish it.

Keep IDs stable: never reuse or renumber assigned identifiers after reordering, removal, or moving a story between features in the same module. When migrating existing documentation, preserve a mapping from old IDs to new IDs, update links and references, and keep any unmigrated criteria accessible.

## Feature catalogue file (`README.md`)

The catalogue is a navigation and tracking overview. The module file owns the detailed product model, stories, and criteria; do not copy those details into the catalogue. Start with a short purpose and status legend, followed by a module table and feature tables grouped by module.

- **Module / Scope:** link to the module file and summarize its domain or feature count. A count is not a completion measure.
- **ID / Feature:** show the feature ID and link the feature title to its definition in the module file.
- **Intended scope:** state the project's intended release or mark it proposed or undecided. Scope is separate from progress.
- **Status:** use the feature's assessed state, consistent with the evidence and the states of its stories; do not infer acceptance solely from their count or completion.

Example catalogue structure and rows:

```markdown
# Feature catalogue

Intended product capabilities and their current assessment.

## Status legend

Not assessed: evidence has not been examined.

## Modules

| Module                      | Scope                        |
| --------------------------- | ---------------------------- |
| [Task management](tasks.md) | Tasks and their organization |

## Features

### Task management

| ID            | Feature                                             | Intended scope      | Status       |
| ------------- | --------------------------------------------------- | ------------------- | ------------ |
| `FEAT-TASK-001` | [Create a task](tasks.md#feat-task-001-create-a-task) | MVP execution scope | Not assessed |
```

## Module file structure

Each module file is the reference for its product model and feature specifications. Group related features in one file; a submodule label may clarify their grouping. Start with a short purpose, then use the sections below in order.

### Product model

Define the concepts, relationships, boundaries, and rules shared by multiple features. Explain product behavior and distinguish accepted decisions from provisional rules. Do not repeat the same model under every story or describe implementation details unless they affect the product contract.

### Status overview

List every story with these columns, including each story when a feature has several:

| Column         | Meaning                                                              |
| -------------- | -------------------------------------------------------------------- |
| User story     | Stable story ID, linked to its story section.                        |
| Feature        | Feature ID and title, linked to its feature section.                 |
| Actor          | Person or external system seeking the outcome.                       |
| Intended scope | Intended release or explicit proposed/undecided scope.               |
| Status         | Assessed story state; not a substitute for coverage or acceptance.   |

### Test coverage overview

List the same stories with `User story`, `Main journey`, `Criteria coverage`, and `Gaps`. Identify the kind of journey and assessed coverage only when they have been mapped to evidence; otherwise use **Not assessed**. A coverage overview is not the result of the most recent test run. Do not invent a percentage or declare a gap closed without verification.

### Features and user stories

For each feature, use its feature ID and title as a heading. Record the submodule if applicable, intended scope, and specification status. Under it, give each story its own story ID and title, followed by its checkbox criteria. Group criteria into **Main journey** and **Business rules and edge cases** where applicable. Close the module with links to relevant product documents or decision records.

The following is an illustrative module file. The actor and outcomes are examples, not requirements for every project:

```markdown
# Task management

## Product model

A task is work belonging to a project. Tasks may be organized without being duplicated.

## Status overview

| User story  | Feature       | Actor          | Intended scope      | Status       |
| ----------- | ------------- | -------------- | ------------------- | ------------ |
| [US-TASK-001](#us-task-001-create-a-task) | [FEAT-TASK-001 Create a task](#feat-task-001-create-a-task) | Project member | MVP execution scope | Not assessed |

## Test coverage overview

| User story  | Main journey | Criteria coverage | Gaps         |
| ----------- | ------------ | ----------------- | ------------ |
| US-TASK-001 | Not assessed | Not assessed      | Not assessed |

## Features

### FEAT-TASK-001 Create a task

**Submodule:** Task organization

**Intended scope:** MVP execution scope

**Specification status:** Draft for review

#### US-TASK-001 Create a task

**As** a project member

**I want** to create a task

**So that** my team can track work in the project

##### Acceptance criteria

###### Main journey

- [ ] `AC-US-TASK-001-01` A member can create a task in an accessible project.

###### Business rules and edge cases

- [ ] `AC-US-TASK-001-02` A request without a task title is rejected.

## Related documentation

Link to the project's product model and relevant decision records.
```

Write criteria for the relevant main journey, business rules, and edge or error cases; omit an empty category rather than inventing rules. A criterion should describe a testable outcome, not just repeat a feature title or prescribe a button or implementation. Record a genuinely unresolved rule as unresolved instead of presenting it as a settled criterion.

## Create and maintain the catalogue

1. Read the project's vision, decisions or ADRs, product model, scope, and open questions. Distinguish accepted decisions from proposals.
2. Group the functional domains into modules. Identify distinct capabilities within each, using submodules only when they clarify the grouping. Do not turn UI clicks or implementation tasks into features.
3. Assign stable feature and story IDs and add each feature to both the catalogue and its module file. State each story's actor, need, expected outcome, scope, and acceptance criteria.
4. Capture shared concepts in the module product model. Specify feature-specific behavior in its stories and criteria; refer to the project's decision records for the rationale.
5. Populate status and coverage overviews from evidence. If the evidence has not been assessed, say so; an unassessed entry does not mean tests are absent or passing.
6. Review consistency and links, preserve earlier requirements during migrations, and run the project's documentation and formatting checks.

Use these states consistently for features and stories: **Not assessed** (evidence not examined), **To do** (accepted work not started), **In progress**, **Awaiting validation**, **Done** (verified and accepted), and **Abandoned** (explicitly dropped). Assess the feature as a whole when it contains multiple stories; do not assume one story's state applies to the entire feature. State is distinct from the intended release. In the coverage overview, identify the main journey, assessed criteria coverage, and known gaps; use **Not assessed** when no mapping exists.

Leave an AC unchecked until it has been verified. A checked criterion alone does not establish acceptance of the entire story. Track implementation status, test coverage, test run results, and product acceptance as separate facts; a closed issue, merged PR, or passing CI does not establish acceptance by itself.

Keep product behavior and criteria in the module files. Decisions and ADRs record decisions; issues and PRs support delivery and review. Do not copy issue or PR tracking metadata into the product specifications. Keep proposed scope and unresolved choices explicit.
