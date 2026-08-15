# Agent Note lifecycle

An Agent Note records a proposal or decision that affects the codebase: the why, the meaningful alternatives, and what the chosen direction gives up.

## Path model

When a repository has no equivalent system, use:

```text
.agents/notes/
├── proposed/<class>/yyyy-mm-dd-topic-title.md
├── implemented/<class>/yyyy-mm-dd-topic-title.md
├── rejected/<class>/yyyy-mm-dd-topic-title.md
└── archived/<class>/yyyy-mm-dd-topic-title.md
```

Use the date the topic was first proposed. Keep it when moving lifecycle folders. Use relative Markdown links between notes so link checkers can survive moves.

The closed default class set is:

- `feature`
- `bug-fix`
- `simplification`
- `architecture`
- `process`
- `testing`

Do not add `refactor` by default. Classify by the decision: behavior-preserving removal or consolidation is usually `simplification`; shipped-source topology is `architecture`; workflow/tooling around source is `process`.

## Header contract

Use exactly:

```markdown
# Agent Note: <title>

Status: proposed
```

or:

```markdown
Status: implemented
```

or:

```markdown
Status: rejected — <concise reason>
```

The lifecycle path and status must agree.

## Proposed

A substantial unbuilt or partially built change stays proposed. Required semantic skeleton:

```markdown
## Problem
## Proposal
## Alternatives considered
## Acceptance criteria
## Risks
```

The problem must stand without the proposal. Acceptance criteria describe observable completion, not implementation tasks. Risks include likely failure modes and capability knowingly surrendered.

## Implemented

An implemented note records shipped reality:

```markdown
## Problem
## Decision
## Alternatives considered
## Consequences
```

Optional present-tense `Testing`, `Verification`, `Deferred`, or `Related` sections are valid. Do not leave proposal-era `Proposal`, `Plan`, `Migration plan`, or `Acceptance criteria` headings in an implemented note. Rewrite them into current facts and consequences.

Keep factual locations current when source later moves. Do not rewrite the decision itself unless it truly changes.

## Rejected

A rejected note preserves the evaluated proposal and alternatives. Put the verdict on the status line. Keep it only while the rationale prevents a plausible repeated mistake; otherwise delete it according to repository policy.

## Supersession and consolidation

Never edit an implemented note into the opposite decision. Create a new owning note and cross-link both.

Delete a fully superseded active note only after the current owner preserves every unique:

- rationale and alternative;
- consequence and surrendered capability;
- required verification and named coverage gap;
- reintroduction condition;
- inbound reference.

Partial supersession keeps both notes active and cross-linked.

An addition note may be consolidated into a later removal note only when the feature is absent from production source, configuration, schemas, durable/wire formats, migrations, compatibility behavior, current docs, and supported-behavior tests. The removal owner must preserve the original motivation, why it no longer justified the feature, alternatives to full removal, capability lost, reintroduction conditions, and proof of absence.

## Archive

Archive only implemented notes with low future decision value. Never archive proposed or rejected work merely to clean the tree.

Keep an implemented note active when it still owns:

- an important alternative or ownership boundary;
- a negative guarantee;
- durable, wire, or compatibility semantics;
- a security rule;
- a reintroduction condition;
- a named test or coverage gap.

Treat archived notes as immutable history and never current authority. A host repository may add translations, sidecars, hashes, or freeze gates; follow its established contract exactly.

When adopting the full default archive contract:

1. move only an implemented note into `archived/<class>/` without rewriting its decision;
2. retain `Status: implemented` and add `Archived: YYYY-MM-DD` immediately below it;
3. repair or deliberately remove inbound active links;
4. record the archived content in an append-only checksum manifest;
5. reject later edits, moves, reformats, translations, or deletions with a mechanical gate;
6. exclude archived sources from current-document freshness checks while still allowing intentional historical links into them.

If the host cannot enforce immutability yet, state that archive freezing is review-enforced rather than pretending a checksum guarantee exists.
