# Repository authority system

DS Spec Loop uses a distributed specification. Each artifact answers a different question; overlap is acceptable only when ownership remains clear.

## Artifact ownership

| Artifact | Owns | Must not become |
|---|---|---|
| Root and subtree agent instructions | Durable rules, architecture invariants, commands, scope map | A task diary or giant design document |
| Architecture and subsystem docs | Current system map, public contracts, ownership, composition | Proposal history or unbuilt wishes |
| Proposed Agent Note | Problem, candidate decision, alternatives, acceptance, risks | A claim that work shipped |
| Implemented Agent Note | Shipped decision, rejected alternatives, consequences, current factual locations | A migration checklist or future plan |
| Rejected Agent Note | Evaluated proposal and the reason it lost | Current contract |
| Archived Agent Note | Frozen historical rationale | Current authority |
| Source, types, config, manifests | Executable structure and contract | The only explanation of why |
| Tests, snapshots, runnable examples | Observable behavior and regressions | Complete decision rationale |
| Generated references | Mechanically derived current inventory | A hand-edited parallel truth |
| Gates and CI | Mechanically decidable invariants | Proof of product or semantic correctness |
| Issue/PR | Work intake and delivery summary | Permanent architecture authority |
| Repository-local Skill | Repeatable agent procedure | Runtime contract or completion evidence |

## One home for each fact

Assign a canonical home before editing:

- “What can callers rely on now?” belongs in public types and current-state docs.
- “Why this design instead of another?” belongs in an active implemented note.
- “What would prove this behavior?” belongs in acceptance language and executable evidence.
- “How should an agent perform this recurring task?” belongs in instructions or a Skill.
- “What was considered and declined?” belongs in a rejected or still-active decision note.

Other artifacts may link to the owner or summarize it briefly. Do not maintain two independent detailed copies.

## Authority precedence

When artifacts disagree, do not silently choose the most convenient one. Use this investigation order:

1. Read the governing repository instructions.
2. Identify the public contract and actual assembled runtime path.
3. Run or inspect the closest executable evidence.
4. Read the active owning decision note for rationale.
5. Read Git history, rejected notes, and archive for historical explanation.
6. Surface the contradiction and repair every current authority in the same change.

Code can reveal what exists, but not always what is intended. A note can reveal intent, but not prove that the runtime still follows it. Current truth requires both.

## Current-state convergence

A non-trivial change is not converged until all changed facts have one current owner and all dependent summaries agree. Typical drift checks include:

- note paths and names match the tree;
- README examples match public types and defaults;
- registrations and generated catalogs expose the same surface;
- tests exercise supported behavior rather than deleted compatibility;
- instructions name commands and directories that still exist;
- proposed notes do not describe already-shipped work;
- implemented notes do not promise unbuilt work.

## Progressive repository context

Keep root instructions short and navigational. Put detailed rules close to the subtree they govern. Agents should read the root, then progressively load only relevant subsystem instructions, current docs, notes, and tests. This keeps the repository legible without reducing the spec to a single oversized file.
