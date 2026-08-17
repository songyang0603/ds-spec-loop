# Decision: Generalize the strict repository-native Spec loop

Status: accepted

## Problem

The original Skill preserved a strong repository-native development loop but named artifacts and lifecycle conventions from the source repository used to derive it. Runtime instructions could therefore lead agents to copy unfamiliar names, directories, statuses, or testing machinery instead of first discovering the target repository's existing instructions, Specs, RFCs, ADRs, current documentation, tests, and CI.

The earlier wording also left requirement changes, decision ownership granularity, and stable replacement underspecified. Real use produced a dedicated `superseded/` directory where a scoped replacement relationship was required, and created separate records for implementation details that could have remained under an existing owner.

The Skill must remain reusable across languages and repositories without weakening its strict core: every non-mechanical change creates or updates one owning decision record and converges requirements, implementation, direct evidence, and current documentation in one bounded change.

## Decision

`SKILL.md` and all runtime references use source-neutral responsibility terms:

- repository instructions;
- working proposal;
- decision record;
- current documentation;
- source and public contracts;
- executable evidence;
- repository checks;
- bounded change.

The Skill maps these responsibilities onto the host repository's existing artifacts and commands. It does not prescribe Node commands to another ecosystem or create a second decision tree in a repository whose Spec, RFC, ADR, or design-doc conventions already own the responsibility. When no equivalent convention exists, it proposes only a minimal generic structure: repository instructions, current architecture documentation, and decision records with Working, Current, and Declined semantics.

The strict loop remains unchanged:

- every non-mechanical change has one owning decision record;
- an existing owner is updated before another record is created;
- when no artifact owns a non-mechanical correction, a narrow bug-fix owner is created;
- the problem stands independently of the preferred solution;
- alternatives are real rather than invented;
- acceptance criteria map to direct observations;
- implementation follows the real consumer path;
- changed current authorities converge in one bounded change;
- working proposals may be revised before delivery;
- a one-file Working-to-Current transition rewrites the title and semantic sections rather than only its status;
- Current decisions retain Verification or an equivalent durable evidence mapping;
- stable decisions are replaced through new cross-linked records with explicit partial or full scope;
- obsolete rationale is consolidated or retired without competing with current truth.

Requirement changes use one generic protocol for clarification, living revision, evidence-driven refinement, independent decisions, and stable reversal. The protocol reconciles outcomes, non-goals, constraints, acceptance, source/contracts, tests/evidence, current docs, and decision authority before implementation continues.

The runtime Skill and references contain no source-repository-specific names or framework terms. The public READMEs and `NOTICE` retain transparent method attribution and the independent-community-project boundary.

The repository name and invocation remain `ds-spec-loop` for compatibility. Codex-specific UI metadata displays `Spec Loop` and uses generic wording; it does not change portable behavior or invocation policy.

## Alternatives considered

**Keep source-repository terminology inside runtime instructions and explain portability only in the README.** Rejected because agents act on `SKILL.md` and its references. Runtime terminology can still create parallel conventions in a host repository.

**Offer a lighter default that omits a durable owner for some behavioral changes.** Rejected because it changes the strict loop rather than generalizing it.

**Require one universal directory, lifecycle vocabulary, taxonomy, test command, or validator.** Rejected because those are repository encodings rather than semantic responsibilities. Host conventions and commands remain authoritative.

**Bundle a synthetic evaluation suite with the distributed Skill.** Rejected because direct evidence depends on the repository's real failure surfaces. Development-time forward tests remain outside the published package.

## Consequences

- Repositories with existing ADR, RFC, proposal, documentation, test, and CI conventions reuse them instead of receiving parallel files.
- Repositories without conventions receive a minimal fallback rather than copied class folders, archive infrastructure, indexes, validators, translations, or checksum manifests.
- Strict decision ownership remains mandatory for every non-mechanical change; portability does not become a lighter method.
- Lifecycle mapping uses semantic stages rather than status-word matching. In particular, an `accepted` ADR is not assumed to be delivered until implementation, direct evidence, and current documentation converge.
- Replacement remains a scoped relationship. A host may retain its established `superseded` status, but it must still preserve a current replacement owner, cross-links, replacement scope, and rationale.
- The Skill adds explicit requirement-change and owner-granularity protocols while reducing total runtime reference lines.
- The separately installed Skill remains unchanged while two active tasks use it. Updating or migrating that installed copy is a later user-authorized operation.

## Verification

- `quick_validate.py skills/ds-spec-loop` — passed; Skill structure and frontmatter are valid.
- YAML parsing of `agents/openai.yaml` — passed.
- `git diff --check` — passed.
- Local Markdown target scan — passed with no broken relative link.
- Runtime terminology scan for source-specific repository/framework terms and the removed lifecycle filename — zero unexpected results.
- English and Chinese README review — meaning-equivalent; one overly narrow translation of “surface” was corrected.
- Existing-ADR Python bug forward test — updated the existing ADR, used `python3 -m pytest -q`, added no parallel decision directory, and passed two tests.
- Mid-flight requirement-change forward test — the first run exposed a status-only transition; after tightening the lifecycle rule, the rerun rewrote the proposal as a Current decision, preserved the rejected array alternative, updated implementation/tests/docs, and passed `npm test`.
- Partial-replacement Rust forward test — kept the local-filesystem decision Current, added a cross-linked object-storage owner for the remote clause, removed the old HTTP implementation, and passed two `cargo test` tests.
- No-convention JavaScript forward test — added only repository instructions, `docs/decisions/README.md`, and one implemented feature decision; no archive, taxonomy tree, index, or validator was created; `npm test` passed.
- Independent maintainer review — found and closed the no-owner bug-fix gap and the missing durable Verification requirement.
- Independent bilingual/compatibility review — found no blocking issue; runtime terminology, installation paths, attribution, and cross-host structure are consistent.
- GitHub connector inspection — public `main` remains at `5704fb8`; no push or external publication occurred.
- Installed-copy audit — `/Users/songyang/.codex/skills/ds-spec-loop` was not modified, so the two referenced active tasks continue using their previously loaded version.
