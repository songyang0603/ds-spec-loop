---
name: ds-spec-loop
description: Run a complete repository-native, spec-anchored development loop inspired by DeepSeek Harness. Use for feature development, bug fixes, simplification, architecture, process, or testing work that changes behavior, contracts, structure, test strategy, durable formats, or decision rationale; when asked to write, review, continue, implement, reject, supersede, archive, or verify a spec/Agent Note/RFC/ADR; or when code, tests, current-state docs, and decision rationale must converge in one change. Also use for read-only spec-to-code drift checks. Do not create a spec for a purely mechanical local edit that changes none of those things.
---

# DS Spec Loop

Treat the spec as a repository-wide authority system, not one planning document. Keep six surfaces coherent:

- repository instructions and architecture invariants;
- current-state documentation and public contracts;
- lifecycle-managed decision notes;
- source, types, package topology, configuration, and generated artifacts;
- executable evidence such as unit, integration, replay, snapshot, and end-to-end tests;
- mechanical gates for facts a program can decide.

Preserve the user's requested boundary. `specify only`, `verify only`, `review`, `implement`, and `simplify` are different assignments. Do not silently turn one into another.

## Load the relevant reference

- Read [system-of-authority.md](references/system-of-authority.md) before changing a repository's spec system or deciding which artifact owns a fact.
- Read [agent-note-lifecycle.md](references/agent-note-lifecycle.md) whenever creating, moving, superseding, rejecting, or archiving a decision note.
- Read [decision-classes.md](references/decision-classes.md) for the class-specific content and evidence expected from feature, bug-fix, simplification, architecture, process, or testing decisions.
- Read [acceptance-and-evidence.md](references/acceptance-and-evidence.md) before writing acceptance criteria, implementing a spec, or verifying completion.
- Read [simplification.md](references/simplification.md) for removal, consolidation, replacement, or “clean up” work.
- Read [documentation-discipline.md](references/documentation-discipline.md) when adding or restructuring instructions, current-state docs, references, generated docs, or archive policy.
- Read [adoption.md](references/adoption.md) when installing this method into a repository that has no equivalent conventions.
- Use [templates.md](references/templates.md) when authoring repository artifacts. Adapt names and paths to existing repository conventions.

## Reconstruct repository authority first

1. Read the root instructions, then every more-specific instruction file governing the target subtree.
2. Map the relevant current-state documents, public types/contracts, source entry points, assembly/composition path, tests, generated outputs, and gates.
3. Search active proposed, implemented, and rejected decision records before creating one. Find the note that already owns the decision; update it instead of duplicating it.
4. Treat archived records and Git history as historical evidence, not present authority.
5. Inspect history when the current tree cannot explain intent, rejected alternatives, a first-proposed date, or a suspected drift.
6. State unresolved contradictions before building on them. Prefer direct repository evidence over issue prose or stale plans.

Do not begin from a preferred implementation. First write a problem statement that remains true if the preferred solution is removed.

## Decide whether the change needs an Agent Note

Create or update a note in the same change whenever work alters behavior, architecture, a cross-file or cross-package contract, tooling/process, test strategy, durable/on-disk/wire/configuration format, or a decision maintainers may revisit.

Exempt only purely mechanical or local edits with no change to behavior, contract, structure, process, test strategy, or rationale. Do not use effort, diff size, or file count as the discriminator.

Classify the owning decision as exactly one of:

- `feature`: new user- or model-facing capability;
- `bug-fix`: defect correction or postmortem gap closure;
- `simplification`: removal of code, behavior, or surface area without adding a capability;
- `architecture`: structural decision about shipped source and runtime boundaries;
- `process`: tooling, policy, or workflow around the code;
- `testing`: test infrastructure or test strategy.

Use the host repository's established names if it already has an equivalent taxonomy. Otherwise follow [adoption.md](references/adoption.md).

After classifying, apply the class-specific investigation and evidence requirements in [decision-classes.md](references/decision-classes.md). Classification is not only a folder name; it identifies the durable decision and the most likely failure surfaces.

## Establish the owning decision

For substantial future work, create or repair a proposed note before implementation. Record:

- a solution-independent problem;
- the proposed decision and affected ownership boundaries;
- genuine alternatives and why they lose;
- observable acceptance criteria;
- risks, trade-offs, and intentionally surrendered capability.

For a decision already shipped in the same small change, an implemented note may be created directly. Do not mislabel partial work as implemented.

Keep one owning note per decision. A note may contain bespoke technical sections—topology, protocol, schema, invariants, migration—but the lifecycle skeleton remains intact. Do not invent fake alternatives to satisfy a heading; investigate the record or say what evidence is unavailable.

## Bind acceptance to falsifying evidence

For every acceptance statement, identify:

1. the observable behavior or absence that would make it true;
2. the layer where it can fail;
3. the direct evidence that can falsify it;
4. the exact command, inspection, or runtime path used to obtain that evidence.

Match evidence to the failure surface:

- local logic and invariants → unit tests;
- provider/loader/package composition → integration or composition tests;
- persistence, recovery, or event reconstruction → replay/resume tests;
- model- or user-visible behavior → runnable example plus stable snapshot;
- external service behavior → real end-to-end test when access exists, otherwise an explicit unverified boundary;
- deletion → negative search, absent path/registration/manifest/catalog/reference, and preserved replacement behavior;
- documentation or generated-reference promises → repository-native sync checks;
- architectural dependency direction → manifest/import/topology checks.

Static source inspection is evidence about source, not proof of runtime behavior. A passing format gate is evidence about encoded format rules, not semantic agreement between spec and implementation.

## Change the complete assembled path

Implement through the repository's actual composition path, not only a leaf module. Trace definition, provider, registration/loader, consumer, persistence, and UI/model exposure where they exist.

In the same change, update every authority surface whose fact changed:

- source and public types/contracts;
- relevant tests, fixtures, snapshots, and generated outputs;
- current-state architecture or package documentation;
- the owning decision note;
- repository instructions or gates when the durable workflow itself changed.

Keep the patch scoped to the decision. Record unrelated discoveries instead of folding opportunistic refactors into the change.

## Review against the real consumer

Before claiming completion:

1. Re-read the user request and owning note without looking at the implementation first.
2. Check each acceptance criterion against direct evidence.
3. Trace at least one real assembled execution path for user- or model-visible behavior.
4. Check negative guarantees: what must no longer exist, happen, or be reachable.
5. Review from the caller, model, user, and future maintainer perspective—not only the implementing module.
6. Run the narrow relevant checks locally; leave unrelated full matrices to the repository's established CI unless the user requests them.
7. Report commands actually run, meaningful outputs, skipped checks, and remaining uncertainty. Reserve “passed” for an executed check; describe manual source/doc comparison as “inspected” with exact paths. Never translate “not run” into “passed.”

## Converge lifecycle and current truth

After the implementation and evidence agree, move `proposed` to `implemented` and rewrite it as present truth:

- change `Proposal` to `Decision`;
- replace future plans with what actually shipped;
- fold acceptance and risks into present-tense consequences and testing/verification;
- update paths, package names, defaults, contracts, and other factual locations;
- preserve why the decision won and what it gave up.

If the proposal is declined, move it to `rejected`, put the concise reason in the status, and preserve the evaluated proposal and alternatives. If a decision changes, supersede it with a new cross-linked note; do not edit the old note into its opposite.

Archive only implemented decisions whose rationale is unlikely to guide future work. Keep active any note that still owns an alternative, boundary, negative guarantee, durable or wire semantic, security rule, reintroduction condition, or named coverage gap. Never use archived text as current authority.

Finish by checking that current-state docs describe current behavior, active notes describe current decisions, tests pin observable promises, and no proposed text falsely reads as completed.

## Report the outcome

Lead with what is now true. Then identify:

- the owning decision note and lifecycle transition;
- behavior and authority surfaces changed;
- acceptance evidence and commands actually run;
- explicit gaps, blockers, or work deliberately left proposed.

Do not call a phase complete merely because Markdown exists or a checker exits zero.
