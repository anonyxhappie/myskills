# README Polisher

## Purpose

Produce and maintain repository READMEs that present a project accurately, clearly, and at a senior-engineer level without inventing capabilities, metrics, architecture, or claims.

## Core principles

1. **Evidence first** — derive claims from the repository's actual code, configuration, tests, workflows, dependencies, demos, and current behavior.
2. **Do not invent** — never fabricate benchmarks, production usage, scale, security guarantees, supported platforms, compatibility, or performance numbers.
3. **Architecture over marketing** — explain important boundaries, data flow, components, dependencies, and engineering trade-offs.
4. **Show the problem and solution** — make the repository understandable within the first screen.
5. **Senior signal** — emphasize design decisions, constraints, reliability, safety, performance, observability, testing, and trade-offs where supported by evidence.
6. **Runnable beats aspirational** — installation and usage instructions must match the current repository.
7. **Progressive disclosure** — concise overview first; detailed architecture and implementation sections later.
8. **Avoid technology walls** — mention technologies in context rather than listing every dependency as a badge.
9. **Respect project maturity** — clearly distinguish stable functionality, experimental functionality, and planned work.
10. **Keep the README maintainable** — prefer ordinary Markdown, local screenshots/assets, stable links, and examples that can be verified from the repository.

## Required workflow

### 1. Inspect before editing

Review, when available:

- repository metadata and description
- current README
- repository tree
- dependency manifests
- application entry points
- major modules/services
- database/schema definitions
- tests and test configuration
- CI/CD workflows
- Docker/compose/deployment configuration
- screenshots/demo assets
- recent commits when useful for maturity/context

Do not rewrite a README based only on repository metadata.

### 2. Establish the factual project model

Determine:

- problem being solved
- intended users
- primary capabilities
- runtime/deployment model
- major architectural components
- important data/control flows
- external dependencies
- security/privacy boundaries
- operational constraints
- testing/verification evidence
- current maturity and known limitations

Mark anything not established by repository evidence as unknown rather than guessing.

### 3. Recommended README structure

Use only sections that are useful for the specific repository. A strong default is:

```text
# Project Name

One-sentence value proposition.

Short explanation of what makes the project technically interesting.

## Why

The problem and design motivation.

## Features

Only implemented, verifiable capabilities.

## Architecture

System diagram when useful, followed by concise component/boundary explanations.

## How it works

Important data/control flows.

## Requirements

Actual supported runtime/tool versions.

## Quick start

Minimal reproducible setup.

## Usage

Representative commands/examples.

## Configuration

Important environment variables/settings.

## Testing

Actual test commands and what they cover.

## Design decisions / Trade-offs

Only decisions supported by the implementation or project documentation.

## Limitations

Known constraints, incomplete areas, or experimental components.

## Roadmap

Only if there is a meaningful project roadmap.

## License

Actual repository license, if present.
```

### 4. Senior-engineer quality checks

Before finalizing, verify:

- Every technical claim is supported by repository evidence.
- Commands and paths actually exist.
- Dependency versions are consistent with manifests.
- Architecture descriptions match the implementation.
- No stale technology names remain after migrations.
- No TODO/planned feature is presented as implemented.
- Security/privacy statements are precise and scoped.
- Performance claims have measurements or are removed.
- Screenshots describe the current UI.
- The README explains meaningful engineering trade-offs.
- The first ~30 seconds of reading explains why the project matters.

## What to avoid

- Generic phrases such as "revolutionary", "blazing fast", "enterprise-grade", or "production-ready" without evidence.
- Huge icon/badge walls.
- Duplicate feature lists.
- Long framework inventories.
- Unverified benchmark numbers.
- Marketing claims that exceed the code.
- Installation steps that depend on undocumented local state.
- Dead links, placeholder URLs, and copied usernames.
- Excessive emoji.
- Hiding important limitations.

## Editing policy

When improving an existing README:

1. Preserve accurate project-specific information.
2. Remove obsolete or contradicted information.
3. Prefer restructuring over adding length.
4. Do not change source code merely to make README claims true unless explicitly asked.
5. If a README needs evidence that the repository does not contain, document the gap rather than inventing it.
6. Keep the final README concise enough that a reviewer can understand the project quickly.

## Portfolio mode

For repositories intended to represent a senior software engineer, optimize for:

- clear problem framing
- architecture and boundaries
- meaningful implementation details
- explicit trade-offs
- reliability and failure behavior
- security/privacy model where relevant
- testing strategy
- reproducibility
- evidence of engineering depth

Do not optimize for keyword density. The goal is to make a technically capable reviewer want to inspect the code.
