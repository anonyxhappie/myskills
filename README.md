# myskills

Reusable skills for structured software and product engineering workflows.

## Skills

### idea-to-kickstarter
A generic, adversarial product-design workflow that transforms a raw idea into a validated, implementation-ready package:

**brainstorm → challenge assumptions → define boundaries → design architecture → compare and synthesize → roadmap → UI/UX → testing → security → coding-agent rules → consistency audit**

The separation is intentional:

```text
SKILL
    = HOW TO THINK / WORK

ARCHITECTURE
    = WHAT TO BUILD

ROADMAP
    = IN WHAT ORDER TO BUILD IT

UI/UX
    = HOW THE USER EXPERIENCES IT

SECURITY
    = WHAT MUST NOT GO WRONG

TEST STRATEGY
    = HOW WE KNOW IT WORKS

AGENT RULES
    = WHAT THE CODING AGENT MUST NEVER VIOLATE
```

### readme-polisher
A repository-aware workflow for producing accurate, concise, senior-engineer-quality READMEs. It inspects implementation evidence before making claims and emphasizes architecture, boundaries, trade-offs, reliability, security, testing, reproducibility, and project maturity.

See [`readme-polisher/SKILL.md`](readme-polisher/SKILL.md).

## Design principle

Skills define **reusable ways of working**. They should be applicable across unrelated repositories without silently inventing project-specific facts.
