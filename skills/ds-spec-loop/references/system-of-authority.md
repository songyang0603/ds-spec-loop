# Repository authority system

A repository-native Spec is distributed across artifacts that answer different questions. Reuse the host repository's existing owners before adding anything.

## Artifact responsibilities

| Responsibility | Possible repository forms | Owns | Must not become |
|---|---|---|---|
| Repository instructions | `AGENTS.md`, `CLAUDE.md`, Copilot instructions, contributor rules | durable rules, commands, architecture invariants, context map | task diary or full design history |
| Working proposal | Spec, RFC, proposal, design doc, draft ADR | problem, candidate direction, alternatives, acceptance, risks | a claim that unfinished work is current |
| Stable decision | ADR, decision record, implemented design, accepted-and-shipped RFC | why the current decision won, alternatives, consequences, verification obligations | API manual, migration checklist, future plan |
| Declined proposal | rejected RFC, declined proposal, rejected decision | evaluated direction and reason it lost | current contract |
| Historical record | archive, history, frozen decisions, Git | past rationale and chronology | current authority |
| Current documentation | architecture docs, README, API/package/user docs | current topology, public behavior, usage, ownership | proposal history or unbuilt wishes |
| Executable system | source, types, config, manifests, schemas | actual behavior, structure, public contract | the only explanation of why |
| Executable evidence | unit/integration/e2e tests, examples, replay, snapshots, smoke tests | observable promises, regressions, negative guarantees | complete decision rationale |
| Generated reference | generated API docs, catalogs, schema docs | exhaustive current inventory derived from a source owner | hand-edited parallel truth |
| Mechanical checks | project scripts, Makefile, pre-commit, CI | facts a program can decide | product value or semantic correctness |
| Intake and delivery | Issue, PR, commit, release note | task boundary, collaboration, chronology, delivery summary | permanent architecture authority |
| Reusable procedure | repository-local Skill, script, contributor guide | how an agent repeats a workflow | runtime contract or completion evidence |

## Map owners before editing

For each mutable fact, identify one canonical home and the surfaces that depend on it:

| Fact | Canonical owner | Dependent surfaces |
|---|---|---|
| Current caller behavior | public contract and current docs | examples and tests |
| Design rationale | owning stable decision | short references elsewhere |
| Observable promise | acceptance and executable evidence | delivery summary |
| Exhaustive inventory | source or generator | generated reference |

Updating all affected authorities does not mean copying the same volatile details into every file. Update each artifact only for the question it owns.

## Resolve disagreement

When artifacts conflict:

1. read governing repository instructions;
2. identify the public contract and real consumer path;
3. run or inspect the closest executable evidence;
4. read the active owning proposal or decision for intent and rationale;
5. inspect Git, declined proposals, and historical records;
6. surface the contradiction and repair every current authority in the same bounded change.

Code shows what exists but not always what was intended. A decision record explains intent but does not prove runtime behavior. Current truth requires the relevant owners to agree.

## Progressive repository context

Keep root instructions short and navigational. Put detailed rules close to the subtree they govern. Load only the instructions, current docs, decisions, source, and evidence relevant to the task.
