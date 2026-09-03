# GitHub Repository Governance & Release Confidence

## Purpose

Turn an existing software repository into a controlled, verifiable engineering system rather than relying on local discipline or an agent's claim that the project is "done".

Use this skill when reviewing, hardening, or preparing a repository for continued development by humans or coding agents.

The goal is not bureaucracy. The goal is to make the repository's health, release readiness, and regression protection **observable and enforceable**.

## Core principles

1. **GitHub is part of the engineering system.** Repository settings, pull requests, Actions, tags, releases, and branch rules matter alongside source code.
2. **Local green is not release confidence.** A developer or coding agent running tests locally is evidence, not enforcement. Important checks should execute in CI.
3. **Protect the production branch.** The primary branch should not be an unrestricted landing zone for unverified changes.
4. **Make quality gates explicit.** Define the exact checks that must pass before merging or releasing.
5. **Use evidence, not claims.** Do not say "CI is passing", "tests are green", or "the release is ready" without inspecting the corresponding GitHub evidence.
6. **Separate fast feedback from deep verification.** Keep required PR checks reasonably fast, while preserving heavier E2E, integration, migration, import, stateful, or smoke tests as appropriate release gates.
7. **Agents must leave a trace.** Agent-driven changes should be reviewable through branches, commits, PRs, checks, and concise summaries of verification performed.
8. **Prefer deterministic verification.** Pin runtimes/dependencies where practical and make verification commands reproducible from a clean checkout.
9. **Do not weaken safeguards to make a check green.** Fix the underlying failure or explicitly document why a check is intentionally non-blocking.
10. **Release readiness is a state, not a feeling.** A release should have a known commit, known checks, known version, and a clear rollback/recovery path.

## Initial repository audit

Before changing anything, inspect:

- default branch
- current HEAD commit
- recent commit history
- open and recently closed pull requests
- open issues relevant to reliability/release work
- GitHub Actions workflows
- latest workflow runs for the default branch and recent PRs
- commit status/check results
- branch protection/rulesets
- tags and releases
- package/build/test scripts
- deployment configuration
- contribution/development documentation

Record facts separately from assumptions.

### Minimum health questions

Answer these before proposing hardening:

```text
What is the production/default branch?
What commit is currently at its tip?
What automated checks exist?
Which checks actually run in GitHub?
Which checks are required before merge?
Can the default branch be changed without passing those checks?
Are release artifacts/tags deterministic?
Can a fresh checkout reproduce the documented verification?
```

## CI design

A healthy repository should have a GitHub Actions workflow triggered for pull requests and pushes to the protected production branch.

### Baseline required pipeline

Adapt the commands to the repository's actual stack, but preserve the intent:

```text
install dependencies
  ↓
static validation
  ├─ lint
  └─ type-check / compile
  ↓
tests
  ├─ unit
  └─ integration where practical
  ↓
production build
  ↓
optional smoke/E2E gate
```

For JavaScript/TypeScript repositories, a common baseline is:

```bash
npm ci
npm run lint
npm run type-check
npm test -- --runInBand
npm run build
```

Do not invent scripts. First inspect `package.json`, repository documentation, and workflow files. Use the project's actual commands.

### Deep verification

Where the repository exposes specialized checks, incorporate them deliberately:

- end-to-end browser tests
- database migration tests
- import/ETL regression tests
- stateful/audit tests
- API contract tests
- accessibility checks
- production smoke tests
- security scans

Not every deep check must block every PR, but every release-critical behavior must have an explicit verification path.

## PR and branch protection

The production branch should normally:

- require pull requests rather than direct pushes
- require successful CI checks
- require the branch to be up to date before merge when appropriate
- prevent force pushes
- prevent branch deletion
- require at least one review when there is meaningful multi-person collaboration
- apply CODEOWNERS where ownership is important

For solo repositories, do not add ceremony that provides no value. A single required CI gate is still valuable even when review count is effectively one.

### Required-check naming

Choose stable, descriptive check names, for example:

```text
CI / lint
CI / type-check
CI / test
CI / build
```

Do not frequently rename required checks after branch protection is configured; doing so can leave stale required contexts.

## Release gating

A release should be traceable to an immutable Git identity:

```text
version
  → tag/release
  → exact commit
  → successful verification
```

Before declaring a release ready, verify:

- version metadata is consistent
- release/tag points to the intended commit
- required CI checks passed for that commit
- build completed successfully
- relevant integration/E2E/regression checks passed
- release notes accurately describe shipped behavior
- rollback/recovery is understood

Never infer release readiness from the existence of a commit message such as `Release V1.0.0`.

## Agent-driven development

This skill is particularly important when coding agents are making repeated repository changes.

Require the agent to work in a traceable loop:

```text
inspect repository
  ↓
state current risks
  ↓
implement focused change
  ↓
run project verification
  ↓
push branch
  ↓
CI verifies independently
  ↓
review evidence
  ↓
merge only after gates pass
```

Agent instructions should forbid:

- declaring success solely because a local command passed
- bypassing or deleting CI checks to get green status
- force-pushing protected branches
- weakening tests without documenting the reason
- changing release/version claims without evidence
- treating generated files as proof that underlying behavior works

When an agent reports completion, inspect GitHub state independently whenever the repository is accessible.

## Regression baseline

For a mature repository, identify a minimum regression suite that protects the product's core contract.

A useful pattern is:

```text
Tier 0 — syntax / formatting / type validity
Tier 1 — unit + deterministic integration tests
Tier 2 — production build
Tier 3 — E2E / browser / API smoke tests
Tier 4 — data import / migration / stateful / release verification
```

Use the lowest sufficient tier for routine changes, but require the appropriate higher tier for changes that cross that boundary.

Examples:

```text
UI copy change       → Tier 0-2
business logic       → Tier 0-2, relevant Tier 1 tests
routing/auth change  → Tier 0-3
schema/migration     → Tier 0-4
import/data logic    → Tier 0-4
release candidate    → Tier 0-4 as supported by the project
```

## Infrastructure and configuration checks

Inspect repository configuration as code.

Look for:

- workflow triggers that accidentally exclude PRs or the default branch
- missing lockfile enforcement
- unsupported runtime versions
- permissions broader than necessary
- secrets referenced without safe handling
- deployment workflows that can bypass validation
- release jobs that run from arbitrary branches
- CI steps that silently ignore failures
- flaky tests hidden behind `continue-on-error`
- stale required status names
- unprotected production branches

Do not assume a workflow file exists merely because CI is mentioned in documentation.

## Failure analysis

When CI is missing or broken, classify the issue before fixing it:

```text
A. configuration defect
B. dependency/environment defect
C. deterministic product defect
D. flaky/non-deterministic test
E. missing test coverage
F. documentation mismatch
G. repository-policy gap
```

Fix the root cause at the correct layer.

Examples:

- A missing Node version matrix is a CI configuration problem, not an application bug.
- A failing import regression test after a schema change is probably a product/data compatibility issue.
- A passing local test with no GitHub workflow is an enforcement gap, not evidence of CI health.

## Verification commands

After changing repository governance, verify the result from GitHub rather than relying only on local state.

At minimum inspect:

```text
latest default-branch commit
↓
workflow run for that commit
↓
individual jobs/check conclusions
↓
branch protection/ruleset state
↓
open PR behavior where possible
```

For a release candidate, inspect the exact release commit rather than merely the latest branch tip.

## Documentation requirements

Keep a concise repository-level section such as:

```text
Development checks
- lint
- type-check
- tests
- build

Merge policy
- PR required
- CI required

Release policy
- release from tagged commit
- release checks required
```

Documentation must match the actual repository configuration. Do not document a safeguard that GitHub does not enforce.

## Recommended implementation sequence

When hardening a repository with weak governance:

1. Establish the actual current state.
2. Add or repair CI.
3. Confirm CI passes on a normal branch/PR path.
4. Add the required checks to the production branch protection/ruleset.
5. Add deeper release/regression checks where they provide product value.
6. Update contributor/development documentation.
7. Verify the final GitHub state independently.
8. Record any intentional exceptions.

Do not protect a nonexistent/broken check before validating that the workflow itself works.

## Validation checklist

Before declaring the repository hardened:

- [ ] Default branch identified.
- [ ] Current HEAD verified.
- [ ] CI workflow exists for relevant PR/push events.
- [ ] Required baseline checks run in CI.
- [ ] CI failures fail the workflow rather than being ignored.
- [ ] Production build is exercised.
- [ ] Relevant regression/E2E/import checks have an explicit role.
- [ ] Production branch is protected by branch rules/ruleset.
- [ ] Required status checks correspond to real workflow checks.
- [ ] Force pushes are blocked where appropriate.
- [ ] Release tags/releases map to exact commits.
- [ ] Release readiness can be independently verified.
- [ ] Documentation matches the actual configuration.
- [ ] No safeguard was weakened merely to obtain a green build.

## Anti-patterns

Avoid:

- "CI" mentioned in README but no workflow exists
- local-only verification for release-critical behavior
- unprotected production branches for mature products
- required checks that no longer run
- `continue-on-error` around meaningful correctness checks
- skipping builds because tests pass
- treating passing unit tests as proof that migrations/imports/E2E work
- creating release tags before verification
- claiming a release is healthy because a release commit exists
- bypassing branch protection for convenience
- deleting regression tests because they expose a real defect
- changing multiple unrelated governance mechanisms in one unverified step

## Practical output

When using this skill to review a repository, produce a compact engineering verdict:

```text
Repository state
  current ref / commit

CI
  present / absent / failing

Protection
  protected / unprotected

Verification
  baseline / deep checks

Release confidence
  low / medium / high

Critical gaps
  1–5 concrete findings

Next actions
  ordered remediation steps
```

The output must distinguish **implemented capability** from **enforced engineering controls**. A repository can have excellent tests and still have poor release governance if those tests are not executed and required by GitHub.
