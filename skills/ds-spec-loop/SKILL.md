---
name: ds-spec-loop
description: Run a strict repository-native Spec programming loop that keeps requirements, owning decisions, implementation, tests, and current documentation consistent in one bounded change. Use when explicitly invoked; when repository instructions require a Spec, RFC, ADR, proposal, design doc, or decision record for non-mechanical changes; when implementing, revising, rejecting, replacing, retiring, simplifying, or verifying such a decision; or when auditing Spec-to-code drift. Do not use for a purely mechanical or local edit that changes no behavior, contract, structure, process, test strategy, durable format, or rationale.
---

# Repository-native Spec loop

Treat the Spec as a distributed repository authority system, not one planning document. Keep these responsibilities coherent:

- repository instructions and architecture invariants;
- working proposals and stable decision rationale;
- current documentation and public contracts;
- source, types, configuration, package topology, and generated artifacts;
- executable evidence such as unit, integration, replay, snapshot, and end-to-end tests;
- repository checks and CI for facts a program can decide;
- Git and change-review history for chronology.

Preserve the user's requested boundary. `specify only`, `verify only`, `review`, `implement`, and `simplify` are different assignments. Do not silently turn one into another.

Preserve the strict loop across repositories. Adapt names, paths, commands, and mechanical checks to the host repository; do not weaken the rule that every non-mechanical change creates or updates one owning decision record.

## Load the relevant reference

- Read [system-of-authority.md](references/system-of-authority.md) before deciding which artifact owns a fact or changing a repository's Spec system.
- Read [decision-record-lifecycle.md](references/decision-record-lifecycle.md) when creating, accepting, rejecting, replacing, consolidating, retiring, or archiving a decision.
- Read [requirement-change.md](references/requirement-change.md) when a user correction, review finding, failed premise, measurement, or implementation discovery changes the accepted direction.
- Read [decision-classes.md](references/decision-classes.md) for class-specific investigation and evidence.
- Read [acceptance-and-evidence.md](references/acceptance-and-evidence.md) before writing acceptance criteria, implementing a proposal, or verifying completion.
- Read [simplification.md](references/simplification.md) for removal, consolidation, replacement, or cleanup work.
- Read [documentation-discipline.md](references/documentation-discipline.md) when adding or restructuring instructions, current docs, references, generated docs, or historical records.
- Read [adoption.md](references/adoption.md) when a repository has no equivalent conventions or wants this loop as a standing rule.
- Use [templates.md](references/templates.md) only when the repository has no equivalent templates.

## Reconstruct repository authority first

1. Read the root repository instructions, then every more-specific instruction file governing the target subtree.
2. Reconstruct the requested outcome, explicit non-goals, and unresolved product or architecture choices. Ask before freezing a direction when a missing choice materially changes the result.
3. Map the relevant working proposals, stable decisions, current docs, public contracts, source entry points, real composition path, tests, generated outputs, and repository checks.
4. Search existing Spec, RFC, proposal, design-doc, ADR, and decision-record conventions before creating anything. Reuse the repository's names and lifecycle.
5. Find the record that already owns the decision. Update it instead of creating a parallel record.
6. Assign one canonical home to every mutable fact. Other surfaces may summarize or link; they do not become independent detailed copies.
7. Treat historical records and Git history as context, not present authority.
8. State unresolved contradictions before building on them. Prefer direct repository evidence over stale plans or issue prose.

Do not begin from a preferred implementation. First state a problem that remains true if the preferred solution is removed.

## Cover every non-mechanical change

Create or update one owning decision record in the same PR or bounded change whenever work alters behavior, architecture, a contract shared across files or packages, tooling/process, test strategy, durable/on-disk/wire/configuration format, or another decision a maintainer may reasonably revisit.

Exempt only a purely mechanical or local edit with no change to behavior, contract, structure, process, test strategy, durable format, or rationale. Do not use effort, diff size, elapsed time, or file count as the discriminator.

Use the host repository's established decision classes. If none exist, choose one primary class from [decision-classes.md](references/decision-classes.md). Classification identifies the decision and likely failure surfaces; it does not require a particular directory tree.

Before creating a new record, prove that no active record already owns the decision. When an owner exists, create a separate record only for an independently revisitable problem with its own real alternatives, consequences, or stable contract. When no record or equivalent contract artifact owns a non-mechanical correction, create a narrowly scoped bug-fix decision owner. A changed file, module, implementation phase, test layer, follow-up fix, or release step is not automatically a separate decision.

## Establish the owning proposal or decision

For substantial future work, create or repair a working proposal before implementation. Record:

- a solution-independent problem;
- the proposed direction and affected ownership boundaries;
- genuine alternatives and why they lose;
- observable acceptance criteria;
- risks, trade-offs, and intentionally surrendered capability.

For a small decision already made in the same bounded change, create or update the stable decision record directly if the repository's convention allows it. Do not describe partial work as current behavior.

Keep one owner per decision. Add bespoke technical sections only when the decision needs topology, protocol, schema, invariants, migration, or compatibility detail. Do not invent alternatives to satisfy a template; investigate the record or state that the evidence is unavailable.

When an outcome is empirically unknown, do not fabricate the final decision in advance. Record the problem, candidate direction, observation method, acceptance boundary, and stopping condition; run the bounded experiment; then write the stable decision from the observed result.

## Handle changed requirements and discoveries

Before continuing after a correction or discovery, read [requirement-change.md](references/requirement-change.md) and reconcile the delta.

- Inside one uncompleted PR or change stack, revise the living proposal rather than creating a permanent replacement chain.
- Identify which outcomes and acceptance criteria remain, change, or are withdrawn.
- Classify existing code, tests, and docs as retained, revised, removed, or historical.
- Ask the decision owner before accepting a new external dependency, recurring cost, privacy exposure, compatibility loss, product direction, or other material trade-off not already authorized by repository policy.
- After a stable decision has shipped, create a new replacement decision and cross-link it; never rewrite history as though the earlier decision never existed.

## Bind acceptance to direct evidence

For every acceptance statement, identify:

1. the observable behavior or absence that would make it true;
2. the layer where it can fail;
3. the direct evidence that can falsify it;
4. the exact repository-native command, inspection, or runtime path used to obtain that evidence.

Match evidence to the failure surface:

- local logic and invariants → focused unit tests;
- package, service, loader, or runtime composition → integration or composition tests;
- persistence, recovery, or event reconstruction → replay/resume tests;
- user- or model-visible behavior → the real runnable product path and stable output evidence;
- external service behavior → real end-to-end evidence when access exists, otherwise an explicit unverified boundary;
- deletion → negative search plus absence from source, exports, registration, manifests, docs, tests, and durable formats;
- documentation or generated-reference promises → the repository's own synchronization checks;
- dependency direction → manifest, import, or topology checks.

Static source inspection is evidence about source, not proof of runtime behavior. A passing format check proves only the encoded format rule, not semantic agreement.

Use the smallest direct evidence set that covers the changed claims. Do not add a validator, benchmark, replay system, snapshot framework, or synthetic evaluation merely to make the change look rigorous. Add deterministic automation only when an important mechanically decidable rule lacks an existing owner and is likely to drift.

## Change the complete consumer path

Implement through the repository's real composition path, not only a leaf module. Trace the applicable chain:

```text
public contract → implementation/provider → registration/composition
→ consumer → persistence → user/model-visible behavior
```

Not every repository has every layer. Follow only layers that exist.

In the same PR or bounded change, update every authority surface whose owned fact changed:

- source and public contracts;
- relevant tests, fixtures, snapshots, and generated outputs;
- current architecture, package, API, or user documentation;
- the owning proposal or decision;
- repository instructions or checks when the durable workflow itself changed.

Keep the patch scoped to the decision. Record unrelated discoveries instead of folding opportunistic refactors into the change.

The convergence unit is the PR or bounded change stack, not each intermediate commit. Checkpoint commits may isolate implementation, review fixes, measurements, or lifecycle rewriting as long as the complete change converges before delivery.

## Review against the real consumer

Before claiming completion:

1. Re-read the user request and owning proposal without looking at the implementation first.
2. Check each acceptance criterion against direct evidence.
3. Trace at least one real assembled execution path for user- or model-visible behavior.
4. Check negative guarantees: what must no longer exist, happen, or be reachable.
5. Review from the caller, user/model, operator, and future maintainer perspectives.
6. Run the narrow relevant checks locally; leave unrelated full matrices to established CI unless the user requests them or the change is irreducibly repository-wide.
7. Report commands actually run, meaningful outcomes, skipped checks, and remaining uncertainty. Reserve “passed” for executed checks.

## Converge lifecycle and current truth

After implementation and evidence agree, rewrite the working proposal as a stable decision according to the repository's convention:

- when one file carries both stages, rewrite its title and semantic sections; never change only the status word;
- replace future proposal language with the decision that actually shipped;
- fold acceptance and risks into present-tense consequences and verification;
- update paths, names, defaults, contracts, and other factual locations;
- preserve why the decision won and what it gave up.

If the proposal is declined, retain the evaluated proposal and concise rejection reason only while that rationale prevents a plausible repeated mistake.

Supersession is a relationship between decisions, not a required status or directory. A stable replacement gets a new cross-linked record. Partial replacement keeps both records current and states which clauses each owns. Fully consolidate, retire, or archive an old record only after the current owner preserves every unique rationale, alternative, consequence, verification obligation, coverage gap, reintroduction condition, and inbound link.

Finish by checking that current docs describe current behavior, stable decisions describe current rationale, tests pin observable promises, and working proposals do not falsely read as completed.

## Report the outcome

Lead with what is now true. Then identify:

- the owning proposal or decision and its lifecycle change;
- whether the work updated an existing owner or justified a new one;
- any requirement delta and the authority that approved it;
- behavior and authority surfaces changed;
- acceptance evidence and commands actually run;
- explicit gaps, blockers, or work deliberately left proposed.

Do not call work complete merely because a document exists or a checker exits zero.
