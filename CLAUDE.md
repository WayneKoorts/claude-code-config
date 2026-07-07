# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This repository stores custom Claude Code configuration including agents, commands, and settings. It is intended as a personal configuration store, not a build-able project.

## Structure

- `agents/` - Custom agent definitions in Markdown format with YAML frontmatter
  - Only `name` and `description` are required; `tools`, `model`, and `color` are optional
  - Agent body contains the system prompt/instructions

## Agent Definition Format

```markdown
---
name: agent-name
description: When to use this agent (include examples)
tools: Comma-separated list of allowed tools (omit to inherit all tools)
model: sonnet | opus | haiku | fable | inherit | a full model ID (defaults to inherit)
color: purple | blue | green | etc.
---

System prompt content here...
```

Additional optional frontmatter fields are also supported (`disallowedTools`, `permissionMode`, `skills`, `mcpServers`, `hooks`, `memory`, `background`, `effort`, `isolation`, `initialPrompt`) — see the [subagents documentation](https://code.claude.com/docs/en/sub-agents#supported-frontmatter-fields) for the full list.

## Conventions

- Agent files use kebab-case naming: `my-custom-agent.md`
- Descriptions should include usage examples in the format shown in existing agents
- Keep agent prompts focused and specific to their review/task domain
- When creating or editing agent files, use YAML literal block scalar syntax (`|`) for multiline `description` fields instead of escaped `\n` characters
