# Decision records

Decision records preserve the problem, real alternatives, accepted direction, consequences, and verification obligations that code and current documentation cannot explain alone.

This repository uses one directory and a status field instead of path-encoded lifecycle folders:

- `Status: proposed` — a working proposal that is unbuilt or only partly built;
- `Status: accepted` — a stable decision reflected by the repository;
- `Status: rejected — <reason>` — an evaluated proposal that did not become current.

Supersession is a cross-linked relationship between accepted decisions. It is not a status or directory. Partial replacement keeps both records current and states which clauses each owns. A fully replaced record may be removed only after its unique rationale, alternatives, consequences, verification obligations, reintroduction conditions, and inbound links are preserved by the current owner.

Every non-mechanical change creates or updates one owning record in the same bounded change. An existing owner is preferred; files, modules, implementation phases, and test layers do not get separate records unless they represent independently revisitable decisions.

## Proposed structure

```markdown
# Decision: <title>

Status: proposed

## Problem
## Proposal
## Alternatives considered
## Acceptance criteria
## Risks
```

## Accepted structure

```markdown
# Decision: <title>

Status: accepted

## Problem
## Decision
## Alternatives considered
## Consequences
## Verification
```

Rewrite a proposal into current truth when accepting it. Preserve the acceptance-to-evidence obligations in Verification or an equivalent durable evidence section. Do not leave future plans or acceptance checklists in an accepted record.
