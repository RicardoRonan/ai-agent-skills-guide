# AI Agent Skills Implementation Guide

A universal guide for implementing and managing AI agent skills across 7 major coding agents. Works with OpenCode, Claude Code, Cursor, Codex, Windsurf, GitHub Copilot, and Gemini CLI.

## What This Is

This guide covers how to install, configure, and manage a skill library following the [Agent Skills standard](https://agentskills.io). It is written to be read by any AI coding agent: the agent detects which tool it is, then follows the correct paths and commands for that agent.

The library ships with 114 curated skills drawn from a 322+ skill collection plus a context-engineering kit, organized into role-based packages so you install what fits your work instead of everything.

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
| Skills Catalog | 114 skills organized by category with role package tags |
| Installation | Role-based install scripts (OpenCode, Claude Code, Cursor, Codex, Windsurf, Copilot, Gemini) |
| Directory Structure | Where skills live on disk per agent |
| Cross-Tool Compatibility | Which frontmatter fields work across agents |
| Avoiding AI Writing Tells | Rules for writing human-sounding skill content |
| Keeping the Catalog Updated | Re-run procedure that detects and adds new upstream skills |
| Contributing | How to create your own custom skills |
| Resources | Links to specs, docs, and skill sources |

## Role-Based Packages

Pick the role that matches your work. Each installs a curated set of skills.

| Role | Skills | Best For |
|------|--------|----------|
| `fullstack` | 24 | Most developers (frontend + backend + tools) |
| `frontend` | 20 | UI/UX development, React, Vue, Angular |
| `backend` | 19 | API development, servers, databases |
| `devops` | 17 | Infrastructure, CI/CD, monitoring, SRE |
| `mobile` | 16 | iOS, Android, Flutter, React Native |
| `data` | 14 | Data engineering, ML, analytics |
| `security` | 13 | Application security, penetration testing |
| `architect` | 15 | System design, tech leads |
| `content` | 11 | Copywriting, SEO, marketing |
| `optimize` | 16 | Token cost and context window efficiency |

Add individual skills on top of any role with the `$extras` array. No long lists to delete through.

## Skills Catalog

114 skills across 13 categories. Expand any category to see each skill, its purpose, and the role packages that include it. `all` means the skill is part of every role package.

<details>
<summary><strong>Design & UI/UX</strong> (17 skills)</summary>

| Skill | Purpose | Packages |
|-------|---------|----------|
| `checklist-design` | 129 UI/UX checklists for web, mobile, design systems | frontend |
| `design-review` | Visual audit with before/after screenshots | fullstack, frontend |
| `apple-hig` | Apple Human Interface Guidelines | frontend |
| `brutalist-skill` | Brutalist design patterns | frontend |
| `canvas-design` | Canvas-based design | frontend |
| `color-expert` | Color theory and palette generation | frontend |
| `design-brief` | Design brief creation | frontend |
| `design-consultation` | Design consultation workflows | frontend |
| `design-shotgun` | Design exploration and ideation | frontend |
| `frontend-design` | Frontend design patterns and best practices | frontend |
| `hand-drawn-diagrams` | Hand-drawn diagram generation | frontend |
| `image-to-code-skill` | Convert visual designs to code | frontend |
| `minimalist-skill` | Minimalist design principles | frontend |
| `platform-design` | Platform-specific design guidelines | frontend |
| `shadcn-ui` | shadcn/ui component patterns | frontend |
| `ui-ux-pro-max` | Advanced UI/UX workflows | frontend |
| `web-design-guidelines` | Web design standards and patterns | frontend |

</details>

<details>
<summary><strong>Code Quality & Security</strong> (7 skills)</summary>

| Skill | Purpose | Packages |
|-------|---------|----------|
| `code-reviewer` | PR reviews, security vulnerabilities, code smells | all |
| `security-reviewer` | SAST, penetration testing, vulnerability scanning | fullstack, backend, security, architect |
| `best-practices` | CSP, SRI, Trusted Types, browser compatibility | fullstack, frontend, backend |
| `fullstack-guardian` | Security-focused full-stack implementation | fullstack, backend, security |
| `code-documenter` | Documentation generation and standards | fullstack, backend |
| `prompt-engineer` | AI prompt engineering patterns | data, fullstack |
| `secure-code-guardian` | Secure coding patterns and review | security |

</details>

<details>
<summary><strong>Development Workflow</strong> (13 skills)</summary>

| Skill | Purpose | Packages |
|-------|---------|----------|
| `feature-forge` | Requirements workshops, user stories, EARS specs | all |
| `executing-plans` | Step-by-step plan execution | fullstack, backend, architect |
| `brainstorming` | Idea generation and exploration | fullstack, frontend, mobile |
| `evaluation` | Solution assessment and comparison | fullstack, backend, architect, data |
| `finishing-a-development-branch` | Branch completion and merge workflows | fullstack, backend |
| `onboarding` | Project onboarding for new contributors | fullstack, backend |
| `pr-feedback-quality-gate` | PR feedback standards and quality checks | fullstack, backend, architect |
| `receiving-code-review` | How to receive and apply review feedback | fullstack, backend |
| `requesting-code-review` | How to request effective reviews | fullstack, backend |
| `systematic-debugging` | Debugging methodology and process | fullstack, backend, mobile |
| `test-driven-development` | TDD workflows and patterns | fullstack, backend |
| `using-git-worktrees` | Git worktree patterns for parallel work | fullstack, backend |
| `verification-before-completion` | Pre-ship verification checklists | all |

</details>

<details>
<summary><strong>Architecture & Design</strong> (6 skills)</summary>

| Skill | Purpose | Packages |
|-------|---------|----------|
| `architecture-designer` | System design, ADRs, scalability planning | fullstack, backend, architect |
| `api-designer` | REST/GraphQL APIs, OpenAPI specs | fullstack, backend, architect |
| `cloud-architect` | Cloud infrastructure design and planning | devops, architect |
| `graphql-architect` | GraphQL schema design and federation | backend, architect |
| `microservices-architect` | Microservice patterns and decomposition | architect |
| `site-architecture` | Site structure and information architecture | frontend, architect |

</details>

<details>
<summary><strong>Testing & Quality</strong> (5 skills)</summary>

| Skill | Purpose | Packages |
|-------|---------|----------|
| `test-master` | Unit, integration, E2E, performance testing | fullstack, backend |
| `debugging-wizard` | Systematic debugging methodology | fullstack, backend, mobile |
| `playwright-expert` | Playwright test patterns and strategies | fullstack, frontend |
| `export-download-debugging` | Export and download flow debugging | fullstack, frontend |
| `verification-before-completion` | Pre-completion verification checks | all |

</details>

<details>
<summary><strong>Infrastructure & DevOps</strong> (12 skills)</summary>

| Skill | Purpose | Packages |
|-------|---------|----------|
| `devops-engineer` | CI/CD, Docker, Kubernetes, Terraform | fullstack, backend, devops |
| `database-optimizer` | Query optimization, index design | fullstack, backend, devops |
| `chaos-engineer` | Resilience testing, failure injection | devops, security |
| `kubernetes-specialist` | Kubernetes deep dive and operations | devops |
| `monitoring-expert` | Observability, alerting, dashboards | devops |
| `postgres-pro` | PostgreSQL advanced patterns | backend, devops |
| `redis-core` | Redis patterns and data structures | backend, devops |
| `redis-query-engine` | Redis query optimization | backend, devops |
| `sre-engineer` | Site reliability engineering | devops |
| `spark-engineer` | Apache Spark data processing | data, devops |
| `sql-pro` | SQL optimization and advanced queries | backend, devops, data |
| `terraform-engineer` | Terraform infrastructure as code | devops |

</details>

<details>
<summary><strong>Language & Frameworks</strong> (26 skills)</summary>

| Skill | Purpose | Packages |
|-------|---------|----------|
| `react-expert` | React 19, Server Components, hooks | fullstack, frontend |
| `typescript-pro` | Advanced types, type guards, tRPC | fullstack, frontend, backend |
| `vue-expert` | Vue.js 3, Composition API, Nuxt | frontend |
| `angular-architect` | Angular patterns and architecture | frontend |
| `nextjs-developer` | Next.js App Router, Server Components | frontend |
| `nestjs-expert` | NestJS patterns and architecture | backend |
| `python-pro` | Python patterns, asyncio, packaging | data, backend |
| `javascript-pro` | Modern JavaScript patterns | fullstack, frontend |
| `golang-pro` | Go concurrency, patterns, stdlib | backend |
| `rust-engineer` | Rust ownership, async, systems programming | backend |
| `java-architect` | Java patterns, Spring ecosystem | backend |
| `kotlin-specialist` | Kotlin coroutines, Android, patterns | mobile, backend |
| `swift-expert` | Swift, SwiftUI, iOS patterns | mobile |
| `php-pro` | PHP patterns, modern PHP 8+ | backend |
| `csharp-developer` | C#/.NET patterns and best practices | backend |
| `cpp-pro` | C++ modern patterns, performance | backend |
| `flutter-expert` | Flutter/Dart app patterns | mobile |
| `rails-expert` | Ruby on Rails patterns and conventions | backend |
| `laravel-specialist` | Laravel patterns and best practices | backend |
| `spring-boot-engineer` | Spring Boot patterns and configuration | backend |
| `dotnet-core-expert` | .NET Core patterns and middleware | backend |
| `django-expert` | Django patterns, ORM, views | backend |
| `fastapi-expert` | FastAPI patterns, async, validation | backend |
| `react-native-expert` | React Native patterns and debugging | mobile |
| `wordpress-pro` | WordPress plugin and theme development | backend |
| `shopify-expert` | Shopify Liquid, Storefront API | backend |

</details>

<details>
<summary><strong>Content & Marketing</strong> (5 skills)</summary>

| Skill | Purpose | Packages |
|-------|---------|----------|
| `copywriting` | Marketing copy, landing pages, CTAs | content |
| `copy-editing` | Polish and refine existing copy | content |
| `cold-email` | Cold email writing and sequences | content |
| `emails` | Email copywriting and automation | content |
| `seo` | SEO optimization and strategy | content |

</details>

<details>
<summary><strong>AI & Machine Learning</strong> (3 skills)</summary>

| Skill | Purpose | Packages |
|-------|---------|----------|
| `fine-tuning-expert` | Model fine-tuning strategies | data |
| `ml-pipeline` | ML pipeline design and orchestration | data |
| `rag-architect` | RAG system design and retrieval | data |

</details>

<details>
<summary><strong>Token Optimization & Context Engineering</strong> (16 skills)</summary>

| Skill | Purpose | Packages |
|-------|---------|----------|
| `context-engineering` | Context components, mechanics, and constraints in agent systems | all |
| `multi-agent-patterns` | Multi-agent architectures for context isolation | all |
| `write-concisely` | Concise writing rules to cut output tokens | all |
| `prompt-engineer` | Prompt design and refactoring for token efficiency | all |
| `launch-sub-agent` | Dispatch an isolated subagent for a task | optimize |
| `do-in-parallel` | Run independent tasks in parallel subagents | optimize |
| `memorize` | Curate insights into CLAUDE.md (agentic memory) | optimize |
| `decay` | Prune stale memory and context | optimize |
| `reset` | Reset context cleanly between tasks | optimize |
| `apply-anthropic-skill-best-practices` | Token-efficient skill authoring | optimize |
| `prompt-engineering` | Advanced prompt patterns for agents, hooks, and skills | optimize |
| `test-prompt` | Test and iterate prompts | optimize |
| `setup-codemap-cli` | Semantic code retrieval to cut file reads | optimize |
| `setup-serena-mcp` | Serena MCP for semantic code retrieval | optimize |
| `output-skill` | Full-output enforcement, handles token-limit splits | optimize |
| `graphify` | Turn a codebase into a queryable knowledge graph | optimize |

</details>

<details>
<summary><strong>Data & Visualization</strong> (3 skills)</summary>

| Skill | Purpose | Packages |
|-------|---------|----------|
| `d3-visualization` | D3.js chart and visualization patterns | data, frontend |
| `data-report` | Data reporting and presentation | data |
| `pandas-pro` | Pandas data analysis patterns | data |

</details>

<details>
<summary><strong>CLI & Tools</strong> (2 skills)</summary>

| Skill | Purpose | Packages |
|-------|---------|----------|
| `cli-developer` | CLI tools, argument parsing, completions | fullstack |
| `mcp-developer` | MCP server development patterns | backend |

</details>

<details>
<summary><strong>Game Development</strong> (1 skill)</summary>

| Skill | Purpose | Packages |
|-------|---------|----------|
| `game-developer` | Game development patterns and engines | (standalone) |

</details>

The source of truth, including the full 322+ skill set and the self-update procedure, is in `AI_AGENT_SKILLS_IMPLEMENTATION.md`.

## Quick Start

1. Open `AI_AGENT_SKILLS_IMPLEMENTATION.md`
2. Follow the Agent Detection section to identify your agent
3. Pick your role and run the install script for your agent
4. Skills are now available across all your projects

## Universal Fallback

If you use multiple agents or aren't sure which one, install skills to `.agents/skills/` at your project root. Nearly every compatible agent reads from that directory.

## Self-Updating Catalog

The guide keeps itself current. The Skills Catalog carries a `Last synced` date, and the "Keeping the Catalog Updated" section holds scripts that:

1. Detect skills added to the upstream repos since that date (via commit history)
2. Detect catalog entries that were removed or renamed upstream
3. Fetch each new skill's description
4. Classify it into a category and role package

Run the guide again after a while and the agent runs these checks before acting, so the catalog never drifts from upstream. The repo currently ships 114 curated skills out of 322+ available.

## Contributing

See the Contributing section in the guide for how to create custom skills using the Agent Skills standard.

## License

MIT
