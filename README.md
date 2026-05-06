Agent Skills for LeviTK workflows.

This repository follows the [Agent Skills specification](https://agentskills.io/specification). Skills are designed for agents that support `SKILL.md` discovery, including Claude Code, Codex CLI, OpenCode, and compatible coding agents.

## Installation

### Marketplace

```text
/plugin marketplace add LeviTK/LeviTK_Skills
/plugin install levitk-skills@LeviTK_Skills
```

### npx skills

```bash
npx skills add git@github.com:LeviTK/LeviTK_Skills.git
```

### Manually

#### Claude Code

Copy the repository contents into `/.claude` at your project root.

#### Codex CLI

Copy the `skills/` directory into `~/.codex/skills`.

#### OpenCode

Clone the full repository into OpenCode's skills directory:

```bash
git clone https://github.com/LeviTK/LeviTK_Skills.git ~/.opencode/skills/LeviTK_Skills
```

Clone the full repository, not only the inner `skills/` directory, so metadata and future shared resources remain available.

## Skills

| Skill | Description |
|-------|-------------|
| [managing-heptabase](skills/managing-heptabase) | Search, read, analyze, and write Heptabase knowledge base content through available Heptabase tools or CLI workflows. |

## Repository layout

```text
LeviTK_Skills/
├── .claude-plugin/
│   ├── marketplace.json
│   └── plugin.json
├── skills/
│   └── managing-heptabase/
│       ├── SKILL.md
│       └── references/
│           └── TOOLING.md
├── LICENSE
└── README.md
```

Each skill lives in `skills/<skill-name>/SKILL.md`. Larger reference material should be placed under `skills/<skill-name>/references/` and linked from the skill file.
