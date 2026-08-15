# Copy-ready artifact templates

Adapt paths and terms to the host repository. These templates encode the lifecycle semantics; they are not a substitute for repository investigation.

## Proposed Agent Note

```markdown
# Agent Note: <decision title>

Status: proposed

## Problem

<Describe the user, model, maintainer, or system problem without assuming the solution.>

## Proposal

<State the intended decision, ownership boundary, assembled path, and migration if any.>

## <Bespoke technical section, if needed>

<Topology, protocol, schema, invariants, lifecycle, or compatibility details.>

## Alternatives considered

**<Real alternative>.** <Why it loses under the stated problem and constraints.>

**<Another real alternative>.** <Why it loses.>

## Acceptance criteria

- <Observable behavior or absence, including the real assembled path.>
- <Failure, cleanup, durability, compatibility, or negative guarantee.>
- <Current-state docs and generated surfaces agree with the shipped contract.>

## Risks

- <Likely failure mode and mitigation or evidence.>
- <Capability, flexibility, or compatibility knowingly given up.>
```

## Implemented Agent Note

Rewrite; do not merely rename headings.

```markdown
# Agent Note: <decision title>

Status: implemented

## Problem

<Keep the solution-independent motivation current.>

## Decision

<Describe what the repository now does, in present tense, with current paths and names.>

## <Bespoke technical section, if still useful>

<Current topology, protocol, schema, invariants, or compatibility facts.>

## Alternatives considered

**<Alternative>.** <Why the shipped decision wins.>

## Consequences

<What the decision buys, costs, forbids, removes, or leaves intentionally deferred.>

## Testing / Verification

- `<exact command>` — <actual outcome and acceptance claim covered>.
- <Static or runtime evidence with exact repository locations>.
- Not run: <check and missing condition>, if applicable.
```

## Rejected Agent Note

```markdown
# Agent Note: <decision title>

Status: rejected — <concise verdict>

## Problem

<Problem that motivated evaluation.>

## Proposal

<Proposal as evaluated.>

## Alternatives considered

**<Alternative>.** <Trade-off.>

## Acceptance criteria

<Preserve proposal-time criteria if useful to understand the evaluation.>

## Risks

<Preserve proposal-time risks.>
```

## Change delivery summary

```markdown
## Outcome

<What is now true.>

## Decision lifecycle

- Owning note: `<path>`
- Transition: `<created proposed | proposed → implemented | proposed → rejected | updated implemented | superseded>`

## Authority surfaces changed

- Source/contracts: <paths>
- Executable evidence: <paths>
- Current-state docs/generated references: <paths>

## Verification

- `<command>` — <actual outcome>
- Not run: <check and reason>

## Remaining proposed or blocked work

- <Only real remaining work; omit if none.>
```
