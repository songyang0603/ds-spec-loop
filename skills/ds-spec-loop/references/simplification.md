# Simplification as a Spec change

Deletion and consolidation change contracts, ownership, and future options. Treat them as decisions, not housekeeping.

## Establish a candidate

Investigate:

- production consumers and registration;
- public exports, types, config, manifests, catalogs, and generated references;
- durable/on-disk/wire state and migrations;
- tests that exercise supported behavior versus self-tests of the candidate;
- current docs and examples;
- compatibility shims and fallback paths;
- original motivation and plausible reintroduction conditions.

A surface used only by tests may be removable, but the test can also document a real contract. Understand why it exists.

## Compare real alternatives

At minimum evaluate:

- keep it;
- narrow or internalize it;
- replace it with an existing owner;
- remove it completely.

Prefer the smallest contract that preserves required behavior. Do not use line or package count as the sole decision metric.

## Specify negative acceptance

Removal is complete only when the old capability is absent from every relevant authority:

- source and exports;
- registration and consumer lookup;
- manifests, catalogs, generated references, examples, and current docs;
- durable data, migrations, wire fields, and compatibility handling, unless intentionally retained and documented;
- supported-behavior tests.

Confirm replacement behavior remains observable. A zero-result search proves only the query searched, so include naming variants and conceptual aliases.

## Preserve decision value

The owning simplification decision records:

- why the old surface no longer earns its cost;
- alternatives to full removal;
- capability and compatibility surrendered;
- surviving owner;
- how absence was checked;
- conditions for reintroduction.

If consumers remain or evidence is ambiguous, retaining the surface with a documented reason is valid.

## Keep the change narrow

Do not mix unrelated cleanup into the deletion. Net deletion is valuable when it reduces concepts and maintenance burden, not when removed code is replaced with speculative abstraction.
