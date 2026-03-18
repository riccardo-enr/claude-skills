# Claude Code Skills

A collection of custom [Claude Code skills](https://docs.anthropic.com/en/docs/claude-code/skills) for academic research, robotics development, Obsidian knowledge management, and developer productivity.

## Skills

### Research & Writing

| Skill | Description |
|---|---|
| **academic-explainer** | Explains prerequisite topics and background concepts needed to understand a paper or research note. Targets robotics/control/ML audience. |
| **academic-reviewer** | Structured academic review with novelty assessment, technical soundness evaluation, and actionable suggestions. Specializes in sampling-based optimal control, MPPI, and UAV autonomy. |

### Obsidian Integration

| Skill | Description |
|---|---|
| **obsidian-markdown** | Creates and edits Obsidian Flavored Markdown — wikilinks, embeds, callouts, and frontmatter properties. |
| **obsidian-bases** | Creates and edits Obsidian Bases (`.base` files) with filters, formulas, and database-like views. |
| **obsidian-cli** | Interacts with running Obsidian instances via CLI — read/create/search notes, manage plugins, inspect DOM. |
| **json-canvas** | Creates and edits JSON Canvas files (`.canvas`) with text/file/link/group nodes and edges. |

### Developer Tools

| Skill | Description |
|---|---|
| **simplify** | Reviews changed code for unnecessary complexity, duplication, and inefficiency. |
| **explicode-docs** | Adds [Explicode](https://github.com/riccardo/codedoc.nvim)-compatible documentation blocks to code files. |
| **create-issue** | Creates GitHub issues using the `gh` CLI. |
| **defuddle** | Extracts clean markdown from web pages using [Defuddle](https://github.com/nichochar/defuddle-cli), removing clutter to save tokens. |
| **keybindings-help** | Configures Claude Code keyboard shortcuts in `~/.claude/keybindings.json`. |

### Planning

| Skill | Description |
|---|---|
| **impl-plan** | Implementation planner for ROS2, PX4, Python, and C++/CUDA robotics projects. Produces phased plans with architecture diagrams, package layout, and risk registers. |

## Installation

Clone this repository and add it to your Claude Code skills path:

```bash
git clone https://github.com/riccardo-enr/claude-skills.git
```

Then add the path to your Claude Code settings (`~/.claude/settings.json`):

```json
{
  "skills": [
    "/path/to/claude-skills"
  ]
}
```

Each skill is a directory containing a `SKILL.md` file that defines its behavior, with optional `references/` subdirectories for detailed syntax documentation.

## Structure

```
claude-skills/
├── academic-explainer/SKILL.md
├── academic-reviewer/SKILL.md
├── create-issue/SKILL.md
├── defuddle/SKILL.md
├── explicode-docs/SKILL.md
├── impl-plan/SKILL.md
├── json-canvas/
│   ├── SKILL.md
│   └── references/EXAMPLES.md
├── keybindings-help/SKILL.md
├── obsidian-bases/
│   ├── SKILL.md
│   └── references/FUNCTIONS_REFERENCE.md
├── obsidian-cli/SKILL.md
├── obsidian-markdown/
│   ├── SKILL.md
│   └── references/
├── simplify/SKILL.md
└── README.md
```