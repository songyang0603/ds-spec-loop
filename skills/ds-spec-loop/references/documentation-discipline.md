# Documentation discipline

The distributed Spec works only when each fact has one owner and historical material does not crowd out current truth.

## Separate current facts from rationale

- Put current topology and behavior in architecture, API, package, and user documentation.
- Put public contracts in types, schemas, generated references, and current docs.
- Put why, alternatives, and consequences in the owning stable decision.
- Put agent procedure in repository instructions and Skills.
- Put executable observations in tests, examples, snapshots, and runtime checks.
- Keep historical records out of ordinary current-authority search unless history is requested.

Link to an owner instead of copying detailed content.

## Keep decision ownership coarse enough

Before creating a decision record, ask:

- Does an existing record already own the problem or contract?
- Is this only a follow-up implementation, bug, test layer, or factual location update?
- Does the proposed record have an independent problem, real alternatives, consequences, and reversal boundary?
- Could future maintainers meaningfully replace this decision without replacing its parent?

Changed files, phases, and test surfaces do not get separate records by default.

## Remove proposal language after delivery

Current documentation and stable decisions describe present reality. Remove:

- completed checklists and migration plans;
- predictions written as facts;
- empty TODOs and speculative roadmap sections;
- proposal and acceptance headings from a stable decision;
- stale inventories better derived from source;
- repeated API references copied into rationale.

Preserve deferred work as a working proposal or precise current limitation.

## Use generated references deliberately

Generate exhaustive inventories when source can produce them reliably. Treat source and generator as canonical, add freshness checks only when justified, and do not hand-edit generated output into a second owner.

## Control growth

When documentation becomes difficult to load:

1. remove duplication and stale history;
2. move detail to its owning artifact;
3. tighten language while preserving complete propositions;
4. split by subsystem with clear navigation;
5. add or raise a budget only when the information earns the space.

Do not create central indexes, archive machinery, or numerical budgets without an observed problem and clear owner.

## Keep alternatives real

Alternatives must have been plausible under the problem and constraints. Do not invent “do nothing” or other straw alternatives to satisfy a template.

## Review what checks cannot decide

Review still owns whether:

- the problem is framed correctly;
- the decision serves the real consumer;
- alternatives and trade-offs are honest;
- acceptance matches user intent;
- evidence addresses likely failure;
- a historical record remains worth keeping.
