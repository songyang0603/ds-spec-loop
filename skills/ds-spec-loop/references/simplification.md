# Simplification as a spec-driven change

Deletion and consolidation change contracts, ownership, and future options. Treat them as decisions, not housekeeping.

## Establish a deletion candidate

Collect evidence before removing:

- production consumers and registrations;
- public exports, types, configuration, manifests, catalogs, and generated references;
- durable/on-disk/wire state and migrations;
- tests that exercise supported behavior versus tests that only self-test the candidate;
- current docs and examples;
- compatibility shims and fallback paths;
- original motivation and plausible reintroduction conditions.

A surface used only by its own tests may be a candidate, but the test can also document a contract. Investigate why the contract existed.

## Compare real alternatives

At minimum evaluate:

- keep as-is;
- narrow or internalize the contract;
- replace it with an existing owner;
- remove it completely.

Prefer the smallest contract that preserves required observable behavior. Do not use line count or package count as the sole decision metric.

## Specify negative acceptance

A removal is complete only when the old capability is absent from every authority surface that could keep it alive. Acceptance should cover, when relevant:

- source path and exports are absent;
- provider registration and consumer lookup are absent;
- manifests, catalogs, generated references, examples, and current docs no longer advertise it;
- durable data, migrations, wire fields, and compatibility handling are removed or intentionally retained and documented;
- replacement behavior remains observable;
- no supported-behavior test still presents the removed surface as current.

Use negative search as evidence, but search broadly enough to include naming variants and conceptual aliases. A zero-result search proves only the query searched.

## Preserve the decision value

The implemented simplification note should record:

- why the surface no longer earned its cost;
- alternatives to full removal;
- the capability and compatibility given up;
- what replaced or absorbed the ownership;
- how complete absence was checked;
- conditions that would justify reintroduction.

If production consumers still exist or the evidence is ambiguous, retaining the surface with a documented reason is a valid result. Do not force deletion to satisfy the task label.

## Keep the patch narrow

Avoid mixing unrelated cleanup into the deletion. Net deletion is valuable when it reduces concepts and maintenance burden, not when removed code is replaced with speculative abstraction.
