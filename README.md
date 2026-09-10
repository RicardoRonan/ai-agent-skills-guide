# AI Agent Skills Implementation Guide

A universal guide for implementing and managing AI agent skills across 7 major coding agents. Works with OpenCode, Claude Code, Cursor, Codex, Windsurf, GitHub Copilot, and Gemini CLI.

## What This Is

This guide covers how to install, configure, and manage a skill library following the [Agent Skills standard](https://agentskills.io). It is written to be read by any AI coding agent: the agent detects which tool it is, then follows the correct paths and commands for that agent.

The library ships with 90+ curated skills drawn from a 322+ skill collection, organized into role-based packages so you install what fits your work instead of everything.

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
| Skills Catalog | 90+ skills organized by category with role package tags |
| Installation | Role-based install scripts (OpenCode, Claude Code, Cursor, Codex, Windsurf, Copilot, Gemini) |
| Directory Structure | Where skills live on disk per agent |
| Cross-Tool Compatibility | Which frontmatter fields work across agents |
| Avoiding AI Writing Tells | Rules for writing human-sounding skill content |
| Contributing | How to create your own custom skills |
| Resources | Links to specs, docs, and skill sources |

## Role-Based Packages

Pick the role that matches your work. Each installs a curated set of skills.

| Role | Skills | Best For |
|------|--------|----------|
| `fullstack` | 18 | Most developers (frontend + backend + tools) |
| `frontend` | 15 | UI/UX development, React, Vue, Angular |
| `backend` | 14 | API development, servers, databases |
| `devops` | 12 | Infrastructure, CI/CD, monitoring, SRE |
| `mobile` | 10 | iOS, Android, Flutter, React Native |
| `data` | 10 | Data engineering, ML, analytics |
| `security` | 8 | Application security, penetration testing |
| `architect` | 10 | System design, tech leads |
| `content` | 6 | Copywriting, SEO, marketing |

Add individual skills on top of any role with the `$extras` array. No long lists to delete through.

## Skills Catalog

90+ skills across these categories:

- **Design & UI/UX**: checklist-design, design-review, shadcn-ui, color-expert, and more
- **Code Quality & Security**: code-reviewer, security-reviewer, best-practices, fullstack-guardian
- **Development Workflow**: feature-forge, executing-plans, brainstorming, evaluation
- **Architecture & Design**: architecture-designer, api-designer, microservices-architect
- **Testing & Quality**: test-master, debugging-wizard, playwright-expert
- **Infrastructure & DevOps**: devops-engineer, kubernetes-specialist, terraform-engineer, sre-engineer
- **Language & Frameworks**: 26 skills covering Python, JavaScript, Vue, Angular, Go, Rust, Java, PHP, C#, Swift, and more
- **Content & Marketing**: copywriting, copy-editing, seo, cold-email
- **AI & Machine Learning**: fine-tuning-expert, ml-pipeline, rag-architect
- **Data & Visualization**: d3-visualization, data-report, pandas-pro
- **Game Development**: game-developer

The full catalog with purposes and package tags is in the guide.

## Quick Start

1. Open `AI_AGENT_SKILLS_IMPLEMENTATION.md`
2. Follow the Agent Detection section to identify your agent
3. Pick your role and run the install script for your agent
4. Skills are now available across all your projects

## Universal Fallback

If you use multiple agents or aren't sure which one, install skills to `.agents/skills/` at your project root. Nearly every compatible agent reads from that directory.

## Contributing

See the Contributing section in the guide for how to create custom skills using the Agent Skills standard.

## License

MIT
