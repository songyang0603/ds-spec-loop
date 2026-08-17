# Decision classes

Use the host repository's existing taxonomy. If none exists, choose one primary semantic class below. A class guides investigation and evidence; it does not require a folder.

## Feature

Use for a new user-, model-, or external-caller-visible capability. Record:

- public behavior and ownership;
- how the capability is defined, composed, and consumed;
- lifecycle, cleanup, persistence, permission, and failure behavior when relevant;
- real alternatives and surrendered capability.

Evidence normally includes the real composition path, consumer behavior, visible output, and current public documentation.

## Bug fix

Use to restore an intended contract. Record:

- reproducible failure or direct gap;
- root cause rather than symptom;
- smallest semantic correction;
- why adjacent behavior remains unchanged;
- whether the defect exposes a missing invariant, evidence layer, or process rule.

Prefer regression evidence that fails before the fix and passes after it. Update an existing owner when one owns the intended contract. If no decision record or equivalent contract artifact owns a non-mechanical correction, create a narrowly scoped bug-fix owner; do not leave the strict loop without an owner.

## Simplification

Use to remove behavior, code, package surface, compatibility, or duplicate ownership without adding a capability. Record:

- complexity or duplicate owner removed;
- surviving owner;
- behavior retained;
- negative acceptance proving the old path is absent;
- capability or compatibility surrendered;
- reintroduction conditions.

Read [simplification.md](simplification.md).

## Architecture

Use for shipped-source structure: module/package ownership, dependency direction, runtime concepts, protocol, persistence model, or replaceable capability boundaries.

Make topology and invariants explicit. Evidence normally includes manifests/imports or structural checks, public contracts, real composition, integration behavior, and synchronized architecture docs.

## Process

Use for tooling, contribution policy, release, documentation workflow, or CI around shipped source.

Distinguish review-enforced policy from mechanical enforcement. Add a check only when the rule is important, decidable, uncovered, and likely to drift. If automation is not justified, state that review remains the enforcement mechanism.

## Testing

Use for test architecture, fixtures, determinism, snapshot policy, end-to-end lanes, or CI layering. Record:

- which failure existing evidence cannot catch;
- why the new evidence is closer to the consumer;
- how fixtures and outputs remain deterministic and reviewable;
- how the lane enters normal local or CI execution;
- what passing infrastructure does and does not prove.

When practical, demonstrate the lane against a known failing condition before restoring the passing state.
