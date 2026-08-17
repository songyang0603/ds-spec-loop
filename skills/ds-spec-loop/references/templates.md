# Generic artifact templates

Use the host repository's established formats first. These are fallback semantic templates, not mandatory filenames, headings, statuses, or directories.

## Working proposal

```markdown
# Proposal: <decision title>

Status: proposed

## Problem

<Describe the user, maintainer, operator, or system problem without assuming the solution.>

## Proposal

<State the intended decision, ownership, real consumer path, and migration if any.>

## <Technical detail, if needed>

<Topology, protocol, schema, invariants, lifecycle, or compatibility.>

## Alternatives considered

**<Real alternative>.** <Why it loses under the stated constraints.>

## Acceptance criteria

- <Observable behavior or absence through the real consumer path.>
- <Failure, cleanup, durability, compatibility, or negative guarantee.>
- <Current docs and generated surfaces agree with the delivered contract.>

## Risks

- <Likely failure and matching evidence.>
- <Capability, flexibility, or compatibility knowingly surrendered.>
```
## Stable decision

Rewrite the proposal; do not merely rename headings.

```markdown
# Decision: <decision title>

Status: implemented

## Problem

<Keep the solution-independent motivation current.>

## Decision

<Describe what the repository now does, in present tense, with current paths and names.>

## <Technical detail, if still useful>

<Current topology, protocol, schema, invariants, or compatibility.>

## Alternatives considered

**<Alternative>.** <Why the current decision wins.>

## Consequences

<What the decision buys, costs, forbids, removes, or leaves deferred.>

## Verification

- `<exact command or runtime path>` — <actual outcome and covered claim>.
- Not run: <check and missing condition>, if applicable.
```

## Declined proposal

```markdown
# Proposal: <decision title>

Status: rejected — <concise verdict>

## Problem
## Proposal
## Alternatives considered
## Acceptance criteria
## Risks
```

Retain only while the verdict prevents a plausible repeated mistake.

## Requirement delta

```markdown
| Item | Previous accepted state | New accepted state | Disposition |
|---|---|---|---|
| Outcome / non-goal | ... | ... | keep / replace / withdraw / add |
| Acceptance | ... | ... | keep / replace / withdraw / add |
| Source / contract | ... | ... | retain / revise / remove |
| Tests / evidence | ... | ... | retain / revise / remove |
| Current docs | ... | ... | retain / revise / remove |
| Rationale | ... | ... | living revision / stable replacement |
```

## Delivery summary

```markdown
## Outcome

<What is now true.>

## Decision ownership

- Owner: `<path or identifier>`
- Lifecycle: `<created proposal | updated proposal | accepted current decision | rejected>`
- Relationship: `<none | replaces | partially replaces | consolidates>`

## Authority surfaces changed

- Source/contracts: <paths>
- Executable evidence: <paths>
- Current docs/generated references: <paths>

## Verification

- `<command>` — <actual outcome>
- Not run: <check and reason>

## Requirement delta

- <Withdrawn, replaced, or newly authorized requirement; omit if none.>

## Remaining work

- <Only real proposed or blocked work; omit if none.>
```
