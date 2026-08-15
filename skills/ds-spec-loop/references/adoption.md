# Adopting DS Spec Loop in a repository

Adopt the smallest complete authority system that fits the host repository. Reuse existing ADR, RFC, design-doc, docs, test, and CI conventions when they already provide equivalent ownership. Do not create parallel systems merely to copy directory names.

## Bootstrap layout

For a repository with no decision-note convention, start with:

```text
AGENTS.md
docs/
├── architecture.md
└── <subsystem current-state docs>
.agents/
└── notes/
    ├── README.md
    ├── proposed/<class>/
    ├── implemented/<class>/
    ├── rejected/<class>/
    └── archived/<class>/
```

Use the six default classes from [agent-note-lifecycle.md](agent-note-lifecycle.md). Create only directories the repository needs now; version control does not need empty folders.

## Root instruction contract

Keep the root instructions short. Include:

- where current architecture and subsystem docs live;
- where decision notes live and which behavior, contract, structure, process, test-strategy, durable-format, or rationale changes require one;
- high-value architecture invariants;
- build, focused test, docs-sync, and full CI commands;
- the rule that model/user-visible behavior needs evidence through a runnable assembled path;
- the rule that a proposed note becomes implemented only after source, tests, docs, and evidence converge;
- pointers to subtree instructions rather than copying their details.

Put package-specific rules in nearer instruction files.

## Note policy

Create `.agents/notes/README.md` as the local contract. Define:

- lifecycle paths and statuses;
- class set;
- filename/date convention;
- proposed, implemented, and rejected skeletons;
- supersession and consolidation rules;
- archive policy;
- link style;
- any translation or sidecar requirements.

Do not create a generated central index unless the repository has a real discovery problem that search and directory structure cannot solve.

## Mechanical gates

Start with conventions and repository-native checks. Add a gate only after a rule is both important and mechanically decidable. Good early candidates are:

- lifecycle path agrees with status;
- active note links resolve;
- implemented notes contain no proposal-only headings;
- generated docs are synchronized;
- architecture dependency rules are checkable;
- deleted paths/registrations are absent when a removal note owns that guarantee.

Prefer a small repository-specific gate over a universal validator. The host repository knows its folders, commands, generated artifacts, and exception policy.

Do not encode semantic judgment—problem quality, alternative plausibility, user value, or test adequacy—as a boolean format check.

## Gradual adoption

Do not rewrite all historical decisions. Apply the system to the next change that affects behavior, contracts, structure, process, test strategy, durable formats, or decision rationale, then repair nearby active authority as work touches it. Preserve existing history. Add automation only when repeated mechanical drift demonstrates its value.
