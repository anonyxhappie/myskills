# Versioning & Portfolio Evolution

## Purpose

Create explicit, inspectable versions of software projects, websites, documentation, and portfolio experiences without destroying historical work. Treat versions as intentional product states, not arbitrary snapshots.

## Core principles

1. **Never overwrite history unnecessarily.** Preserve meaningful previous versions through Git branches, tags, releases, archived paths, or immutable snapshots.
2. **Version the experience, not just the code.** A major redesign or change in product purpose deserves its own version even when implementation technology is unchanged.
3. **Make the current version obvious.** Users and maintainers should be able to identify what is current, what is archived, and what changed.
4. **Use semantic intent.** Prefer `v1`, `v2`, `v3` for major product states and semantic versions such as `v2.1.0` when software compatibility/release semantics matter.
5. **Separate history from production.** Historical versions should remain accessible without making the primary experience confusing.
6. **Reproducibility matters.** A version should map to a Git ref, commit, tag, release, or otherwise deterministic artifact.
7. **Do not fabricate chronology.** If an exact release date, feature history, or prior state cannot be established from Git evidence, say so.
8. **Version boundaries should be meaningful.** Major versions represent substantial changes in information architecture, product positioning, UX, architecture, or audience.
9. **Avoid version sprawl.** Do not create a new major version for tiny copy, CSS, or bug-fix changes.
10. **Keep upgrade paths explicit.** When appropriate, document what changed, why, and whether the previous version remains supported.

## Required workflow

### 1. Inventory existing history

Inspect:

- branches
- tags/releases
- commit history
- deployment configuration
- existing version directories/routes
- current production entry point
- documentation mentioning versions
- historical assets

Establish the actual version lineage before creating a new one.

### 2. Classify the requested change

Use:

```text
PATCH   = bug/content/cosmetic correction
MINOR   = backward-compatible capability or content expansion
MAJOR   = substantial redesign, repositioning, architecture change, or new primary experience
```

For personal portfolios and websites, a major visual/product repositioning should normally receive a new major version.

### 3. Choose the version boundary

For a GitHub Pages site with historical branches:

```text
master/main     → production/current version
v1              → historical major version
v2              → historical major version
v3              → new major version under development
```

If GitHub Pages is configured to serve a branch, do not change that deployment target merely to create a new version unless explicitly requested.

### 4. Create the version safely

Preferred sequence:

1. Identify the current production ref.
2. Create a new branch from the appropriate baseline.
3. Implement the new version on that branch.
4. Preserve previous version branches/tags.
5. Update documentation to explain the version map.
6. Only merge/promote to production after the new version is reviewed.

### 5. Versioned website architecture

For a portfolio site, prefer a clean major-version model such as:

```text
v1/  historical portfolio
v2/  historical interactive portfolio
v3/  current portfolio experience
```

The exact hosting mechanism can be:

- Git branches for isolated deployed states
- tags/releases for immutable milestones
- subdirectories for multiple versions in one deployment
- a version selector/archive page when multiple versions are intentionally exposed

Choose the least complex mechanism that preserves both history and usability.

## Portfolio-specific rules

A new portfolio major version should be treated as a **curated representation of professional work**, not a dump of every repository.

### Project selection

Rank projects using evidence from:

- implementation depth
- originality
- architectural sophistication
- relevance to target role
- completeness
- visual/demo quality
- documentation quality
- recency

Prefer a small number of strong projects over an exhaustive repository list.

### Project cards

Each showcased project should ideally expose:

```text
name
one-line problem/value proposition
what was built
key engineering ideas
status
repository link
live/demo link when verified
```

Never claim a live demo if the deployment URL is not verified.

### Link integrity

Before publishing:

- verify repository names
- verify repository visibility
- verify default branches where relevant
- verify GitHub URLs
- verify GitHub Pages/demo URLs
- avoid placeholder usernames or URLs
- avoid links to local files
- avoid stale project names

## Portfolio information architecture

A strong default is:

```text
HERO
  ↓
ABOUT / ENGINEERING THESIS
  ↓
SELECTED WORK
  ↓
PROJECT DETAIL / CASE STUDIES
  ↓
EXPERIENCE
  ↓
CAPABILITIES
  ↓
EXPERIMENTS / OTHER WORK
  ↓
GITHUB / CONTACT
```

The homepage should answer within seconds:

1. Who is this?
2. What kind of engineer is this?
3. What has this person actually built?
4. Where can I inspect the work?

## Version metadata

For a versioned website, maintain a lightweight manifest when useful:

```json
{
  "current": "v3",
  "versions": [
    {
      "id": "v1",
      "status": "archived",
      "ref": "v1"
    },
    {
      "id": "v2",
      "status": "archived",
      "ref": "v2"
    },
    {
      "id": "v3",
      "status": "current",
      "ref": "v3"
    }
  ]
}
```

Do not add a manifest solely for decoration; Git itself remains the source of truth.

## Validation checklist

Before declaring a version complete:

- [ ] Previous meaningful versions remain recoverable.
- [ ] New version has a deterministic Git ref.
- [ ] Current version is clearly identifiable.
- [ ] No stale version labels remain in the current experience.
- [ ] All project links point to real repositories.
- [ ] Live/demo links are verified or omitted.
- [ ] Project descriptions are evidence-backed.
- [ ] Historical work is not accidentally presented as current work.
- [ ] Mobile experience is usable when the site is responsive.
- [ ] No local filesystem URLs or placeholder links remain.
- [ ] README/version documentation explains the version map.

## Anti-patterns

Avoid:

- deleting old branches just to simplify naming
- calling every deploy a major version
- mixing old and new portfolio content without labeling
- keeping multiple versions with identical content
- using version numbers as marketing decoration
- presenting aspirational projects as completed work
- linking to guessed demo URLs
- claiming "latest" without a clear current ref
