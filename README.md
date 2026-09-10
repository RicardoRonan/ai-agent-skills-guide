# AI Agent Skills Implementation Guide

Built by [TheDevRicardo](https://thedevricardo.co.za).

A universal guide for implementing and managing AI agent skills across 7 major coding agents. Works with OpenCode, Claude Code, Cursor, Codex, Windsurf, GitHub Copilot, and Gemini CLI.

## What This Is

This guide covers how to install, configure, and manage a skill library following the [Agent Skills standard](https://agentskills.io). It is written to be read by any AI coding agent: the agent detects which tool it is, then follows the correct paths and commands for that agent.

The library ships with 159 curated skills drawn from six source repos, organized into role-based packages so you install what fits your work instead of everything.

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
| Skills Catalog | 159 skills organized by category with role package tags |
| Skill Activation | When the agent loads each skill, intent routing, and token-smart rules |
| Installation | Role-based install scripts (OpenCode, Claude Code, Cursor, Codex, Windsurf, Copilot, Gemini) |
| Directory Structure | Where skills live on disk per agent |
| Cross-Tool Compatibility | Which frontmatter fields work across agents |
| Avoiding AI Writing Tells | Rules for writing human-sounding skill content |
| Keeping the Catalog Updated | Re-run procedure that detects and adds new upstream skills |
| Contributing | How to create your own custom skills |
| Resources | Links to specs, docs, and skill sources |

## Role-Based Packages

Pick one or more roles that match your work. Each installs a curated set of skills, and selecting several merges them.

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
| `automation` | 14 | n8n and workflow automation |
| `gtm` | 16 | Go-to-market, sales, RevOps |
| `finance` | 15 | Finance, accounting, FP&A, startup CFO |

Combine roles (for example `("fullstack", "devops")`) and add individual skills on top with the `$extras` array. Duplicates across roles are removed automatically.

## How Skills Activate

Skills load lazily. Only each skill's `name` and `description` are read at startup (about 100 tokens). The full instructions load only when a task matches, so an idle skill costs almost nothing.

The guide's Skill Activation section gives the agent a trigger table mapping user intent to a skill, plus token-smart rules:

- Route on intent, not a single keyword
- Load the narrowest matching skill, not several broad ones
- Skip skills for trivial asks
- Prefer subagent isolation for read-heavy exploration so raw file reads stay out of the main context
- Apply `write-concisely` to human-facing output

Examples: asking to write or edit copy loads `copywriting` then `copy-editing`. Asking to cut token usage or shrink a bloated `CLAUDE.md` loads `context-engineering` then `write-concisely`. Asking to review an auth PR loads `security-reviewer` then `code-reviewer`.

## Skills Catalog

159 skills across 16 categories. Expand any category to see each skill, its purpose, and the role packages that include it. `all` means the skill is part of every role package.

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
<summary><strong>Code Quality & Security</strong> (6 skills)</summary>

| Skill | Purpose | Packages |
|-------|---------|----------|
| `code-reviewer` | PR reviews, security vulnerabilities, code smells | all |
| `security-reviewer` | SAST, penetration testing, vulnerability scanning | fullstack, backend, security, architect |
| `best-practices` | CSP, SRI, Trusted Types, browser compatibility | fullstack, frontend, backend |
| `fullstack-guardian` | Security-focused full-stack implementation | fullstack, backend, security |
| `code-documenter` | Documentation generation and standards | fullstack, backend |
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

<details>
<summary><strong>Automation Platforms</strong> (14 skills)</summary>

| Skill | Purpose | Packages |
|-------|---------|----------|
| `n8n-workflow-lifecycle-official` | n8n workflow design, organization, and lifecycle | automation |
| `n8n-subworkflows-official` | Reusable and multi-step n8n sub-workflows | automation |
| `n8n-extending-mcp-official` | Extend n8n MCP capabilities | automation |
| `n8n-expressions-official` | n8n expressions and data references | automation |
| `n8n-node-configuration-official` | Configuring n8n nodes | automation |
| `n8n-code-nodes-official` | Custom logic in n8n Code nodes | automation |
| `n8n-loops-official` | Loops, batching, and pagination | automation |
| `n8n-agents-official` | LangChain Agent node, tools, structured output | automation |
| `n8n-error-handling-official` | Error handling for production n8n workflows | automation |
| `n8n-credentials-and-security-official` | Auth, API keys, and credentials in n8n | automation |
| `n8n-binary-and-data-official` | Files, images, and attachments in n8n | automation |
| `n8n-data-tables-official` | n8n Data Tables: schemas, dedup, state | automation |
| `n8n-debugging-official` | Debugging n8n workflows | automation |
| `using-n8n-skills-official` | Router for the official n8n skill set | automation |

</details>

<details>
<summary><strong>Go-to-Market</strong> (16 skills)</summary>

| Skill | Purpose | Packages |
|-------|---------|----------|
| `gtm-context` | Capture company, ICP, motion, and metrics context | gtm |
| `icp-scoring` | ICP definition and account scoring | gtm |
| `positioning-messaging` | Positioning and messaging hierarchy | gtm |
| `pricing-strategy` | Pricing, packaging, and willingness to pay | gtm |
| `buyer-psychology` | Buyer psychology for GTM decisions | gtm |
| `competitive-intel` | Competitive intelligence and battlecards | gtm |
| `cold-email-strategy` | Cold email strategy and sequences | gtm |
| `cold-email-copywriting` | Cold email copywriting | gtm |
| `email-deliverability` | Domain and inbox deliverability | gtm |
| `multi-channel-outreach` | Multi-channel outreach cadence | gtm |
| `pipeline-management` | Pipeline management and hygiene | gtm |
| `meeting-prep` | Pre-call research and briefing | gtm |
| `objection-handling` | Diagnose and handle objections | gtm |
| `sales-enablement` | Sales asset and enablement creation | gtm |
| `gtm-metrics` | GTM metrics and dashboards | gtm |
| `attribution` | Marketing attribution modeling | gtm |

</details>

<details>
<summary><strong>Financial</strong> (15 skills)</summary>

| Skill | Purpose | Packages |
|-------|---------|----------|
| `financial-analysis` | Financial statement analysis and ratios | finance |
| `budget-forecast` | Budgets, forecasts, and variance analysis | finance |
| `statement-preparation` | Income statement, balance sheet, cash flow (IFRS/GAAP) | finance |
| `investment-analysis` | NPV, IRR, payback, and sensitivity analysis | finance |
| `audit-checklist` | Audit checklists, workpapers, and test procedures | finance |
| `automated-reconciliation` | Bank and account reconciliation at scale | finance |
| `tax-planning` | Tax position optimization and compliance | finance |
| `revenue-recognition` | IFRS 15 / ASC 606 revenue recognition | finance |
| `risk-assessment` | Credit, market, operational, and liquidity risk | finance |
| `treasury-management` | Cash, working capital, and liquidity | finance |
| `wacc-computation` | Weighted average cost of capital | finance |
| `credit-analysis` | Credit risk and rating analysis | finance |
| `cash-forecasting` | Rolling cash forecast and runway (startup CFO) | finance |
| `cap-table-management` | Cap table, dilution, and option pool | finance |
| `unit-economics-analysis` | CAC, LTV, and payback analysis | finance |

</details>

The source of truth, including the full upstream skill sets and the self-update procedure, is in `AI_AGENT_SKILLS_IMPLEMENTATION.md`.

## Quick Start

1. Open `AI_AGENT_SKILLS_IMPLEMENTATION.md`
2. Follow the Agent Detection section to identify your agent
3. Pick one or more roles and run the install script for your agent
4. Skills are now available across all your projects

## Universal Fallback

If you use multiple agents or aren't sure which one, install skills to `.agents/skills/` at your project root. Nearly every compatible agent reads from that directory.

## Self-Updating Catalog

The guide keeps itself current. The Skills Catalog carries a `Last synced` date, and the "Keeping the Catalog Updated" section holds scripts that:

1. Detect skills added to the upstream repos since that date (via commit history)
2. Detect catalog entries that were removed or renamed upstream
3. Fetch each new skill's description
4. Classify it into a category and role package

Run the guide again after a while and the agent runs these checks before acting, so the catalog never drifts from upstream. The repo currently ships 159 curated skills across six upstream repos.

## Contributing

See the Contributing section in the guide for how to create custom skills using the Agent Skills standard.

## Author

Built by [TheDevRicardo](https://thedevricardo.co.za).

## Licensing and Attribution

This guide is original work, licensed MIT (see [LICENSE](LICENSE)). It does not bundle third-party skill files. The install scripts fetch each skill directly from its source repo at install time, so every skill keeps its own license.

| Source | License | Used for |
|--------|---------|----------|
| hosseinmirzapur/opencode-skills | Apache-2.0 | language, workflow, design, data, content skills |
| NeoLabHQ/context-engineering-kit | GPL-3.0 | token optimization and context engineering |
| n8n-io/skills | Apache-2.0 | automation platform skills |
| LeadMagic/gtm-skills | MIT | go-to-market skills |
| GAJETOso/financeskills | MIT | professional finance skills |
| gokulb20/crewm8-cfo-skills | MIT | startup CFO skills |
| Checklist-Design/skills | MIT | checklist-design |

- The MIT license here covers only this guide and its scripts, not the downloaded skills.
- Each skill carries its own author and license in its `SKILL.md` frontmatter.
- If you redistribute downloaded skills, follow each skill's license. The GPL-3.0 skills require GPL terms and source availability if redistributed.
- Not legal advice. Verify licenses before commercial use.

## License

MIT. See [LICENSE](LICENSE).
