# Adopting the Spec loop in a repository

Map responsibilities onto the host repository before adding files. Portability changes names, paths, commands, and mechanical tooling; it does not weaken the requirement that every non-mechanical change creates or updates one owning decision record.

## Responsibility mapping

1. Read repository and subtree instructions.
2. Locate existing Specs, RFCs, proposals, design docs, ADRs, and decision records.
3. Locate current architecture, API, package, and user documentation.
4. Locate focused test commands, real product paths, generated outputs, and complete CI checks.
5. Assign an existing artifact to each responsibility in [system-of-authority.md](system-of-authority.md).
6. Report overlaps and gaps before creating a parallel system.

Examples:

| Responsibility | Possible host form |
|---|---|
| repository rules | `AGENTS.md`, `CLAUDE.md`, Copilot instructions |
| working proposal | Spec, RFC, proposal, design doc |
| stable decision | ADR, decision record, implemented design |
| current documentation | architecture docs, README, API docs |
| focused evidence | `pytest`, `cargo test`, `go test`, `pnpm test`, real CLI/UI/API flow |
| complete checks | GitHub Actions, Makefile, pre-commit, repository scripts |

Never prescribe a command from another ecosystem. Discover commands from the repository's manifests, contributor docs, and CI.

## Reuse before extending

- If existing ADR/RFC conventions cover the responsibility, use them.
- If ADRs cover only architecture but non-mechanical bug, process, or test decisions lack an owner, propose a small extension to the existing decision policy rather than silently overloading ADRs or creating an unrelated tree.
- If working proposals and stable decisions are separate files, link them and choose one current rationale owner after delivery.
- If repository instructions conflict with the Skill, surface the conflict. Do not silently override higher-priority local policy.

## Minimal fallback

Only when no equivalent convention exists, propose a minimal generic structure such as:

```text
<repository instruction file>
docs/
├── architecture.md
└── decisions/
    ├── README.md
    └── yyyy-mm-dd-topic.md
```

Use a status field in each decision record to express proposed, implemented/current, or rejected meaning. Names may change to match the host. Do not pre-create empty class folders, an archive, a generated index, validators, translations, or checksum manifests.

The fallback decision-policy README defines:

- when a record is required;
- lifecycle semantics and host status words;
- filename convention;
- working, current, and declined content expectations;
- replacement and consolidation;
- link style;
- historical-retention policy when one becomes necessary.

## Standing adoption

For team-wide use, put the strict rule in repository instructions:

> Every non-mechanical change creates or updates one owning decision record in the same bounded change. Reuse existing decision conventions and update the current implementation, evidence, and documentation together.

A user may also invoke the Skill for one bounded change. Do not introduce a lighter method or switch policies task by task.

## Mechanical checks

Use existing repository checks first. Add automation only when a rule is important, mechanically decidable, uncovered, and likely to drift. Good candidates may include link resolution, status-format consistency, generated-reference synchronization, forbidden dependency direction, or absence after removal.

Do not automate semantic judgment such as problem quality, alternative plausibility, user value, or test adequacy.

## Gradual adoption

Do not rewrite all historical decisions. Apply the loop to the next non-mechanical change, repair nearby active authority as work touches it, and preserve existing history. Gradual adoption changes how much history is migrated, not which future changes require an owner.
