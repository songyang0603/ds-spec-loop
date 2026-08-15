# Documentation discipline

The distributed spec works only when each fact has one owner and historical material does not crowd out current truth.

## Separate current facts from rationale

- Put current system topology in architecture and subsystem docs.
- Put public usage and contract details in package docs, types, and generated references.
- Put why, alternatives, and consequences in active implemented notes.
- Put agent procedure in instructions and Skills.
- Put executable observations in tests, snapshots, and runnable examples.
- Keep archive out of ordinary current-state search unless history is explicitly needed.

Link to an owner instead of copying detailed content into multiple files.

## Avoid spec-speak after implementation

Implemented documentation should describe present reality. Remove:

- completed checklists and migration plans;
- predictions written as current facts;
- empty TODOs and speculative roadmap sections;
- `Proposal`, `Acceptance criteria`, or `Risks` headings in implemented notes;
- stale inventories better produced from source;
- repeated API reference copied into decision rationale.

Preserve real deferred work as proposed work or a precisely scoped current limitation. Do not hide it by changing tense.

## Use generated references deliberately

Generate exhaustive inventories when source can produce them reliably. Treat the generator/source as canonical and add a freshness check; do not hand-edit generated output into a second authority.

Human-written current-state docs should explain ownership and composition, not duplicate every generated entry.

## Control documentation growth

When instructions or docs become difficult to load and maintain:

1. remove duplication and stale history;
2. move detail to its correct artifact tier;
3. tighten language while preserving complete propositions;
4. split by subsystem with clear navigation;
5. only then raise a documented budget or ceiling when the information genuinely earns it.

A document budget is a mechanical pressure against unbounded growth, not proof of clarity or correctness. Do not invent numerical ceilings for a repository without observing its context constraints and maintenance pattern.

## Keep alternatives real

Alternatives must have been plausible under the problem and constraints. One bold-led paragraph per alternative is usually enough. Do not create straw alternatives or generic claims such as “do nothing is worse” merely to satisfy a template.

## Prefer search over fragile indexes

Lifecycle/class directories, descriptive filenames, relative links, and repository search often provide adequate discovery. Do not add a hand-maintained or generated central index unless it solves an observed navigation problem and has a clear freshness owner.

## Review what gates cannot decide

Human or agent review still owns:

- whether the problem is correctly framed;
- whether a decision serves the real consumer;
- whether alternatives and trade-offs are honest;
- whether acceptance criteria match user intent;
- whether evidence actually addresses the likely failure;
- whether a note remains worth keeping active.
