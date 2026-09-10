# AI Agent Skills Implementation Guide

A universal guide for implementing and managing AI agent skills across 7 major coding agents. Works with OpenCode, Claude Code, Cursor, Codex, Windsurf, GitHub Copilot, and Gemini CLI.

## What This Is

This guide covers how to install, configure, and manage a comprehensive skill library (22+ skills) following the [Agent Skills standard](https://agentskills.io). It is designed to be read by any AI coding agent: the agent detects which tool it is, then follows the correct paths and commands for that agent.

## Who This Is For

- Developers using AI coding agents who want to expand their agent's capabilities with specialized skills
- Teams standardizing on a shared skill library across multiple agents
- Anyone building custom skills who wants cross-agent compatibility

## What's Inside

| Section | What It Covers |
|---------|---------------|
| Agent Detection | Self-identifying which agent is reading the guide |
| Supported Agents | Directory paths, instruction files, and SKILL.md support per agent |
| Agent Skills Standard | The portable YAML frontmatter + markdown body format |
| Skills Installed | 22+ skills organized by category (design, security, architecture, testing, DevOps, etc.) |
| Installation | Agent-specific install commands (OpenCode, Claude Code, Cursor, Codex, Windsurf, Copilot, Gemini) |
| Directory Structure | Where skills live on disk per agent |
| Cross-Tool Compatibility | Which frontmatter fields work across agents |
| Avoiding AI Writing Tells | Rules for writing human-sounding skill content (banned words, structural rules, self-review checklist) |
| Contributing | How to create your own custom skills |
| Resources | Links to specs, docs, and skill sources |

## Skills Included

22+ skills across 9 categories:

- **Design & UI/UX**: checklist-design, design-review
- **Code Quality & Security**: code-reviewer, security-reviewer, best-practices, fullstack-guardian
- **Development Workflow**: feature-forge, executing-plans, brainstorming, evaluation
- **Architecture & Design**: architecture-designer, api-designer
- **Testing & Quality**: test-master, debugging-wizard
- **Infrastructure & DevOps**: devops-engineer, database-optimizer, chaos-engineer
- **Language-Specific**: react-expert, typescript-pro
- **Content & Marketing**: copywriting, copy-editing
- **CLI & Tools**: cli-developer

## Quick Start

1. Open `AI_AGENT_SKILLS_IMPLEMENTATION.md`
2. Follow the Agent Detection section to identify your agent
3. Run the installation commands for your agent
4. Skills are now available across all your projects

## Universal Fallback

If you use multiple agents or aren't sure which one, install skills to `.agents/skills/` at your project root. Nearly every compatible agent reads from that directory.

## Contributing

See the Contributing section in the guide for how to create custom skills using the Agent Skills standard.

## License

MIT
