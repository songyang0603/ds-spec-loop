# Decision classes

Choose one primary class for the durable decision. A change may touch many surfaces; do not create duplicate notes for each surface.

## Feature

Use for a new user-, model-, or external-caller-visible capability.

The note should establish:

- the public behavior and ownership boundary;
- how the capability is defined, provided, loaded, and consumed;
- lifecycle, cleanup, persistence, replay, or permission semantics when relevant;
- compatibility and failure behavior;
- what simpler or narrower alternatives were rejected.

Evidence should normally include the real composition path, consumer behavior, user/model-visible evidence, and current public documentation. A leaf implementation test alone does not prove availability.

## Bug fix

Use to restore an existing intended contract.

The note should establish:

- a reproducible failure or direct evidence of the gap;
- the root cause rather than only the symptom;
- the smallest semantic correction;
- why adjacent behavior remains unchanged;
- whether the defect reveals a missing invariant, test layer, or process rule.

Prefer regression evidence that fails before the fix and passes after it. Do not broaden a bug fix into a redesign unless the root cause requires a new decision; if so, make that decision explicit.

## Simplification

Use to remove code, behavior, package surface, compatibility, or duplicated ownership without adding a capability.

The note should name:

- the complexity or duplicate owner being removed;
- the surviving owner;
- externally observable behavior that remains;
- negative acceptance proving the old path is absent;
- capability or compatibility surrendered;
- conditions for reintroduction.

Read [simplification.md](simplification.md) before acting.

## Architecture

Use for shipped-source structure: package/module ownership, dependency direction, runtime vocabulary, protocol, persistence model, or capability seam.

The note should make topology and invariants explicit. Evidence should normally include manifests/imports or structural checks, public types, provider-consumer composition, integration behavior, and synchronized architecture docs.

Do not classify surrounding tooling or contribution workflow as architecture; that is process.

## Process

Use for tooling, policy, contribution workflow, release, documentation workflow, or CI around the shipped source.

Distinguish a review-enforced policy from a mechanically enforced one. If the decision claims deterministic enforcement, implement the gate, test the gate's meaningful failure mode, wire it into the real developer/CI path, and update contributor instructions. If automation is not justified, say that review remains the enforcement mechanism.

Do not add a checker merely because the decision is classified as process. The rule must be important, decidable, and likely to drift.

## Testing

Use for test architecture, fixtures, determinism, snapshot policy, end-to-end lanes, and CI test layering.

The note should establish:

- which failure an existing test layer cannot catch;
- why the proposed evidence is closer to the real consumer;
- how fixtures and snapshots remain deterministic and reviewable;
- how the lane enters normal local or CI execution;
- what the test infrastructure passing does and does not prove.

When practical, verify the lane with an intentionally failing fixture or pre-fix failure, then restore the passing state. Do not confuse successful test orchestration with successful product behavior.
