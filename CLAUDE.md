# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This repository stores custom Claude Code configuration including agents, commands, and settings. It is intended as a personal configuration store, not a build-able project.

## Structure

- `agents/` - Custom agent definitions in Markdown format with YAML frontmatter
  - Agents define `name`, `description`, `tools`, `model`, and `color` in frontmatter
  - Agent body contains the system prompt/instructions

## Agent Definition Format

```markdown
---
name: agent-name
description: When to use this agent (include examples)
tools: Comma-separated list of allowed tools
model: opus | sonnet | haiku
color: purple | blue | green | etc.
---

System prompt content here...
```

## Conventions

- Agent files use kebab-case naming: `my-custom-agent.md`
- Descriptions should include usage examples in the format shown in existing agents
- Keep agent prompts focused and specific to their review/task domain
