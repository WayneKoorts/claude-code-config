# Claude Code Config - agents, commands, etc.

My custom agents, commands, configuration etc. for Claude Code.

## Usage

### Agent Definitions

Agent definitions are Markdown files with YAML frontmatter that define custom subagents for Claude Code. They can be installed at two levels:

#### Global Configuration (all projects)

Copy agent files to your global Claude configuration directory:

- **macOS/Linux**: `~/.claude/agents/`
- **Windows**: `%USERPROFILE%\.claude\agents\`

```bash
# Example: Install code-consistency-reviewer globally
cp agents/code-consistency-reviewer.md ~/.claude/agents/
```

Agents installed globally are available in all projects.

#### Project-Level Configuration

Copy agent files to your project's `.claude/agents/` directory:

```bash
# From your project root
mkdir -p .claude/agents
cp /path/to/claude-code-config/agents/code-consistency-reviewer.md .claude/agents/
```

Project-level agents are only available within that specific project and can override global agents with the same name.

#### Using Agents

Once installed, agents are automatically available to Claude Code. They appear in the Task tool's available agent types and can be invoked when their trigger conditions are met (as defined in the agent's `description` field).

