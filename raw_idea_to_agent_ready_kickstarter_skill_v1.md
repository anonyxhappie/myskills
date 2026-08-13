# Raw Idea → Agent-Ready Product Kickstart Skill

## Purpose

Transform an unstructured product idea into a small, coherent set of implementation-ready documents that can be handed to coding agents with minimal hidden context.

This skill is a **reasoning and specification workflow**, not a template-filling exercise.

The process should:

```text
raw idea
→ clarify the product
→ challenge assumptions
→ identify contradictions
→ define principles and boundaries
→ model the system
→ compare competing approaches
→ synthesize a canonical architecture
→ derive implementation phases
→ derive UI/UX
→ define testing/security/quality gates
→ produce an agent handoff package
```

The goal is not to produce the most documents.

The goal is to produce the **smallest set of mutually consistent documents that preserve the important decisions and let another agent build without guessing**.

---

# 1. When to Use This Skill

Use this workflow when the user has:

- a raw product concept;
- rough notes;
- a chat brainstorm;
- multiple competing drafts;
- an early technical idea;
- a product concept that needs to become buildable;
- one or more documents that need to be reconciled;
- a prototype idea that needs a proper engineering foundation.

Typical requests:

```text
"Here is my idea. Grill it."
"Challenge this."
"Turn this into architecture."
"Compare these designs."
"Make the best of all these documents."
"Create implementation phases."
"Create a UI/UX spec."
"Prepare this for a coding agent."
"Create a reusable process for doing this."
```

---

# 2. Operating Mode

## 2.1 Be adversarial, not agreeable

Do not optimize for making the idea sound impressive.

Optimize for:

```text
clarity
correctness
consistency
testability
buildability
```

A strong response may conclude:

```text
this assumption is weak
this feature is premature
this boundary is missing
this architecture contradicts itself
this metric is not meaningful
this feature should be deferred
```

## 2.2 Separate four kinds of statements

Every important conclusion should be mentally classified as:

```text
FACT
ASSUMPTION
DESIGN DECISION
OPEN QUESTION
```

Never let an assumption silently become a fact.

## 2.3 Convert principles into invariants

Weak:

> "The system should be secure."

Strong:

```text
Sensitive records cannot appear in logs.
All authoritative values have provenance.
A lower-trust subsystem cannot override a higher-trust fact.
```

The architecture becomes reliable when important ideas are expressed as rules that can be implemented and tested.

## 2.4 Prefer explicit boundaries

For every subsystem, define:

```text
What it owns
What it can change
What it can read
What it cannot change
What it may claim
What it must abstain from claiming
```

## 2.5 Prefer deterministic mechanisms where consequences are high

When a decision affects:

```text
money
identity
security
permissions
state transitions
data integrity
```

prefer deterministic rules where practical.

Probabilistic systems should generally be used for:

```text
suggestion
ranking
classification
summarization
candidate generation
explanation
```

unless the domain clearly justifies more automation.

---

# 3. The Overall Workflow

Use this sequence.

```text
A. Capture the raw idea
B. Clarify the actual product claim
C. Grill the idea
D. Identify assumptions and failure modes
E. Define product boundaries
F. Establish core principles/invariants
G. Model data and system responsibilities
H. Draft one or more architectures
I. Compare alternatives
J. Synthesize a canonical architecture
K. Derive implementation phases
L. Derive UI/UX from the architecture
M. Define testing/security/quality gates
N. Build the agent handoff package
O. Run a final consistency audit
```

Do not jump straight from A to K.

---

# 4. Phase A — Capture the Raw Idea

Extract the idea without prematurely improving it.

Record:

```text
Problem
User
Desired outcome
Inputs
Outputs
Key features
Differentiator
Constraints
Known technologies
Known unknowns
```

Also preserve the user's terminology.

Do not silently rewrite the concept into a different product.

---

# 5. Phase B — Clarify the Actual Product Claim

Translate the raw idea into one precise statement:

```text
For [user],
this product helps them [outcome]
by [mechanism],
using [important inputs],
while respecting [critical constraints].
```

Then answer:

### What is the product?

Not:

> "An AI platform."

But something like:

> "A desktop application that transforms X into Y under Z constraints."

### What is it not?

Write explicit non-goals.

This becomes important later when feature creep begins.

---

# 6. Phase C — Adversarial Grilling

Attack the idea before designing it.

## 6.1 Assumption audit

Ask:

```text
What are we assuming?
Which assumptions are unverified?
Which assumption would break the product if false?
```

## 6.2 Failure-mode questions

Ask:

```text
What if the input is incomplete?
What if the input is contradictory?
What if the model is wrong?
What if the user is wrong?
What if two sources disagree?
What if the system cannot determine the truth?
What if the user expects something the system cannot prove?
```

## 6.3 Worst-case questions

For every high-impact automated action:

```text
What is the worst false positive?
What is the worst false negative?
Which one is more harmful?
What should the system do when uncertain?
```

## 6.4 Abuse/misuse questions

Ask:

```text
How can this feature be misused?
How can a malicious input exploit it?
How can an accidental workflow corrupt state?
What happens when a user misunderstands the UI?
```

## 6.5 Complexity questions

Ask:

```text
What can be removed?
What can be deferred?
What is genuinely required for v1?
Which feature introduces the most architectural risk?
```

The output of grilling should be a list of:

```text
assumptions
risks
contradictions
required decisions
deferred decisions
```

---

# 7. Phase D — Define Product Boundaries

Define explicit boundaries for:

```text
source/input boundary
data boundary
automation boundary
AI boundary
security boundary
user-control boundary
external-system boundary
```

For AI specifically:

```text
AI may:
- suggest
- classify
- summarize
- rank
- explain
- generate candidates

AI may not:
- silently redefine authoritative state
- bypass required validation
- invent unsupported facts
- override deterministic constraints
```

Adjust these rules to the actual domain rather than applying them blindly.

---

# 8. Phase E — Define Core Principles and Invariants

Create 5–15 non-negotiable rules.

Good invariant format:

```text
If X is true,
then Y must always be true.

If X is false,
the system must abstain / block / downgrade / require confirmation.
```

Examples:

```text
Every authoritative value has provenance.
Every destructive action creates history.
A failed validation cannot produce an authoritative result.
A user confirmation does not rewrite source data.
A low-trust suggestion cannot silently become a high-trust fact.
```

For each invariant, define:

```text
implementation mechanism
test
UI implication
failure behavior
```

---

# 9. Phase F — Model the System

Create a layered conceptual model before choosing frameworks.

## 9.1 Input layer

```text
sources
files
events
user input
external systems
```

## 9.2 Evidence / raw data layer

```text
immutable inputs
normalized raw facts
provenance
timestamps
source references
```

## 9.3 Validation / verification layer

```text
validation
reconciliation
consistency checks
quality gates
exceptions
certificates where appropriate
```

## 9.4 Canonical domain layer

```text
entities
records
relationships
state
revisions
```

## 9.5 Interpretation layer

```text
classification
rules
recommendations
semantic analysis
AI suggestions
```

## 9.6 Presentation layer

```text
dashboard
workflows
search
reports
AI assistant
exports
```

The purpose is to prevent analytics/UI concepts from becoming accidental sources of truth.

---

# 10. Data-Model Reasoning

Before writing SQL or code, identify:

```text
entities
attributes
relationships
lifecycle
immutability
revision
ownership
provenance
```

For every table or object ask:

```text
Is this source data?
Is this verified data?
Is this canonical state?
Is this derived state?
Can it be overwritten?
What proves it?
```

## Schema consistency audit

Check:

```text
duplicate table definitions
invalid indexes
missing foreign keys
ambiguous ownership
polymorphic references
inconsistent relationship directions
missing uniqueness constraints
missing lifecycle state
missing revision semantics
```

Do not trust prose claims such as:

> "FK integrity is enforced"

until the actual schema supports them.

---

# 11. State-Machine Design

Do not let implementation agents invent status strings independently.

Define canonical state models for:

```text
record lifecycle
verification
review
resolution
coverage
publication
revision
```

Separate:

```text
state
tier
action
confidence
lifecycle
```

These are often different concepts.

For example:

```text
PROBABLE_MATCH
```

is not the same thing as:

```text
USER_CONFIRMED_EXISTING
```

and neither is the same thing as:

```text
ENTITY_ACTIVE
```

---

# 12. Architecture Drafting

Produce an architecture document with at least:

## 12.1 Product definition

```text
What it is
What it is not
Who it serves
```

## 12.2 Non-negotiable invariants

The rules established earlier.

## 12.3 System flow

```text
input
→ processing
→ validation
→ canonical state
→ interpretation
→ presentation
```

## 12.4 Trust hierarchy

What can be trusted at each layer.

## 12.5 Domain model

The canonical concepts.

## 12.6 Data model

Actual storage model and relationships.

## 12.7 Integration model

External services, local services, APIs.

## 12.8 Security model

Threats, boundaries, secrets, encryption, local processing.

## 12.9 Testing model

Golden cases, negative cases, mutation cases, regressions.

## 12.10 Implementation order

The dependency-aware sequence in which the system should be built.

---

# 13. Compare Competing Documents

When multiple drafts exist, treat them as evidence, not as authorities.

Use a comparison matrix:

| Dimension | Draft A | Draft B | Draft C |
|---|---:|---:|---:|
| Product clarity | | | |
| Core principles | | | |
| Trust model | | | |
| Data model | | | |
| Validation | | | |
| Security | | | |
| Testing | | | |
| Implementation readiness | | | |
| Agent safety | | | |
| UX implications | | | |

Score only to aid comparison.

Do not let the score replace reasoning.

---

# 14. How to Decide Between Drafts

Prefer the draft that:

1. protects important invariants;
2. has fewer internal contradictions;
3. has clearer domain boundaries;
4. makes important assumptions explicit;
5. is easier to test;
6. is safer to automate;
7. is more reversible when wrong;
8. creates less hidden coupling.

Preserve useful material from weaker drafts if it improves completeness without violating the winning architecture.

---

# 15. Synthesis Protocol

Do not concatenate the documents.

Build a new canonical version.

The synthesis process is:

```text
collect strengths
→ identify contradictions
→ choose principle per contradiction
→ correct concrete defects
→ normalize terminology
→ normalize states
→ normalize schema
→ define final boundaries
→ write canonical document
```

## Mandatory post-synthesis audit

### Architecture

```text
Do all sections use the same concepts?
Do all states mean the same thing?
Do all examples match the chosen architecture?
```

### Schema

```text
Do tables match prose?
Are indexes valid?
Are FKs real?
Are relationships directional and consistent?
```

### Trust

```text
Can derived data become source data?
Can lower-trust components override higher-trust state?
Can partial data look authoritative?
```

### AI

```text
Can AI mutate authoritative state?
Can AI invent facts?
Can AI bypass deterministic rules?
```

### Security

```text
Can the local service be abused?
Can secrets leak through logs?
Are backups/restores safe?
```

---

# 16. Architecture → Implementation Roadmap

The roadmap must be derived from dependencies.

Typical pattern:

```text
Phase 0 — Foundation & contracts
Phase 1 — Input / ingestion
Phase 2 — Core domain processing
Phase 3 — Canonicalization / resolution
Phase 4 — Relationships / workflows
Phase 5 — Intelligence / analytics
Phase 6 — Hardening / distribution
```

Do not assume this exact six-phase structure is mandatory.

Adapt phase count to the product.

The key rule is:

> **Later work consumes earlier trust/contracts; it must not recreate them independently.**

---

# 17. Phase 0 Must Establish Contracts

Before feature code:

```text
domain types
state models
revision model
database
immutability
provenance
validation contracts
coverage where relevant
configuration contracts
security baseline
test harness
integration contracts
```

The exact list depends on the product.

---

# 18. Implementation Task Design

Every engineering task should answer:

```text
What?
Why?
Depends on?
Inputs?
Outputs?
State changes?
Failure behavior?
Tests?
Acceptance criteria?
```

Avoid vague tasks like:

> "Build matching."

Prefer:

```text
Implement deterministic exact matching for identifier X
within namespace Y.

Inputs:
verified evidence IDs

Outputs:
resolution result

Constraints:
no canonical entity may be used as evidence

Tests:
exact match
conflict
missing identifier
wrong namespace
```

---

# 19. Global Phase Gates

Every phase should have explicit exit criteria.

Good gates are measurable:

```text
schema passes
tests pass
false acceptance = 0
determinism holds
migration succeeds
security test passes
coverage semantics hold
```

Avoid gates like:

> "feature works well."

---

# 20. Cumulative Gates

A later phase is valid only if:

```text
phase_N_pass
AND
all_prior_phase_gates_pass
AND
no critical regression
```

This protects earlier invariants from later feature additions.

---

# 21. Testing Strategy

Testing should mirror trust boundaries.

## Golden tests

Expected truth.

## Negative tests

Known cases the system must reject.

## Mutation tests

Deliberately corrupt inputs to test whether validation catches them.

## Determinism tests

Same canonical input/configuration:

```text
→ same output
→ same certificate / hash where applicable
```

## Regression tests

Protect every previously fixed bug.

## Recovery tests

Test:

```text
crash
partial work
restart
migration failure
backup failure
network failure
external dependency unavailable
```

---

# 22. Security Review

For every product, inspect at least:

```text
authentication
authorization
secrets
encryption
data at rest
data in transit
local APIs
uploads
parsing
injection
prompt injection
logging
backups
restore
migration
filesystem access
external integrations
```

Translate the threat model into:

```text
architecture rule
implementation task
test
UI behavior
```

---

# 23. UI/UX Derivation

The UI/UX document must come after the core architecture is stable enough to define:

```text
states
trust
workflow
exceptions
coverage
roles
```

Do not design screens independently of the domain model.

---

# 24. UI/UX Specification Structure

For every major screen define:

```text
Purpose
Primary user
Information shown
Trust state
Coverage state
Actions
System behavior
Evidence/provenance
Loading states
Empty states
Error states
Accessibility
Responsive behavior
Acceptance criteria
```

## Global UI primitives

Define reusable components for:

```text
trust state
verification
coverage
evidence
review
confirmation
errors
loading
empty states
```

---

# 25. UI/UX Trust Rules

The UI should make it impossible or difficult to confuse:

```text
verified
with
complete
```

or:

```text
reviewed
with
resolved
```

or:

```text
resolved
with
confirmed user
```

or:

```text
coverage
with
confidence
```

or:

```text
AI explanation
with
authoritative calculation
```

These distinctions should be expressed consistently in:

```text
badges
copy
tooltips
dialogs
tables
charts
exports
notifications
```

---

# 26. Component Design Rules

Every reusable stateful component should define:

```text
Default
Hover
Active
Focus
Disabled
Loading
Success
Warning
Error
```

Trust-critical components must remain understandable when colors are unavailable.

---

# 27. Accessibility

Target the appropriate accessibility standard for the product.

At minimum:

```text
keyboard navigation
visible focus
semantic labels
screen reader support
sufficient contrast
non-color state communication
dialog focus management
adequate touch targets
```

Define accessibility during component design, not after the UI is finished.

---

# 28. Coding-Agent Handoff

The final handoff should be a small set of canonical documents.

Recommended package:

```text
01_PRODUCT_DEFINITION.md
02_ARCHITECTURE.md
03_DATA_MODEL.md
04_IMPLEMENTATION_ROADMAP.md
05_UI_UX_SPEC.md
06_SECURITY.md
07_TEST_STRATEGY.md
08_AGENT_RULES.md
```

Optional:

```text
09_API_CONTRACTS.md
10_DOMAIN_GLOSSARY.md
11_DECISION_LOG.md
```

The package should be internally consistent and versioned.

---

# 29. Agent Context Contract

Before starting a task, a coding agent should be able to answer:

```text
What architectural decision does this implement?
What domain contract does it depend on?
What state does it read/write?
What data is authoritative?
What evidence/provenance is required?
What invariants must not be broken?
What tests prove correctness?
What failure states exist?
```

If the documents do not answer these, the agent should surface:

```text
CONTRACT GAP
```

instead of inventing architecture.

---

# 30. Coding-Agent Guardrails

Agents must never silently:

```text
invent a new domain state
invent a new source of truth
bypass validation
rewrite immutable history
weaken security constraints
turn a candidate into an authoritative fact
make a probabilistic decision automatic
let AI override deterministic constraints
create a new schema relationship without documenting it
change a contract without updating tests and dependent documents
```

---

# 31. Decision Log

Important design decisions should be recorded as:

```text
Decision
Context
Alternatives considered
Why chosen
Trade-offs
Affected documents
Migration impact
```

This prevents future agents from "simplifying away" deliberate safeguards.

---

# 32. Document Consistency Audit

Before finalizing the kickstarter package, run a cross-document audit.

Check:

### Terminology

```text
same term = same meaning everywhere
```

### States

```text
same enum
same transition
same UI meaning
```

### Schema

```text
prose ↔ database
```

### Roadmap

```text
architecture dependency ↔ implementation order
```

### UI

```text
domain states ↔ visual states
```

### Tests

```text
every invariant ↔ at least one proving test
```

### Agent rules

```text
every critical invariant ↔ guardrail
```

---

# 33. Versioning Strategy

Use a canonical version for each document.

Example:

```text
Architecture v1.0
Roadmap v1.0
UI/UX v1.0
```

When a foundational decision changes:

```text
major version
```

When wording/details change without changing architecture:

```text
minor version
```

Do not maintain multiple competing "final" documents.

---

# 34. Final Review Rubric

Rate the resulting package on:

| Dimension | Question |
|---|---|
| Product clarity | Is the product claim precise? |
| Problem fit | Does the architecture solve the real problem? |
| Assumption quality | Were dangerous assumptions challenged? |
| Trust | Can important claims be justified? |
| Data model | Is the domain coherent? |
| Security | Are important threats addressed? |
| Testability | Are invariants provable? |
| Implementation | Can agents execute the roadmap? |
| UX | Can users understand system state? |
| Consistency | Do all documents agree? |
| Evolution | Can the design change safely? |

A high score is not the goal.

The goal is to identify the weakest dimension before implementation starts.

---

# 35. Final Success Condition

The process is complete when:

```text
[ ] The product claim is explicit.
[ ] Non-goals are explicit.
[ ] Assumptions have been challenged.
[ ] Major failure modes are understood.
[ ] Trust boundaries are explicit.
[ ] Domain model exists.
[ ] State models exist.
[ ] Data/provenance model exists.
[ ] Security model exists.
[ ] Testing model exists.
[ ] Canonical architecture exists.
[ ] Implementation roadmap exists.
[ ] UI/UX specification exists.
[ ] Coding-agent guardrails exist.
[ ] All documents are mutually consistent.
[ ] Another coding agent can start without hidden conversation context.
```

---

# 36. The Reusable Method

The whole skill can be remembered as:

```text
IDEA
 ↓
CLARIFY
 ↓
GRILL
 ↓
ASSUMPTIONS
 ↓
FAILURES
 ↓
BOUNDARIES
 ↓
INVARIANTS
 ↓
DOMAIN MODEL
 ↓
ARCHITECTURE
 ↓
COMPARE
 ↓
SYNTHESIZE
 ↓
CONSISTENCY AUDIT
 ↓
ROADMAP
 ↓
UI/UX
 ↓
TEST + SECURITY
 ↓
AGENT RULES
 ↓
HANDOFF
```

The central rule is:

> **Do not turn a raw idea directly into code. Turn it into explicit contracts first, then make every downstream document a faithful consumer of those contracts.**

That is what makes the resulting documents useful to coding agents instead of merely useful to humans reading a design document.
