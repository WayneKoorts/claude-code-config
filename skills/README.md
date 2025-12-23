# Skills

This directory contains reusable Claude Code skills that can be copied to either a project-level or user-level skills directory. For more information on skills, see the [Claude Skills documentation](https://docs.anthropic.com/en/docs/claude-code/skills).

## Installation

Copy any skill folder to one of these locations:

- **Project-level**: `.claude/skills/` in your project root
- **User-level**: `~/.claude/skills/` (applies to all projects)

Each skill folder contains a `SKILL.md` file that defines the skill's name, description, and instructions.

## Available Skills

| Skill | Description |
|-------|-------------|
| `mdl2-icon-picker` | Helps select appropriate Segoe MDL2 Assets icons for WinUI Windows applications. Provides icon recommendations with Unicode points, visual descriptions, and creative alternatives based on use case. The skill generation included a visual identification of the glyphs, so it understands what the glyphs fully look like, not just how they're described by Microsoft.|
| `word-template-generator` | Generates Word documents (.docx) using direct OOXML manipulation. Creates resumes, invoices, letters, reports, proposals, and other documents with full control over formatting and structure. This skill was generated with a full reference of Word's .DOCX file format.|
