# Claude Code Config - agents, skills, commands, etc.

My custom agents, skills, commands, configuration etc. for Claude Code.

## Usage

### Agent Definitions

Agent definitions are Markdown files with YAML frontmatter that define custom subagents for Claude Code.

#### Prerequisites

Before using agents from this repository:

- **GitHub MCP Server**: Some agents include GitHub MCP tools (prefixed with `mcp__github__`) and assume the [GitHub MCP server](https://github.com/github/github-mcp-server) is configured in Claude Code.
- **GitHub CLI**: Some agents may invoke the `gh` command-line utility for GitHub operations. Install it from [cli.github.com](https://cli.github.com/).
- **Review before use**: Agent files should be reviewed before installing to ensure they are suitable for your specific workflow and environment. Check the `tools` list and system prompt to understand what each agent can do.

#### Installation

Agents can be installed at two levels:

##### Global (all projects)

Copy agent files to your global Claude configuration directory:

- **macOS/Linux**: `~/.claude/agents/`
- **Windows**: `%USERPROFILE%\.claude\agents\`

```bash
# Example: Install code-consistency-reviewer globally
cp agents/code-consistency-reviewer.md ~/.claude/agents/
```

Agents installed globally are available in all projects.

##### Project-Level

Copy agent files to your project's `.claude/agents/` directory:

```bash
# From your project root
mkdir -p .claude/agents
cp /path/to/claude-code-config/agents/code-consistency-reviewer.md .claude/agents/
```

Project-level agents are only available within that specific project and can override global agents with the same name.

#### Using Agents

Once installed, agents are automatically available to Claude Code. They appear in the Task tool's available agent types and can be invoked when their trigger conditions are met (as defined in the agent's `description` field).

