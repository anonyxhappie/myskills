# idea-to-kickstarter

## Installation

Install it into each agent through its native mechanism.

### Agent-Specific Paths

| Agent | Installation Path | Reference |
|-------|------------------|-----------|
| **Claude Code** | `~/.claude/skills/idea-to-kickstarter/SKILL.md` | Direct skill file |
| **Cursor** | `.cursor/rules/idea-to-kickstarter.mdc` | MDC rule format |
| **Codex** | `.agent/skills/idea-to-kickstarter/SKILL.md` | In `AGENTS.md` |
| **Copilot** | `.github/copilot-instructions.md` | References methodology |
| **Gemini** | Tool-specific instruction file | References it |

**Note**: The actual methodology remains identical across all agents.

---

## Usage

Once installed, the experience becomes very simple.

Start a new repo.

Tell the agent:

```
Use the idea-to-kickstarter skill.

Here is my raw idea:

[idea]

Do not write code yet.

Start with:
1. product clarification
2. assumptions
3. adversarial questions
4. failure modes
5. open decisions

Do not create the architecture until we resolve the important contradictions.
```

After the brainstorming:

```
Now create Architecture v1 from the decisions we reached.
```

Then:

```
Create two alternative architectures and compare them.
```

Then:

```
Synthesize the best version into Architecture v2.
Run a consistency audit.
```

Then:

```
Generate the implementation roadmap from Architecture v2.
```

Then:

```
Generate the UI/UX specification from the architecture and roadmap.
```

Then:

```
Create the coding-agent handoff package.
```

The **skill remains stable** while the project documents evolve.