# Requirement changes inside the loop

Use this protocol when a user correction, review finding, failed premise, measurement, or implementation discovery changes the accepted direction. Keep the reconciliation in the current working proposal or task state; do not create a second permanent working-spec system.

## Classify the change

| Type | Meaning | Owner action |
|---|---|---|
| Clarification | wording becomes more precise without changing outcome, constraint, acceptance, or decision | update wording; do not manufacture history |
| Living revision | an uncompleted change alters scope, proposal, or acceptance | revise the same working owner |
| Evidence-driven refinement | observed evidence resolves an unknown without replacing the core decision | update proposal, evidence map, and implementation |
| Stable reversal | a Current decision or rationale is replaced after delivery | create a new cross-linked decision |
| Independent decision | a new requirement has its own problem, alternatives, consequences, and reversal boundary | create a separate owner |
| Authority-changing trade-off | new cost, privacy exposure, compatibility loss, product direction, or major architecture choice | ask the decision authority |

The boundary is decision stability, not commit count, elapsed time, or code volume.

## Reconcile the delta

Use a compact table in the working proposal or task state:

| Item | Previous accepted state | New accepted state | Disposition |
|---|---|---|---|
| Outcome and non-goals | earlier intent | current intent | keep / replace / withdraw / add |
| Constraints | earlier constraint | current constraint | keep / replace / withdraw / add |
| Acceptance | earlier observable claim | replacement or none | keep / replace / withdraw / add |
| Alternatives and rationale | earlier trade-off | current trade-off | valid / invalidated / newly relevant |
| Source and contracts | current implementation | required direction | retain / revise / remove |
| Tests and evidence | current proof | required proof | retain / revise / remove |
| Current docs/generated output | current fact | required fact | retain / revise / remove |
| Authority | existing authorization | new authorization | authorized / ask |

Do not preserve withdrawn acceptance as current truth.

## Ask only for material authority

Continue when the direction is explicit in the user request or repository policy and introduces no material unapproved trade-off.

Ask before accepting:

- product-scope or public-positioning changes;
- an external service, credential, payment, or recurring cost;
- privacy, security, data-transfer, or permission exposure;
- compatibility loss, migration burden, or irreversible deletion;
- a new architecture or ownership boundary with real competing options.

Show the conflict, affected acceptance, smallest coherent change, capability surrendered, and exact choice required. Do not ask the user to decide routine implementation details.

## Re-converge

After accepting the new direction:

- update the working owner before continuing implementation;
- repair every current authority that now disagrees;
- remove invalidated implementation, tests, generated entries, registrations, and docs;
- rerun only evidence invalidated by the delta;
- report withdrawn acceptance and removed work;
- use a replacement record only after a stable decision boundary.

If the revised change is delivered in the same run and the host uses one file for both Working and Current stages, rewrite that file into current truth: change Proposal to Decision, replace Acceptance and Risks with present-tense Consequences and Verification, and update the title when it still calls the record a proposal. Never mark work current by changing only a status word.
