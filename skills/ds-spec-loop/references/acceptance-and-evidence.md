# Acceptance and evidence

Acceptance is useful only when an observation can contradict it. “Implement X,” “add tests,” and “update docs” are tasks, not acceptance criteria.

## Write observable acceptance

Good acceptance identifies:

- actor or caller;
- starting state and input;
- observable behavior or absence;
- durable or compatibility effect when relevant;
- failure behavior and negative guarantee;
- the boundary beyond which the claim is not made.

## Build an evidence map

Use a compact table in the working proposal or task state:

| Acceptance | Failure surface | Direct evidence | Result |
|---|---|---|---|
| consumer reaches the capability through real composition | registration and composition | repository-native integration test | record actual result |
| cleanup removes the capability | lifecycle cleanup | dispose/unregister observation | record actual result |
| persisted state reconstructs behavior | persistence and projection | resume/replay evidence | record actual result |
| removed API is absent | source, exports, docs, catalogs | negative search plus relevant tests | record actual result |

Write exact repository commands and outcomes. If evidence cannot run because a credential, platform, environment, or authority is missing, state that boundary; lower-layer evidence supports only the narrower claim it directly observes.

## Match evidence to risk

| Risk | Primary evidence |
|---|---|
| parsing, transformation, local invariant | focused unit test |
| service/package/runtime composition | integration or composition test |
| persistence, resume, event order | recovery or replay test |
| user/model-visible behavior | real application path and stable output evidence |
| external provider contract | real end-to-end test when access exists |
| complete removal | negative search across source, registration, manifests, docs, tests, and durable formats |
| documentation structure and links | repository documentation checks |
| generated reference sync | regeneration plus clean diff or repository sync check |
| dependency direction | manifest, import, or topology check |

One broad command is not automatically evidence for every acceptance. Explain the connection.

Use the narrowest evidence set that covers the changed claims. Quality comes from matching the failure surface, not maximizing test count.

## Verify the real consumer path

Leaf tests can pass while a feature remains unreachable. Trace the layers that actually exist:

```text
public contract → implementation/provider → registration/composition
→ consumer → persistence → user/model-visible behavior
```

Do not invent missing layers to satisfy the template.

## Separate mechanical and semantic claims

Automate only determinate invariants such as status format, links, generated synchronization, dependency direction, or removed registration.

Do not add a generic validator, benchmark, replay system, snapshot framework, or synthetic evaluation merely because the loop requires evidence. Add deterministic automation only when an important mechanically decidable rule is uncovered and likely to drift.

Human or agent review still decides whether the problem matters, alternatives are genuine, acceptance matches user intent, and evidence addresses the likely failure.

## Completion language

- “Passed: `<command>`” only after successful execution.
- “Inspected: `<path>`” for static evidence.
- “Not run: requires `<condition>`” for unavailable checks.
- “Inferred from `<evidence>`” only for a clearly narrower inference.

Never claim implementation solely because a record changed status or a format check passed.
