# Acceptance and evidence

Acceptance criteria are useful only when they can be contradicted by an observation. “Implement X,” “add tests,” and “update docs” are tasks, not acceptance criteria.

## Write observable acceptance

Good acceptance language identifies:

- actor or caller;
- starting state and input;
- observable behavior or absence;
- durable or compatibility effect when relevant;
- failure behavior and negative guarantee;
- boundary beyond which the claim is not made.

Example:

> When the application loads the local provider through its production composition path, the consumer receives the declared capability; disposing the registration removes that capability, and replaying a recorded session reconstructs the same model-visible input without contacting an external service.

This can fail in registration, composition, disposal, persistence, replay, or model projection. Each surface needs matching evidence.

## Build an evidence map

Use a compact table in the proposed note or implementation working state:

| Acceptance | Failure surface | Direct evidence | Result |
|---|---|---|---|
| Consumer receives capability through real loader | assembly and provider selection | composition test through production loader | record actual result |
| Disposal removes capability | lifecycle cleanup | dispose/unregister assertion | record actual result |
| Replay reconstructs model input | persistence and projection | session replay test or runnable replay | record actual result |
| Removed API is absent | source, exports, docs, catalogs | negative search plus relevant build/tests | record actual result |

Write actual commands and outcomes. If evidence cannot run because a key, platform, environment, or authority is missing, mark that boundary plainly; use lower-layer evidence only for the narrower claim it supports.

## Match evidence to the risk

| Risk | Best primary evidence |
|---|---|
| Parsing, transformation, local invariant | unit test |
| Package/provider/loader composition | integration or composition test |
| Persistence, resume, event ordering | replay/resume test |
| Model-visible text, tools, or prompt | runnable keyless example and stable snapshot |
| User-visible UI flow | real application flow, interaction test, or screenshot when appropriate |
| External provider contract | real-API end-to-end test when available |
| Complete removal | negative search across source, registrations, manifests, catalogs, docs, tests, durable formats |
| Documentation structure and links | static documentation gate |
| Generated reference sync | regeneration plus clean diff or repository sync gate |
| Dependency direction | manifest/import/topology check |

One broad test command is not automatically evidence for every acceptance criterion. Explain the connection.

## Verify the assembled path

Leaf tests can pass while the feature is unreachable. For user- or model-visible behavior, trace the whole available path:

```text
contract/definition → provider → registration/loader → consumer → persistence → projection/UI
```

Not every repository has every layer. The requirement is to find the real assembled path rather than stop at the modified module.

## Separate mechanical and semantic claims

Automate only determinate invariants:

- lifecycle directory matches status;
- required headings exist;
- active links resolve;
- generated output matches source;
- forbidden dependency direction is absent;
- deleted registration or path is absent.

Do not let a generic checker decide whether the problem matters, alternatives are genuine, acceptance matches user intent, or tests prove runtime semantics. Those require repository-grounded review.

## Completion language

Use precise statements:

- “Passed: `<command>`” only after running it successfully.
- “Inspected: `<file/path>`” for static evidence.
- “Not run: requires `<missing condition>`” for unavailable runtime evidence.
- “Inferred from `<evidence>`” only when the narrower inference is useful and clearly not direct verification.

Never claim that a spec is implemented because the note moved folders or a format validator passed.
