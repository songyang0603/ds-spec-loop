# Decision-record lifecycle

The loop requires three semantic stages but does not require particular filenames, directories, or status words.

| Semantic stage | Required meaning | Possible host forms |
|---|---|---|
| Working | unbuilt, partly built, or still changing; owns Problem, Proposal, Alternatives, Acceptance, Risks | Spec, RFC, proposal, design doc, draft ADR |
| Current | decision is reflected by source, evidence, and current docs; owns Decision, Alternatives, Consequences, Verification | ADR, decision record, implemented design, shipped RFC |
| Declined | proposal was evaluated and not adopted; rationale remains useful | rejected RFC, declined proposal, closed/rejected decision |

Do not map status words mechanically. In some ADR systems, `accepted` means approved but not implemented. A record becomes Current for this loop only after the repository's actual implementation, evidence, and current documentation converge.

## Working proposal

A substantial unbuilt or partially built change records:

```markdown
## Problem
## Proposal
## Alternatives considered
## Acceptance criteria
## Risks
```

The Problem stands without the proposal. Alternatives are real. Acceptance describes observable completion. Risks include likely failure modes and intentionally surrendered capability.

## Current decision

After delivery, rewrite the proposal as current truth:

```markdown
## Problem
## Decision
## Alternatives considered
## Consequences
## Verification
```

Verification, or the host repository's equivalent durable evidence mapping, records the acceptance obligations and direct evidence that remain authoritative after delivery. Optional present-tense Testing, Deferred, or Related sections are valid. Do not leave future plans or acceptance checklists in a Current record. Keep factual locations such as paths, symbols, defaults, and mechanisms current when they move; do not rewrite the decision into its opposite.

When one file carries both stages, rewrite its title and semantic sections. A status-only transition is invalid even if the implementation and tests pass.

If the host uses separate proposal and decision files, link them and make one artifact the current rationale owner. Do not maintain two complete competing descriptions of current truth.

## Declined proposal

Retain the evaluated proposal and concise rejection reason only while it prevents a plausible repeated mistake. Otherwise follow repository policy for removal.

## Replacement and consolidation

Replacement is a scoped relationship between decisions, not a fourth semantic stage.

### Living revision

Inside one uncompleted PR or change stack, revise the working proposal when the accepted direction changes. Do not create a permanent replacement chain for every review finding or implementation discovery. Read [requirement-change.md](requirement-change.md).

### Partial replacement

When an earlier decision still owns any valid boundary:

- keep both decisions Current;
- cross-link them;
- state which clauses the replacement changes;
- state which clauses the earlier owner retains;
- keep all remaining current facts accurate.

### Full replacement

Consolidate, retire, or remove an earlier decision only after the current owner preserves every unique:

- rationale and genuine alternative;
- consequence and surrendered capability;
- verification obligation and named coverage gap;
- reintroduction condition;
- inbound reference.

Git history must not be the only remaining copy of this decision value.

### Host repositories with a `superseded` status

Follow an established host lifecycle when it already uses that word. Still require a current replacement owner, cross-links, explicit replacement scope, and preserved rationale. The fallback convention does not introduce a `superseded/` directory or require that status.

## Complete removal

An addition decision can be fully absorbed by a removal decision only when the capability is absent from production source, registration/config, schemas, durable/wire formats, migrations, compatibility behavior, current docs, and supported-behavior tests. Removing one transport, default, implementation, or presentation remains partial replacement.

## Historical archive

Archive is optional and not a current semantic stage. Use the repository's existing historical convention. Create archive machinery only after a real retention need exists.

Keep a decision current when its alternatives, ownership boundary, negative guarantee, durable semantics, security rule, reintroduction condition, or coverage gap still guides future work. Historical records never override current source, contracts, or documentation.
