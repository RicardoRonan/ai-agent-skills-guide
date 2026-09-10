# AI Agent Skills Implementation Guide

## Overview

This document describes the implementation of a comprehensive skill library following the [Agent Skills standard](https://agentskills.io), an open format installed globally across all projects. The skills enhance any compatible AI coding agent's ability to research, plan, and execute developer tasks with specialized knowledge.

This guide works with **OpenCode, Claude Code, Cursor, Codex, Windsurf, GitHub Copilot, Gemini CLI**, and any Agent Skills-compatible agent. The document itself is self-adapting: follow the Agent Detection section to find your agent's paths and commands.

## Goals

1. **Global Installation**: Skills installed in your agent's personal directory are available across all projects
2. **Comprehensive Coverage**: 114 curated skills covering design, code quality, security, architecture, testing, DevOps, languages, token optimization, and more
3. **Workflow Enhancement**: Skills designed to increase developer productivity and code quality

## Agent Detection

> **Before proceeding, identify which agent you are.** Check your runtime environment, configuration files, or CLI name. Then follow the paths and commands specific to your agent throughout this document.

| Check for | You are |
|-----------|---------|
| `opencode` CLI or `~/.config/opencode/` exists | **OpenCode** |
| `claude` CLI or `~/.claude/` exists | **Claude Code** |
| Cursor IDE open or `~/.cursor/` exists | **Cursor** |
| `codex` CLI or `~/.codex/` exists | **Codex** |
| Windsurf/Devin IDE open or `~/.codeium/` exists | **Windsurf** |
| `gh copilot` CLI or VS Code with Copilot extension | **GitHub Copilot** |
| `gemini` CLI or `~/.gemini/` exists | **Gemini CLI** |

**If you cannot determine your agent**, use `.agents/skills/` at your project root. This directory is read by nearly every compatible agent.

## Supported Agents

| Agent | Personal Skills Dir | Project Skills Dir | Instruction File | SKILL.md Support |
|-------|--------------------|--------------------|-----------------|-----------------|
| **OpenCode** | `~/.config/opencode/skills/` | — | — | Yes |
| **Claude Code** | `~/.claude/skills/` | `.claude/skills/` | `CLAUDE.md` | Yes |
| **Cursor** | `~/.cursor/skills/` | `.cursor/skills/` | `.cursor/rules/*.mdc` | Yes |
| **Codex** | `~/.agents/skills/` | `.agents/skills/` | `AGENTS.md` | Yes |
| **Windsurf** | — | `.agents/skills/` | `.windsurfrules` | Yes (via compat) |
| **GitHub Copilot** | `~/.copilot/skills/` | `.github/skills/` or `.agents/skills/` | `.github/copilot-instructions.md` | Yes |
| **Gemini CLI** | `~/.agents/skills/` | `.agents/skills/` | — | Yes |

> **Universal fallback**: `.agents/skills/` at project root is readable by nearly every agent. If in doubt, install there.

## The Agent Skills Standard

All skills in this library follow the [Agent Skills standard](https://agentskills.io), an open format supported by 40+ AI coding tools. A skill is a directory containing a `SKILL.md` file with:

- **YAML frontmatter**: `name`, `description`, and optional fields (`license`, `metadata`, `compatibility`, `allowed-tools`)
- **Markdown body**: Instructions the agent follows when the skill activates
- **Optional directories**: `scripts/`, `references/`, `assets/`

Skills use **progressive disclosure**:
1. **Discovery** (~100 tokens): Agent reads only `name` and `description` at startup
2. **Activation** (< 5000 tokens recommended): Full `SKILL.md` body loads when a task matches
3. **Execution** (as needed): Referenced files load only when the instructions reach for them

This means skills cost almost nothing in context until they are needed.

## Skills Catalog

All available skills organized by category. See the Installation section to pick a role package or build a custom set.

> **Catalog sync:** `Last synced: 2026-09-11` | `Upstream: hosseinmirzapur/opencode-skills`, `NeoLabHQ/context-engineering-kit` | `Tracked: 114 skills`.
> If you are an agent running this guide, run the **Keeping the Catalog Updated** section at the end before trusting these tables. The upstream repo adds skills regularly.

### Design & UI/UX
| Skill | Purpose | Packages |
|-------|---------|----------|
| checklist-design | 129 UI/UX checklists for web, mobile, design systems | frontend |
| design-review | Visual audit with before/after screenshots | fullstack, frontend |
| apple-hig | Apple Human Interface Guidelines | frontend |
| brutalist-skill | Brutalist design patterns | frontend |
| canvas-design | Canvas-based design | frontend |
| color-expert | Color theory and palette generation | frontend |
| design-brief | Design brief creation | frontend |
| design-consultation | Design consultation workflows | frontend |
| design-shotgun | Design exploration and ideation | frontend |
| frontend-design | Frontend design patterns and best practices | frontend |
| hand-drawn-diagrams | Hand-drawn diagram generation | frontend |
| image-to-code-skill | Convert visual designs to code | frontend |
| minimalist-skill | Minimalist design principles | frontend |
| platform-design | Platform-specific design guidelines | frontend |
| shadcn-ui | shadcn/ui component patterns | frontend |
| ui-ux-pro-max | Advanced UI/UX workflows | frontend |
| web-design-guidelines | Web design standards and patterns | frontend |

### Code Quality & Security
| Skill | Purpose | Packages |
|-------|---------|----------|
| code-reviewer | PR reviews, security vulnerabilities, code smells | all |
| security-reviewer | SAST, penetration testing, vulnerability scanning | fullstack, backend, security, architect |
| best-practices | CSP, SRI, Trusted Types, browser compatibility | fullstack, frontend, backend |
| fullstack-guardian | Security-focused full-stack implementation | fullstack, backend, security |
| code-documenter | Documentation generation and standards | fullstack, backend |
| secure-code-guardian | Secure coding patterns and review | security |

### Development Workflow
| Skill | Purpose | Packages |
|-------|---------|----------|
| feature-forge | Requirements workshops, user stories, EARS specs | all |
| executing-plans | Step-by-step plan execution | fullstack, backend, architect |
| brainstorming | Idea generation and exploration | fullstack, frontend, mobile |
| evaluation | Solution assessment and comparison | fullstack, backend, architect, data |
| finishing-a-development-branch | Branch completion and merge workflows | fullstack, backend |
| onboarding | Project onboarding for new contributors | fullstack, backend |
| pr-feedback-quality-gate | PR feedback standards and quality checks | fullstack, backend, architect |
| receiving-code-review | How to receive and apply review feedback | fullstack, backend |
| requesting-code-review | How to request effective reviews | fullstack, backend |
| systematic-debugging | Debugging methodology and process | fullstack, backend, mobile |
| test-driven-development | TDD workflows and patterns | fullstack, backend |
| using-git-worktrees | Git worktree patterns for parallel work | fullstack, backend |
| verification-before-completion | Pre-ship verification checklists | all |

### Architecture & Design
| Skill | Purpose | Packages |
|-------|---------|----------|
| architecture-designer | System design, ADRs, scalability planning | fullstack, backend, architect |
| api-designer | REST/GraphQL APIs, OpenAPI specs | fullstack, backend, architect |
| cloud-architect | Cloud infrastructure design and planning | devops, architect |
| graphql-architect | GraphQL schema design and federation | backend, architect |
| microservices-architect | Microservice patterns and decomposition | architect |
| site-architecture | Site structure and information architecture | frontend, architect |

### Testing & Quality
| Skill | Purpose | Packages |
|-------|---------|----------|
| test-master | Unit, integration, E2E, performance testing | fullstack, backend |
| debugging-wizard | Systematic debugging methodology | fullstack, backend, mobile |
| playwright-expert | Playwright test patterns and strategies | fullstack, frontend |
| export-download-debugging | Export and download flow debugging | fullstack, frontend |
| verification-before-completion | Pre-completion verification checks | all |

### Infrastructure & DevOps
| Skill | Purpose | Packages |
|-------|---------|----------|
| devops-engineer | CI/CD, Docker, Kubernetes, Terraform | fullstack, backend, devops |
| database-optimizer | Query optimization, index design | fullstack, backend, devops |
| chaos-engineer | Resilience testing, failure injection | devops, security |
| kubernetes-specialist | Kubernetes deep dive and operations | devops |
| monitoring-expert | Observability, alerting, dashboards | devops |
| postgres-pro | PostgreSQL advanced patterns | backend, devops |
| redis-core | Redis patterns and data structures | backend, devops |
| redis-query-engine | Redis query optimization | backend, devops |
| sre-engineer | Site reliability engineering | devops |
| spark-engineer | Apache Spark data processing | data, devops |
| sql-pro | SQL optimization and advanced queries | backend, devops, data |
| terraform-engineer | Terraform infrastructure as code | devops |

### Language & Frameworks
| Skill | Purpose | Packages |
|-------|---------|----------|
| react-expert | React 19, Server Components, hooks | fullstack, frontend |
| typescript-pro | Advanced types, type guards, tRPC | fullstack, frontend, backend |
| vue-expert | Vue.js 3, Composition API, Nuxt | frontend |
| angular-architect | Angular patterns and architecture | frontend |
| nextjs-developer | Next.js App Router, Server Components | frontend |
| nestjs-expert | NestJS patterns and architecture | backend |
| python-pro | Python patterns, asyncio, packaging | data, backend |
| javascript-pro | Modern JavaScript patterns | fullstack, frontend |
| golang-pro | Go concurrency, patterns, stdlib | backend |
| rust-engineer | Rust ownership, async, systems programming | backend |
| java-architect | Java patterns, Spring ecosystem | backend |
| kotlin-specialist | Kotlin coroutines, Android, patterns | mobile, backend |
| swift-expert | Swift, SwiftUI, iOS patterns | mobile |
| php-pro | PHP patterns, modern PHP 8+ | backend |
| csharp-developer | C#/.NET patterns and best practices | backend |
| cpp-pro | C++ modern patterns, performance | backend |
| flutter-expert | Flutter/Dart app patterns | mobile |
| rails-expert | Ruby on Rails patterns and conventions | backend |
| laravel-specialist | Laravel patterns and best practices | backend |
| spring-boot-engineer | Spring Boot patterns and configuration | backend |
| dotnet-core-expert | .NET Core patterns and middleware | backend |
| django-expert | Django patterns, ORM, views | backend |
| fastapi-expert | FastAPI patterns, async, validation | backend |
| react-native-expert | React Native patterns and debugging | mobile |
| wordpress-pro | WordPress plugin and theme development | backend |
| shopify-expert | Shopify Liquid, Storefront API | backend |

### Content & Marketing
| Skill | Purpose | Packages |
|-------|---------|----------|
| copywriting | Marketing copy, landing pages, CTAs | content |
| copy-editing | Polish and refine existing copy | content |
| cold-email | Cold email writing and sequences | content |
| emails | Email copywriting and automation | content |
| seo | SEO optimization and strategy | content |

### AI & Machine Learning
| Skill | Purpose | Packages |
|-------|---------|----------|
| fine-tuning-expert | Model fine-tuning strategies | data |
| ml-pipeline | ML pipeline design and orchestration | data |
| rag-architect | RAG system design and retrieval | data |

### Token Optimization & Context Engineering
| Skill | Purpose | Packages |
|-------|---------|----------|
| context-engineering | Context components, mechanics, and constraints in agent systems | all |
| multi-agent-patterns | Multi-agent architectures for context isolation | all |
| write-concisely | Concise writing rules to cut output tokens | all |
| prompt-engineer | Prompt design and refactoring for token efficiency | all |
| launch-sub-agent | Dispatch an isolated subagent for a task | optimize |
| do-in-parallel | Run independent tasks in parallel subagents | optimize |
| memorize | Curate insights into CLAUDE.md (agentic memory) | optimize |
| decay | Prune stale memory and context | optimize |
| reset | Reset context cleanly between tasks | optimize |
| apply-anthropic-skill-best-practices | Token-efficient skill authoring | optimize |
| prompt-engineering | Advanced prompt patterns for agents, hooks, and skills | optimize |
| test-prompt | Test and iterate prompts | optimize |
| setup-codemap-cli | Semantic code retrieval to cut file reads | optimize |
| setup-serena-mcp | Serena MCP for semantic code retrieval | optimize |
| output-skill | Full-output enforcement, handles token-limit splits | optimize |
| graphify | Turn a codebase into a queryable knowledge graph | optimize |

### Data & Visualization
| Skill | Purpose | Packages |
|-------|---------|----------|
| d3-visualization | D3.js chart and visualization patterns | data, frontend |
| data-report | Data reporting and presentation | data |
| pandas-pro | Pandas data analysis patterns | data |

### CLI & Tools
| Skill | Purpose | Packages |
|-------|---------|----------|
| cli-developer | CLI tools, argument parsing, completions | fullstack |
| mcp-developer | MCP server development patterns | backend |

### Game Development
| Skill | Purpose | Packages |
|-------|---------|----------|
| game-developer | Game development patterns and engines | (standalone) |

## Installation

### Prerequisites
- An AI coding agent installed (see Supported Agents table)
- Git installed
- PowerShell (Windows) or bash (macOS/Linux)

### Step 1: Choose Your Role

Pick the role that matches your work. Each role installs a curated set of skills.

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

You can add individual skills on top of any role. See the Skills Catalog for the full list.

### Step 2: Configure Your Install

Each agent section below includes a script with two variables at the top:

```powershell
# Uncomment the role that matches your work
$role = "fullstack"

# Add extra skills you want beyond your role (optional)
$extras = @(
    # "python-pro",
    # "vue-expert",
)
```

Change `$role` to your role. Add any extra skills to `$extras`. Delete or comment out lines you don't want.

### Step 3: Run the Script

Each agent has its own install script below. Copy and run the one for your agent.

---

#### OpenCode

**Personal (all projects):**
```powershell
mkdir -p ~/.config/opencode/skills
```

**Install Checklist-Design:**
```powershell
git clone https://github.com/Checklist-Design/skills.git /tmp/checklist-skills
cp -r /tmp/checklist-skills/skills/checklist-design ~/.config/opencode/skills/
```

**Install skills (PowerShell):**
```powershell
# STEP 1: Pick your role (uncomment ONE)
$role = "fullstack"
# Options: fullstack, frontend, backend, devops, mobile, data, security, architect, content, optimize, optimize

# STEP 2: Add extra skills you want (optional)
$extras = @(
    # "python-pro",
    # "vue-expert",
    # "d3-visualization",
)

# Skills included in every role (token optimization / context engineering)
$base = @("context-engineering","write-concisely","prompt-engineer","multi-agent-patterns")

# Role-to-skills mapping
$roleSkills = @{
    fullstack = @("code-reviewer","security-reviewer","best-practices","fullstack-guardian",
                  "feature-forge","executing-plans","brainstorming","evaluation",
                  "architecture-designer","api-designer","test-master","debugging-wizard",
                  "devops-engineer","database-optimizer","react-expert","typescript-pro",
                  "copywriting","cli-developer","design-review","verification-before-completion")
    frontend  = @("checklist-design","design-review","apple-hig","color-expert","shadcn-ui",
                  "frontend-design","ui-ux-pro-max","web-design-guidelines",
                  "code-reviewer","best-practices","feature-forge","brainstorming",
                  "evaluation","react-expert","typescript-pro","verification-before-completion")
    backend   = @("code-reviewer","security-reviewer","best-practices","fullstack-guardian",
                  "feature-forge","executing-plans","evaluation",
                  "architecture-designer","api-designer","test-master","debugging-wizard",
                  "devops-engineer","database-optimizer","sql-pro","verification-before-completion")
    devops    = @("devops-engineer","database-optimizer","chaos-engineer",
                  "kubernetes-specialist","monitoring-expert","sre-engineer",
                  "terraform-engineer","postgres-pro","redis-core",
                  "code-reviewer","best-practices","feature-forge","verification-before-completion")
    mobile    = @("code-reviewer","security-reviewer","best-practices",
                  "feature-forge","executing-plans","brainstorming",
                  "test-master","debugging-wizard",
                  "react-native-expert","flutter-expert","typescript-pro","verification-before-completion")
    data      = @("code-reviewer","best-practices","feature-forge","evaluation",
                  "python-pro","sql-pro","pandas-pro",
                  "d3-visualization","data-report","verification-before-completion")
    security  = @("security-reviewer","secure-code-guardian","fullstack-guardian",
                  "best-practices","code-reviewer","architecture-designer",
                  "chaos-engineer","devops-engineer","verification-before-completion")
    architect = @("architecture-designer","api-designer","microservices-architect",
                  "cloud-architect","graphql-architect",
                  "code-reviewer","security-reviewer",
                  "feature-forge","executing-plans","evaluation","verification-before-completion")
    content   = @("copywriting","copy-editing","cold-email","emails","seo",
                  "code-reviewer","verification-before-completion")
    optimize  = @("context-engineering","multi-agent-patterns","launch-sub-agent","do-in-parallel",
                  "memorize","decay","reset","write-concisely",
                  "apply-anthropic-skill-best-practices","prompt-engineering","test-prompt",
                  "setup-codemap-cli","setup-serena-mcp",
                  "prompt-engineer","output-skill","graphify")
}

# Skills that come from a repo other than the default
$sourceMap = @{
    "context-engineering"                  = "NeoLabHQ/context-engineering-kit@master"
    "multi-agent-patterns"                 = "NeoLabHQ/context-engineering-kit@master"
    "launch-sub-agent"                     = "NeoLabHQ/context-engineering-kit@master"
    "do-in-parallel"                       = "NeoLabHQ/context-engineering-kit@master"
    "memorize"                             = "NeoLabHQ/context-engineering-kit@master"
    "decay"                                = "NeoLabHQ/context-engineering-kit@master"
    "reset"                                = "NeoLabHQ/context-engineering-kit@master"
    "write-concisely"                      = "NeoLabHQ/context-engineering-kit@master"
    "apply-anthropic-skill-best-practices" = "NeoLabHQ/context-engineering-kit@master"
    "prompt-engineering"                   = "NeoLabHQ/context-engineering-kit@master"
    "test-prompt"                          = "NeoLabHQ/context-engineering-kit@master"
    "setup-codemap-cli"                    = "NeoLabHQ/context-engineering-kit@master"
    "setup-serena-mcp"                     = "NeoLabHQ/context-engineering-kit@master"
}
$defaultSource = "hosseinmirzapur/opencode-skills@main"

$skills = ($roleSkills[$role] + $base + $extras) | Select-Object -Unique

foreach ($skill in $skills) {
    $src = if ($sourceMap.ContainsKey($skill)) { $sourceMap[$skill] } else { $defaultSource }
    $repo, $branch = $src -split '@'
    $url = "https://raw.githubusercontent.com/$repo/$branch/skills/$skill/SKILL.md"
    $outputDir = "$env:USERPROFILE\.config\opencode\skills\$skill"
    New-Item -ItemType Directory -Force -Path $outputDir | Out-Null
    Invoke-WebRequest -Uri $url -OutFile "$outputDir\SKILL.md"
}
```

**Install references (optional):**
```powershell
$skillsWithReferences = @("code-reviewer","security-reviewer","fullstack-guardian",
                          "feature-forge","architecture-designer","api-designer",
                          "test-master","debugging-wizard","devops-engineer",
                          "database-optimizer","react-expert","typescript-pro","cli-developer")

foreach ($skill in $skillsWithReferences) {
    $baseUrl = "https://api.github.com/repos/hosseinmirzapur/opencode-skills/contents/skills/$skill/references"
    $response = Invoke-RestMethod -Uri $baseUrl
    $outputDir = "$env:USERPROFILE\.config\opencode\skills\$skill\references"
    New-Item -ItemType Directory -Force -Path $outputDir | Out-Null
    foreach ($file in $response) {
        if ($file.type -eq "file") {
            Invoke-WebRequest -Uri $file.download_url -OutFile "$outputDir\$($file.name)"
        }
    }
}
```

---

#### Claude Code

**Personal (all projects):**
```bash
mkdir -p ~/.claude/skills
```

**Project (shared via git):**
```bash
mkdir -p .claude/skills
```

**Install skills (bash):**
```bash
# STEP 1: Pick your role (uncomment ONE)
ROLE="fullstack"
# Options: fullstack, frontend, backend, devops, mobile, data, security, architect, content, optimize

# STEP 2: Add extra skills you want (optional)
EXTRAS=()
# EXTRAS=("python-pro" "vue-expert" "d3-visualization")

SKILLS_DIR="$HOME/.claude/skills"  # or ".claude/skills" for project-local

# Checklist-Design
git clone https://github.com/Checklist-Design/skills.git /tmp/checklist-skills
cp -r /tmp/checklist-skills/skills/checklist-design "$SKILLS_DIR/"

# Role-to-skills mapping
case $ROLE in
  fullstack) SKILLS=(code-reviewer security-reviewer best-practices fullstack-guardian
                     feature-forge executing-plans brainstorming evaluation
                     architecture-designer api-designer test-master debugging-wizard
                     devops-engineer database-optimizer react-expert typescript-pro
                     copywriting cli-developer design-review verification-before-completion) ;;
  frontend)  SKILLS=(checklist-design design-review apple-hig color-expert shadcn-ui
                     frontend-design ui-ux-pro-max web-design-guidelines
                     code-reviewer best-practices feature-forge brainstorming
                     evaluation react-expert typescript-pro verification-before-completion) ;;
  backend)   SKILLS=(code-reviewer security-reviewer best-practices fullstack-guardian
                     feature-forge executing-plans evaluation
                     architecture-designer api-designer test-master debugging-wizard
                     devops-engineer database-optimizer sql-pro verification-before-completion) ;;
  devops)    SKILLS=(devops-engineer database-optimizer chaos-engineer
                     kubernetes-specialist monitoring-expert sre-engineer
                     terraform-engineer postgres-pro redis-core
                     code-reviewer best-practices feature-forge verification-before-completion) ;;
  mobile)    SKILLS=(code-reviewer security-reviewer best-practices
                     feature-forge executing-plans brainstorming
                     test-master debugging-wizard
                     react-native-expert flutter-expert typescript-pro verification-before-completion) ;;
  data)      SKILLS=(code-reviewer best-practices feature-forge evaluation
                     python-pro sql-pro pandas-pro
                     d3-visualization data-report verification-before-completion) ;;
  security)  SKILLS=(security-reviewer secure-code-guardian fullstack-guardian
                     best-practices code-reviewer architecture-designer
                     chaos-engineer devops-engineer verification-before-completion) ;;
  architect) SKILLS=(architecture-designer api-designer microservices-architect
                     cloud-architect graphql-architect
                     code-reviewer security-reviewer
                     feature-forge executing-plans evaluation verification-before-completion) ;;
  content)   SKILLS=(copywriting copy-editing cold-email emails seo
                     code-reviewer verification-before-completion) ;;
  optimize)  SKILLS=(context-engineering multi-agent-patterns launch-sub-agent do-in-parallel
                     memorize decay reset write-concisely
                     apply-anthropic-skill-best-practices prompt-engineering test-prompt
                     setup-codemap-cli setup-serena-mcp
                     prompt-engineer output-skill graphify) ;;
esac

# Skills included in every role (token optimization / context engineering)
BASE=(context-engineering write-concisely prompt-engineer multi-agent-patterns)

# Skills sourced from a repo other than the default
source_repo() {
    case "$1" in
        context-engineering|multi-agent-patterns|launch-sub-agent|do-in-parallel|\
        memorize|decay|reset|write-concisely|apply-anthropic-skill-best-practices|\
        prompt-engineering|test-prompt|setup-codemap-cli|setup-serena-mcp)
            echo "NeoLabHQ/context-engineering-kit/master" ;;
        *) echo "hosseinmirzapur/opencode-skills/main" ;;
    esac
}

ALL_SKILLS=($(printf "%s\n" "${SKILLS[@]}" "${BASE[@]}" "${EXTRAS[@]}" | awk '!seen[$0]++'))

for skill in "${ALL_SKILLS[@]}"; do
    src=$(source_repo "$skill")
    mkdir -p "$SKILLS_DIR/$skill"
    curl -sL "https://raw.githubusercontent.com/$src/skills/$skill/SKILL.md" \
        -o "$SKILLS_DIR/$skill/SKILL.md"
done
```

**If your agent is Claude Code**, see the dedicated section below for `CLAUDE.md` setup and `AGENTS.md` template.

---

#### Cursor

**Personal (all projects):**
```bash
mkdir -p ~/.cursor/skills
```

**Project (shared via git):**
```bash
mkdir -p .cursor/skills
```

**Install skills (bash):**
```bash
# STEP 1: Pick your role (uncomment ONE)
ROLE="fullstack"
# Options: fullstack, frontend, backend, devops, mobile, data, security, architect, content, optimize

# STEP 2: Add extra skills you want (optional)
EXTRAS=()
# EXTRAS=("python-pro" "vue-expert" "d3-visualization")

SKILLS_DIR="$HOME/.cursor/skills"  # or ".cursor/skills" for project-local

# Checklist-Design
git clone https://github.com/Checklist-Design/skills.git /tmp/checklist-skills
cp -r /tmp/checklist-skills/skills/checklist-design "$SKILLS_DIR/"

# Role-to-skills mapping
case $ROLE in
  fullstack) SKILLS=(code-reviewer security-reviewer best-practices fullstack-guardian
                     feature-forge executing-plans brainstorming evaluation
                     architecture-designer api-designer test-master debugging-wizard
                     devops-engineer database-optimizer react-expert typescript-pro
                     copywriting cli-developer design-review verification-before-completion) ;;
  frontend)  SKILLS=(checklist-design design-review apple-hig color-expert shadcn-ui
                     frontend-design ui-ux-pro-max web-design-guidelines
                     code-reviewer best-practices feature-forge brainstorming
                     evaluation react-expert typescript-pro verification-before-completion) ;;
  backend)   SKILLS=(code-reviewer security-reviewer best-practices fullstack-guardian
                     feature-forge executing-plans evaluation
                     architecture-designer api-designer test-master debugging-wizard
                     devops-engineer database-optimizer sql-pro verification-before-completion) ;;
  devops)    SKILLS=(devops-engineer database-optimizer chaos-engineer
                     kubernetes-specialist monitoring-expert sre-engineer
                     terraform-engineer postgres-pro redis-core
                     code-reviewer best-practices feature-forge verification-before-completion) ;;
  mobile)    SKILLS=(code-reviewer security-reviewer best-practices
                     feature-forge executing-plans brainstorming
                     test-master debugging-wizard
                     react-native-expert flutter-expert typescript-pro verification-before-completion) ;;
  data)      SKILLS=(code-reviewer best-practices feature-forge evaluation
                     python-pro sql-pro pandas-pro
                     d3-visualization data-report verification-before-completion) ;;
  security)  SKILLS=(security-reviewer secure-code-guardian fullstack-guardian
                     best-practices code-reviewer architecture-designer
                     chaos-engineer devops-engineer verification-before-completion) ;;
  architect) SKILLS=(architecture-designer api-designer microservices-architect
                     cloud-architect graphql-architect
                     code-reviewer security-reviewer
                     feature-forge executing-plans evaluation verification-before-completion) ;;
  content)   SKILLS=(copywriting copy-editing cold-email emails seo
                     code-reviewer verification-before-completion) ;;
  optimize)  SKILLS=(context-engineering multi-agent-patterns launch-sub-agent do-in-parallel
                     memorize decay reset write-concisely
                     apply-anthropic-skill-best-practices prompt-engineering test-prompt
                     setup-codemap-cli setup-serena-mcp
                     prompt-engineer output-skill graphify) ;;
esac

# Skills included in every role (token optimization / context engineering)
BASE=(context-engineering write-concisely prompt-engineer multi-agent-patterns)

# Skills sourced from a repo other than the default
source_repo() {
    case "$1" in
        context-engineering|multi-agent-patterns|launch-sub-agent|do-in-parallel|\
        memorize|decay|reset|write-concisely|apply-anthropic-skill-best-practices|\
        prompt-engineering|test-prompt|setup-codemap-cli|setup-serena-mcp)
            echo "NeoLabHQ/context-engineering-kit/master" ;;
        *) echo "hosseinmirzapur/opencode-skills/main" ;;
    esac
}

ALL_SKILLS=($(printf "%s\n" "${SKILLS[@]}" "${BASE[@]}" "${EXTRAS[@]}" | awk '!seen[$0]++'))

for skill in "${ALL_SKILLS[@]}"; do
    src=$(source_repo "$skill")
    mkdir -p "$SKILLS_DIR/$skill"
    curl -sL "https://raw.githubusercontent.com/$src/skills/$skill/SKILL.md" \
        -o "$SKILLS_DIR/$skill/SKILL.md"
done
```

> Cursor also reads `.claude/skills/` and `.codex/skills/` for compatibility, so skills installed for other agents may already work.

---

#### Codex

**Personal (all projects):**
```bash
mkdir -p ~/.agents/skills
```

**Project (shared via git):**
```bash
mkdir -p .agents/skills
```

**Install skills (bash):**
```bash
# STEP 1: Pick your role (uncomment ONE)
ROLE="fullstack"
# Options: fullstack, frontend, backend, devops, mobile, data, security, architect, content, optimize

# STEP 2: Add extra skills you want (optional)
EXTRAS=()
# EXTRAS=("python-pro" "vue-expert" "d3-visualization")

SKILLS_DIR="$HOME/.agents/skills"  # or ".agents/skills" for project-local

# Checklist-Design
git clone https://github.com/Checklist-Design/skills.git /tmp/checklist-skills
cp -r /tmp/checklist-skills/skills/checklist-design "$SKILLS_DIR/"

# Role-to-skills mapping
case $ROLE in
  fullstack) SKILLS=(code-reviewer security-reviewer best-practices fullstack-guardian
                     feature-forge executing-plans brainstorming evaluation
                     architecture-designer api-designer test-master debugging-wizard
                     devops-engineer database-optimizer react-expert typescript-pro
                     copywriting cli-developer design-review verification-before-completion) ;;
  frontend)  SKILLS=(checklist-design design-review apple-hig color-expert shadcn-ui
                     frontend-design ui-ux-pro-max web-design-guidelines
                     code-reviewer best-practices feature-forge brainstorming
                     evaluation react-expert typescript-pro verification-before-completion) ;;
  backend)   SKILLS=(code-reviewer security-reviewer best-practices fullstack-guardian
                     feature-forge executing-plans evaluation
                     architecture-designer api-designer test-master debugging-wizard
                     devops-engineer database-optimizer sql-pro verification-before-completion) ;;
  devops)    SKILLS=(devops-engineer database-optimizer chaos-engineer
                     kubernetes-specialist monitoring-expert sre-engineer
                     terraform-engineer postgres-pro redis-core
                     code-reviewer best-practices feature-forge verification-before-completion) ;;
  mobile)    SKILLS=(code-reviewer security-reviewer best-practices
                     feature-forge executing-plans brainstorming
                     test-master debugging-wizard
                     react-native-expert flutter-expert typescript-pro verification-before-completion) ;;
  data)      SKILLS=(code-reviewer best-practices feature-forge evaluation
                     python-pro sql-pro pandas-pro
                     d3-visualization data-report verification-before-completion) ;;
  security)  SKILLS=(security-reviewer secure-code-guardian fullstack-guardian
                     best-practices code-reviewer architecture-designer
                     chaos-engineer devops-engineer verification-before-completion) ;;
  architect) SKILLS=(architecture-designer api-designer microservices-architect
                     cloud-architect graphql-architect
                     code-reviewer security-reviewer
                     feature-forge executing-plans evaluation verification-before-completion) ;;
  content)   SKILLS=(copywriting copy-editing cold-email emails seo
                     code-reviewer verification-before-completion) ;;
  optimize)  SKILLS=(context-engineering multi-agent-patterns launch-sub-agent do-in-parallel
                     memorize decay reset write-concisely
                     apply-anthropic-skill-best-practices prompt-engineering test-prompt
                     setup-codemap-cli setup-serena-mcp
                     prompt-engineer output-skill graphify) ;;
esac

# Skills included in every role (token optimization / context engineering)
BASE=(context-engineering write-concisely prompt-engineer multi-agent-patterns)

# Skills sourced from a repo other than the default
source_repo() {
    case "$1" in
        context-engineering|multi-agent-patterns|launch-sub-agent|do-in-parallel|\
        memorize|decay|reset|write-concisely|apply-anthropic-skill-best-practices|\
        prompt-engineering|test-prompt|setup-codemap-cli|setup-serena-mcp)
            echo "NeoLabHQ/context-engineering-kit/master" ;;
        *) echo "hosseinmirzapur/opencode-skills/main" ;;
    esac
}

ALL_SKILLS=($(printf "%s\n" "${SKILLS[@]}" "${BASE[@]}" "${EXTRAS[@]}" | awk '!seen[$0]++'))

for skill in "${ALL_SKILLS[@]}"; do
    src=$(source_repo "$skill")
    mkdir -p "$SKILLS_DIR/$skill"
    curl -sL "https://raw.githubusercontent.com/$src/skills/$skill/SKILL.md" \
        -o "$SKILLS_DIR/$skill/SKILL.md"
done
```

---

#### Windsurf

Windsurf reads `.agents/skills/` and `.claude/skills/` for compatibility.

**Project (shared via git):**
```bash
mkdir -p .agents/skills
```

**Install skills (bash):**
```bash
# STEP 1: Pick your role (uncomment ONE)
ROLE="fullstack"
# Options: fullstack, frontend, backend, devops, mobile, data, security, architect, content, optimize

# STEP 2: Add extra skills you want (optional)
EXTRAS=()
# EXTRAS=("python-pro" "vue-expert" "d3-visualization")

SKILLS_DIR=".agents/skills"

# Checklist-Design
git clone https://github.com/Checklist-Design/skills.git /tmp/checklist-skills
cp -r /tmp/checklist-skills/skills/checklist-design "$SKILLS_DIR/"

# Role-to-skills mapping
case $ROLE in
  fullstack) SKILLS=(code-reviewer security-reviewer best-practices fullstack-guardian
                     feature-forge executing-plans brainstorming evaluation
                     architecture-designer api-designer test-master debugging-wizard
                     devops-engineer database-optimizer react-expert typescript-pro
                     copywriting cli-developer design-review verification-before-completion) ;;
  frontend)  SKILLS=(checklist-design design-review apple-hig color-expert shadcn-ui
                     frontend-design ui-ux-pro-max web-design-guidelines
                     code-reviewer best-practices feature-forge brainstorming
                     evaluation react-expert typescript-pro verification-before-completion) ;;
  backend)   SKILLS=(code-reviewer security-reviewer best-practices fullstack-guardian
                     feature-forge executing-plans evaluation
                     architecture-designer api-designer test-master debugging-wizard
                     devops-engineer database-optimizer sql-pro verification-before-completion) ;;
  devops)    SKILLS=(devops-engineer database-optimizer chaos-engineer
                     kubernetes-specialist monitoring-expert sre-engineer
                     terraform-engineer postgres-pro redis-core
                     code-reviewer best-practices feature-forge verification-before-completion) ;;
  mobile)    SKILLS=(code-reviewer security-reviewer best-practices
                     feature-forge executing-plans brainstorming
                     test-master debugging-wizard
                     react-native-expert flutter-expert typescript-pro verification-before-completion) ;;
  data)      SKILLS=(code-reviewer best-practices feature-forge evaluation
                     python-pro sql-pro pandas-pro
                     d3-visualization data-report verification-before-completion) ;;
  security)  SKILLS=(security-reviewer secure-code-guardian fullstack-guardian
                     best-practices code-reviewer architecture-designer
                     chaos-engineer devops-engineer verification-before-completion) ;;
  architect) SKILLS=(architecture-designer api-designer microservices-architect
                     cloud-architect graphql-architect
                     code-reviewer security-reviewer
                     feature-forge executing-plans evaluation verification-before-completion) ;;
  content)   SKILLS=(copywriting copy-editing cold-email emails seo
                     code-reviewer verification-before-completion) ;;
  optimize)  SKILLS=(context-engineering multi-agent-patterns launch-sub-agent do-in-parallel
                     memorize decay reset write-concisely
                     apply-anthropic-skill-best-practices prompt-engineering test-prompt
                     setup-codemap-cli setup-serena-mcp
                     prompt-engineer output-skill graphify) ;;
esac

# Skills included in every role (token optimization / context engineering)
BASE=(context-engineering write-concisely prompt-engineer multi-agent-patterns)

# Skills sourced from a repo other than the default
source_repo() {
    case "$1" in
        context-engineering|multi-agent-patterns|launch-sub-agent|do-in-parallel|\
        memorize|decay|reset|write-concisely|apply-anthropic-skill-best-practices|\
        prompt-engineering|test-prompt|setup-codemap-cli|setup-serena-mcp)
            echo "NeoLabHQ/context-engineering-kit/master" ;;
        *) echo "hosseinmirzapur/opencode-skills/main" ;;
    esac
}

ALL_SKILLS=($(printf "%s\n" "${SKILLS[@]}" "${BASE[@]}" "${EXTRAS[@]}" | awk '!seen[$0]++'))

for skill in "${ALL_SKILLS[@]}"; do
    src=$(source_repo "$skill")
    mkdir -p "$SKILLS_DIR/$skill"
    curl -sL "https://raw.githubusercontent.com/$src/skills/$skill/SKILL.md" \
        -o "$SKILLS_DIR/$skill/SKILL.md"
done
```

---

#### GitHub Copilot

**Personal (all projects):**
```bash
mkdir -p ~/.copilot/skills
```

**Project (shared via git):**
```bash
mkdir -p .github/skills    # Copilot-native path
# OR
mkdir -p .agents/skills    # Universal path (also works)
```

**Install skills (bash):**
```bash
# STEP 1: Pick your role (uncomment ONE)
ROLE="fullstack"
# Options: fullstack, frontend, backend, devops, mobile, data, security, architect, content, optimize

# STEP 2: Add extra skills you want (optional)
EXTRAS=()
# EXTRAS=("python-pro" "vue-expert" "d3-visualization")

SKILLS_DIR="$HOME/.copilot/skills"  # or ".agents/skills" for project-local

# Checklist-Design
git clone https://github.com/Checklist-Design/skills.git /tmp/checklist-skills
cp -r /tmp/checklist-skills/skills/checklist-design "$SKILLS_DIR/"

# Role-to-skills mapping
case $ROLE in
  fullstack) SKILLS=(code-reviewer security-reviewer best-practices fullstack-guardian
                     feature-forge executing-plans brainstorming evaluation
                     architecture-designer api-designer test-master debugging-wizard
                     devops-engineer database-optimizer react-expert typescript-pro
                     copywriting cli-developer design-review verification-before-completion) ;;
  frontend)  SKILLS=(checklist-design design-review apple-hig color-expert shadcn-ui
                     frontend-design ui-ux-pro-max web-design-guidelines
                     code-reviewer best-practices feature-forge brainstorming
                     evaluation react-expert typescript-pro verification-before-completion) ;;
  backend)   SKILLS=(code-reviewer security-reviewer best-practices fullstack-guardian
                     feature-forge executing-plans evaluation
                     architecture-designer api-designer test-master debugging-wizard
                     devops-engineer database-optimizer sql-pro verification-before-completion) ;;
  devops)    SKILLS=(devops-engineer database-optimizer chaos-engineer
                     kubernetes-specialist monitoring-expert sre-engineer
                     terraform-engineer postgres-pro redis-core
                     code-reviewer best-practices feature-forge verification-before-completion) ;;
  mobile)    SKILLS=(code-reviewer security-reviewer best-practices
                     feature-forge executing-plans brainstorming
                     test-master debugging-wizard
                     react-native-expert flutter-expert typescript-pro verification-before-completion) ;;
  data)      SKILLS=(code-reviewer best-practices feature-forge evaluation
                     python-pro sql-pro pandas-pro
                     d3-visualization data-report verification-before-completion) ;;
  security)  SKILLS=(security-reviewer secure-code-guardian fullstack-guardian
                     best-practices code-reviewer architecture-designer
                     chaos-engineer devops-engineer verification-before-completion) ;;
  architect) SKILLS=(architecture-designer api-designer microservices-architect
                     cloud-architect graphql-architect
                     code-reviewer security-reviewer
                     feature-forge executing-plans evaluation verification-before-completion) ;;
  content)   SKILLS=(copywriting copy-editing cold-email emails seo
                     code-reviewer verification-before-completion) ;;
  optimize)  SKILLS=(context-engineering multi-agent-patterns launch-sub-agent do-in-parallel
                     memorize decay reset write-concisely
                     apply-anthropic-skill-best-practices prompt-engineering test-prompt
                     setup-codemap-cli setup-serena-mcp
                     prompt-engineer output-skill graphify) ;;
esac

# Skills included in every role (token optimization / context engineering)
BASE=(context-engineering write-concisely prompt-engineer multi-agent-patterns)

# Skills sourced from a repo other than the default
source_repo() {
    case "$1" in
        context-engineering|multi-agent-patterns|launch-sub-agent|do-in-parallel|\
        memorize|decay|reset|write-concisely|apply-anthropic-skill-best-practices|\
        prompt-engineering|test-prompt|setup-codemap-cli|setup-serena-mcp)
            echo "NeoLabHQ/context-engineering-kit/master" ;;
        *) echo "hosseinmirzapur/opencode-skills/main" ;;
    esac
}

ALL_SKILLS=($(printf "%s\n" "${SKILLS[@]}" "${BASE[@]}" "${EXTRAS[@]}" | awk '!seen[$0]++'))

for skill in "${ALL_SKILLS[@]}"; do
    src=$(source_repo "$skill")
    mkdir -p "$SKILLS_DIR/$skill"
    curl -sL "https://raw.githubusercontent.com/$src/skills/$skill/SKILL.md" \
        -o "$SKILLS_DIR/$skill/SKILL.md"
done
```

---

#### Gemini CLI

**Personal (all projects):**
```bash
mkdir -p ~/.agents/skills
```

**Project (shared via git):**
```bash
mkdir -p .agents/skills
```

**Install skills (bash):**
```bash
# STEP 1: Pick your role (uncomment ONE)
ROLE="fullstack"
# Options: fullstack, frontend, backend, devops, mobile, data, security, architect, content, optimize

# STEP 2: Add extra skills you want (optional)
EXTRAS=()
# EXTRAS=("python-pro" "vue-expert" "d3-visualization")

SKILLS_DIR="$HOME/.agents/skills"  # or ".agents/skills" for project-local

# Checklist-Design
git clone https://github.com/Checklist-Design/skills.git /tmp/checklist-skills
cp -r /tmp/checklist-skills/skills/checklist-design "$SKILLS_DIR/"

# Role-to-skills mapping
case $ROLE in
  fullstack) SKILLS=(code-reviewer security-reviewer best-practices fullstack-guardian
                     feature-forge executing-plans brainstorming evaluation
                     architecture-designer api-designer test-master debugging-wizard
                     devops-engineer database-optimizer react-expert typescript-pro
                     copywriting cli-developer design-review verification-before-completion) ;;
  frontend)  SKILLS=(checklist-design design-review apple-hig color-expert shadcn-ui
                     frontend-design ui-ux-pro-max web-design-guidelines
                     code-reviewer best-practices feature-forge brainstorming
                     evaluation react-expert typescript-pro verification-before-completion) ;;
  backend)   SKILLS=(code-reviewer security-reviewer best-practices fullstack-guardian
                     feature-forge executing-plans evaluation
                     architecture-designer api-designer test-master debugging-wizard
                     devops-engineer database-optimizer sql-pro verification-before-completion) ;;
  devops)    SKILLS=(devops-engineer database-optimizer chaos-engineer
                     kubernetes-specialist monitoring-expert sre-engineer
                     terraform-engineer postgres-pro redis-core
                     code-reviewer best-practices feature-forge verification-before-completion) ;;
  mobile)    SKILLS=(code-reviewer security-reviewer best-practices
                     feature-forge executing-plans brainstorming
                     test-master debugging-wizard
                     react-native-expert flutter-expert typescript-pro verification-before-completion) ;;
  data)      SKILLS=(code-reviewer best-practices feature-forge evaluation
                     python-pro sql-pro pandas-pro
                     d3-visualization data-report verification-before-completion) ;;
  security)  SKILLS=(security-reviewer secure-code-guardian fullstack-guardian
                     best-practices code-reviewer architecture-designer
                     chaos-engineer devops-engineer verification-before-completion) ;;
  architect) SKILLS=(architecture-designer api-designer microservices-architect
                     cloud-architect graphql-architect
                     code-reviewer security-reviewer
                     feature-forge executing-plans evaluation verification-before-completion) ;;
  content)   SKILLS=(copywriting copy-editing cold-email emails seo
                     code-reviewer verification-before-completion) ;;
  optimize)  SKILLS=(context-engineering multi-agent-patterns launch-sub-agent do-in-parallel
                     memorize decay reset write-concisely
                     apply-anthropic-skill-best-practices prompt-engineering test-prompt
                     setup-codemap-cli setup-serena-mcp
                     prompt-engineer output-skill graphify) ;;
esac

# Skills included in every role (token optimization / context engineering)
BASE=(context-engineering write-concisely prompt-engineer multi-agent-patterns)

# Skills sourced from a repo other than the default
source_repo() {
    case "$1" in
        context-engineering|multi-agent-patterns|launch-sub-agent|do-in-parallel|\
        memorize|decay|reset|write-concisely|apply-anthropic-skill-best-practices|\
        prompt-engineering|test-prompt|setup-codemap-cli|setup-serena-mcp)
            echo "NeoLabHQ/context-engineering-kit/master" ;;
        *) echo "hosseinmirzapur/opencode-skills/main" ;;
    esac
}

ALL_SKILLS=($(printf "%s\n" "${SKILLS[@]}" "${BASE[@]}" "${EXTRAS[@]}" | awk '!seen[$0]++'))

for skill in "${ALL_SKILLS[@]}"; do
    src=$(source_repo "$skill")
    mkdir -p "$SKILLS_DIR/$skill"
    curl -sL "https://raw.githubusercontent.com/$src/skills/$skill/SKILL.md" \
        -o "$SKILLS_DIR/$skill/SKILL.md"
done
```

---

## Directory Structure

Skills are installed in your agent's directory. The internal structure is the same regardless of agent:

```
<skills-root>/
├── checklist-design/
│   ├── SKILL.md
│   └── references/
│       ├── index.md
│       ├── audit.md
│       ├── critique.md
│       └── checklists/ (129 files)
├── code-reviewer/
│   ├── SKILL.md
│   └── references/
│       ├── common-issues.md
│       ├── feedback-examples.md
│       ├── receiving-feedback.md
│       ├── report-template.md
│       ├── review-checklist.md
│       └── spec-compliance-review.md
├── security-reviewer/
│   ├── SKILL.md
│   └── references/
├── best-practices/
│   └── SKILL.md
├── fullstack-guardian/
│   ├── SKILL.md
│   └── references/
├── feature-forge/
│   ├── SKILL.md
│   └── references/
├── architecture-designer/
│   ├── SKILL.md
│   └── references/
├── api-designer/
│   ├── SKILL.md
│   └── references/
├── test-master/
│   ├── SKILL.md
│   └── references/
├── debugging-wizard/
│   ├── SKILL.md
│   └── references/
├── devops-engineer/
│   ├── SKILL.md
│   └── references/
├── database-optimizer/
│   ├── SKILL.md
│   └── references/
├── chaos-engineer/
│   ├── SKILL.md
│   └── references/
├── react-expert/
│   ├── SKILL.md
│   └── references/
├── typescript-pro/
│   ├── SKILL.md
│   └── references/
├── copywriting/
│   ├── SKILL.md
│   └── references/
├── cli-developer/
│   ├── SKILL.md
│   └── references/
├── design-review/
│   └── SKILL.md
├── executing-plans/
│   └── SKILL.md
├── brainstorming/
│   └── SKILL.md
└── evaluation/
    └── SKILL.md
```

**Where `<skills-root>` is** (per agent):

| Agent | Personal `<skills-root>` | Project `<skills-root>` |
|-------|-------------------------|------------------------|
| OpenCode | `~/.config/opencode/skills/` | — |
| Claude Code | `~/.claude/skills/` | `.claude/skills/` |
| Cursor | `~/.cursor/skills/` | `.cursor/skills/` |
| Codex | `~/.agents/skills/` | `.agents/skills/` |
| Windsurf | — | `.agents/skills/` |
| GitHub Copilot | `~/.copilot/skills/` | `.github/skills/` or `.agents/skills/` |
| Gemini CLI | `~/.agents/skills/` | `.agents/skills/` |

## Usage

### Automatic Skill Loading

All supported agents automatically discover and load skills based on context. When you ask a question or give a task, the agent will:
1. Match your request against skill `description` fields
2. Load the relevant `SKILL.md` file
3. Follow the skill's workflow and constraints

### Manual Skill Loading

You can explicitly invoke a skill by name. The invocation syntax varies by agent:

| Agent | Invocation |
|-------|-----------|
| Claude Code | `/skill-name` or "use the X skill" |
| Cursor | `/skill-name` or `@skill-name` |
| Codex | Auto-discover or describe the task |
| OpenCode | Auto-discover or "use the X skill" |
| Windsurf | `/skill-name` |
| GitHub Copilot | Auto-discover or describe the task |
| Gemini CLI | Auto-discover or describe the task |

### Skill Examples

#### Code Review
```
Review this pull request for security vulnerabilities and code quality issues
```
→ Agent loads `code-reviewer` skill

#### Architecture Design
```
Design a microservices architecture for an e-commerce platform
```
→ Agent loads `architecture-designer` skill

#### Debugging
```
Help me debug this memory leak in my Node.js application
```
→ Agent loads `debugging-wizard` skill

#### UI/UX Review
```
Audit this landing page against the Website Landing Page checklist
```
→ Agent loads `checklist-design` skill

## If Your Agent is Claude Code

Claude Code uses `CLAUDE.md` as its project instruction file and has its own skills and rules system. This section covers Claude-specific setup.

### CLAUDE.md Setup

Create a `CLAUDE.md` at your project root (or `~/.claude/CLAUDE.md` for global personal preferences):

```markdown
# Project Instructions

## Stack
- TypeScript 5.x, React 19, Next.js 15
- PostgreSQL, Prisma ORM
- Vitest for testing, Playwright for E2E

## Build & Test
- `npm run build` — production build
- `npm run test` — unit tests (Vitest)
- `npm run test:e2e` — end-to-end tests (Playwright)
- `npm run lint` — ESLint + Prettier

## Architecture
- App Router (Next.js 15), not Pages Router
- Server Components by default, 'use client' only when needed
- API routes in app/api/[resource]/route.ts
- Shared utilities in lib/

## Conventions
- Named exports, not default exports (except React components)
- kebab-case for files, PascalCase for components and types
- No `any` — use `unknown` and narrow with type guards
- Prefer early returns over nested ifs

## Banned Patterns
- Do not use `console.log` in production code — use the logger at lib/logger.ts
- Do not modify existing tests to make new code pass
- Do not add dependencies without discussing first
```

### AGENTS.md Template

If your team uses multiple AI tools (Cursor, Codex, Copilot, etc.), create an `AGENTS.md` at the project root as a shared instruction file. Then have Claude Code import it.

**`AGENTS.md`** (shared across all agents):
```markdown
# Project Conventions

## Overview
This is a [project type] built with [main technologies].

## Build & Test
- `npm run build` — production build
- `npm run test` — run all tests
- `npm run lint` — lint and format check

## Code Style
- Use TypeScript strict mode
- Named exports preferred
- kebab-case for files, PascalCase for types/components
- No `any` types

## Architecture
- [Key architectural decisions]
- [Directory structure conventions]
- [Import patterns]

## Security
- Never hardcode secrets
- Validate all user input
- Use parameterized queries

## Git
- Conventional commits: feat:, fix:, chore:, refactor:
- One logical change per commit
- Run tests before pushing
```

**`CLAUDE.md`** (imports the shared file):
```markdown
@AGENTS.md

# Claude Code Specific

## Tool Usage
- Use the code-reviewer skill for PR reviews
- Use the architecture-designer skill for system design tasks
- Use test-master when writing or reviewing tests

## Error Handling
- Always set onError to "continueRegularOutput" for non-critical nodes
- Use retryOnFail for flaky external API calls
```

The `@AGENTS.md` import on line 1 makes Claude Code load your shared instructions. The sections below it are Claude Code-specific additions.

### Claude Code Rules

For path-specific conventions, use `.claude/rules/`:

```bash
mkdir -p .claude/rules
```

Create rule files with `paths` frontmatter to scope them:

```markdown
---
paths:
  - "src/api/**/*.ts"
  - "app/api/**/*.ts"
---
# API Conventions
- Use Hono or native Next.js route handlers
- Validate request body with Zod
- Return structured JSON: { data, error, meta }
- Use HTTP status codes correctly (201 for creation, 204 for deletion)
```

### Claude Code Skills Location

Claude Code reads skills from:
- `~/.claude/skills/` (personal, all projects)
- `.claude/skills/` (project, shared via git)
- `.claude/skills/` in subdirectories (scoped to that directory)

Skills installed via the Installation section above are automatically available.

## Cross-Tool Compatibility

### Portable Fields (work everywhere)

These `SKILL.md` frontmatter fields are part of the Agent Skills standard and work across all compatible agents:

| Field | Purpose |
|-------|---------|
| `name` | Skill identifier (lowercase, hyphens, max 64 chars) |
| `description` | What the skill does and when to use it (max 1024 chars) |
| `license` | License name or reference |
| `metadata` | Arbitrary key-value pairs for additional info |
| `compatibility` | Environment requirements |

### Agent-Specific Fields

These fields are recognized by specific agents only. They are ignored by agents that don't support them (no errors, just no effect):

| Field | Agent | Purpose |
|-------|-------|---------|
| `allowed-tools` | Claude Code | Pre-approved tools for the skill |
| `context` | Claude Code | Set to `fork` to run in isolated subagent |
| `disable-model-invocation` | Claude Code | Prevent auto-loading (manual only) |
| `user-invocable` | Claude Code | Hide from `/` menu |
| `model` | Claude Code | Override model while skill is active |

### Recommendation

For maximum portability across agents, stick to the **portable fields** (`name`, `description`, `license`, `metadata`, `compatibility`) in your custom skills. Agent-specific fields are safe to use but only take effect in their respective agents.

## Avoiding AI Writing Tells

When creating or editing skill content, avoid patterns that mark text as AI-generated. AI writing tells reduce credibility and make skills feel generic rather than expert-written.

### Why This Matters

Readers (human and AI) dismiss text that feels generated. A skill written like a blog post template loses authority. The goal is writing that sounds like it came from someone who has actually used these tools, not someone who prompted an AI to describe them.

### Banned Words and Phrases

These words appear 3-12x more often in AI text than human text. Replace them:

| AI Word | Use Instead |
|---------|------------|
| delve | examine, dig into, look at |
| leverage | use, take advantage of |
| utilize | use |
| harness | use, apply |
| robust | reliable, solid, battle-tested |
| seamless | smooth, no downtime |
| comprehensive | complete, thorough |
| holistic | full, end-to-end |
| elevate | improve, raise |
| foster | encourage, support |
| unlock | enable, access |
| navigate | handle, work through |
| landscape | field, ecosystem |
| tapestry | (delete or rephrase entirely) |
| realm | area, domain |
| moreover | also, plus, and |
| furthermore | also, and |
| transformative | major, significant |
| cutting-edge | modern, current, latest |
| game-changer | major improvement, big shift |

### Filler Phrases to Cut

These add no meaning. Delete them:

- "It is important to note that..."
- "In today's fast-paced world..."
- "When it comes to..."
- "Navigating the complexities of..."
- "A testament to..."
- "It goes without saying that..."
- "I hope this helps!"
- "Great question!"
- "Certainly! Here is..."
- "I would be happy to help..."
- "Let us dive in..."
- "Without further ado..."

### Structural Rules

AI text has predictable rhythm. Break it:

- **Vary sentence length.** Mix 5-word sentences with 25-word sentences. If every sentence lands between 15-25 words, you sound generated.
- **No symmetric two-clause hooks.** Avoid "Most people think X. The reality is Y." more than once per document.
- **No rule-of-three abuse.** "Faster, smarter, and better" is a cliché. Use two items or four. Three in a row reads as AI formatting.
- **No preview paragraphs.** Do not write "In this section, we will explore X, look at Y, and conclude with Z." Just start.
- **No "In conclusion" endings.** End with a specific point, not a summary paragraph.
- **No parallel sentence pairs on repeat.** If you write two sentences that mirror each other's structure, the next pair must break the pattern.

### Punctuation Rules

- **Em dashes:** Max 1 per 100 words. Use commas, periods, or parentheses instead.
- **Curly quotes:** Use straight quotes (`'` and `"`) in technical writing. Curly quotes are a font-level AI signal.
- **Semicolons:** Max 1 per 200 words. Most semicolons can become periods or commas.
- **Emoji bullets:** Do not use emoji as bullet markers. Use `-` or `*`.

### Required Human Elements

AI text lacks personality. Add these on purpose:

- **Use first person.** "I recommend" or "We use" instead of "It is recommended."
- **Include one specific detail.** A version number, a date, a file path, a real error message. Something that proves you touched the code.
- **Admit uncertainty.** "I am not sure about X" or "This might not work in Y case" makes text human.
- **State an opinion.** "X is better than Y for this" without hedging. AI hedges everything.
- **Reference a real failure.** "This broke in production when Z" is more credible than "this can potentially cause issues."

### Self-Review Checklist

Before publishing skill content, scan for these:

- [ ] No more than 1 em dash per 100 words
- [ ] Zero banned words from the table above
- [ ] Zero filler phrases from the list above
- [ ] Sentence lengths vary (some under 10 words, some over 20)
- [ ] At least one specific detail (version, path, date, or error message)
- [ ] At least one first-person statement
- [ ] No symmetric two-clause hooks repeated more than once
- [ ] No rule-of-three patterns
- [ ] No preview paragraphs or "In conclusion" endings
- [ ] Reads like it was written by someone who used the tools, not someone who read about them

## Benefits

1. **Consistent Quality**: Skills enforce best practices across all projects
2. **Faster Onboarding**: New team members get expert guidance automatically
3. **Security Focus**: Security skills catch vulnerabilities early
4. **Comprehensive Coverage**: From design to deployment, all aspects covered
5. **Knowledge Sharing**: Skills document institutional knowledge
6. **Cross-Agent Portability**: Same skills work in Claude Code, Cursor, Codex, and more

## Troubleshooting

### Skills Not Loading

**OpenCode:**
1. Verify skills are in `~/.config/opencode/skills/`
2. Check SKILL.md files have valid YAML frontmatter
3. Restart OpenCode CLI

**Claude Code:**
1. Run `/context` and check the list under "Skills"
2. Verify skills are in `~/.claude/skills/` or `.claude/skills/`
3. Check SKILL.md files have valid YAML frontmatter
4. Restart Claude Code session

**Cursor:**
1. Type `/` in chat and check if skills appear in the menu
2. Verify skills are in `~/.cursor/skills/` or `.cursor/skills/`
3. Cursor also reads `.claude/skills/` and `.codex/skills/` — check those too
4. Restart Cursor

**Codex:**
1. Ask Codex: "What skills are available?"
2. Verify skills are in `~/.agents/skills/` or `.agents/skills/`
3. Restart Codex session

**Windsurf:**
1. Verify skills are in `.agents/skills/` at project root
2. Windsurf reads `.claude/skills/` for compatibility — check there too
3. Restart Windsurf

**GitHub Copilot:**
1. Run `/instructions` in the CLI to check loaded instruction files
2. Verify skills are in `~/.copilot/skills/`, `.github/skills/`, or `.agents/skills/`
3. Restart your IDE or CLI session

**Gemini CLI:**
1. Verify skills are in `~/.agents/skills/` or `.agents/skills/`
2. Restart Gemini CLI session

### References Not Found
1. Ensure `references/` directory exists alongside `SKILL.md`
2. Check file paths in `SKILL.md` are correct (use relative paths)
3. Verify reference files are downloaded

### Permission Issues
1. Check file permissions on the skills directory
2. Ensure your agent has read access to the skills directory
3. On Windows, check PowerShell execution policy if scripts are involved

### Conflicting Skills Across Agents
If you use multiple agents in the same project:
1. Install skills in `.agents/skills/` (the universal location). All agents will find them
2. Avoid duplicating skills across agent-specific directories
3. Keep one canonical copy; let each agent read from the shared location

## Additional Skills

The Skills Catalog above lists all skills included in the role packages. It draws from two upstream repos:

- **hosseinmirzapur/opencode-skills** (322+ skills): https://github.com/hosseinmirzapur/opencode-skills/tree/main/skills
- **NeoLabHQ/context-engineering-kit** (context engineering and token optimization): https://github.com/NeoLabHQ/context-engineering-kit/tree/master/skills

### Adding Skills Not in Your Role

Use the `$extras` array (PowerShell) or `EXTRAS` (bash) in the install script to add any skill by name:

```powershell
# PowerShell (OpenCode)
$extras = @("game-developer", "shopify-expert", "wordpress-pro")
```

```bash
# Bash (all other agents)
EXTRAS=("game-developer" "shopify-expert" "wordpress-pro")
```

### Popular Picks by Category

| Category | Skills Worth Adding |
|----------|-------------------|
| Python | `python-pro`, `django-expert`, `fastapi-expert`, `pandas-pro` |
| JavaScript/TS | `javascript-pro`, `vue-expert`, `angular-architect`, `nextjs-developer`, `nestjs-expert` |
| Mobile | `flutter-expert`, `react-native-expert`, `swift-expert`, `kotlin-specialist` |
| Go/Rust | `golang-pro`, `rust-engineer` |
| Java/JVM | `java-architect`, `kotlin-specialist`, `spring-boot-engineer` |
| PHP | `php-pro`, `laravel-specialist`, `wordpress-pro` |
| .NET | `csharp-developer`, `dotnet-core-expert` |
| Infrastructure | `kubernetes-specialist`, `terraform-engineer`, `sre-engineer`, `monitoring-expert` |
| Data | `python-pro`, `sql-pro`, `pandas-pro`, `d3-visualization`, `ml-pipeline` |
| Design | `frontend-design`, `shadcn-ui`, `ui-ux-pro-max`, `color-expert` |
| Token optimization | `context-engineering`, `setup-serena-mcp`, `memorize`, `write-concisely` |

## Keeping the Catalog Updated

**Agent instructions:** If you are an agent running this guide, run this section before acting on the catalog. It detects skills added to the upstream repo since the last sync, classifies them, and updates the tables. This makes the guide self-updating.

### Step 1: Detect New Skills

There are two checks. The first finds skills that were **added upstream since the last sync** (the `Catalog Synced` date at the top of the Skills Catalog). The second finds catalog entries that were **removed or renamed**.

#### 1a. New skills since last sync

Set `SINCE` to the `Catalog Synced` date at the top of the Skills Catalog section. This checks every upstream repo the catalog pulls from.

**PowerShell (Windows):**
```powershell
$since = "2026-09-11T00:00:00Z"   # <- set to the Catalog Synced date
$repos = @("hosseinmirzapur/opencode-skills", "NeoLabHQ/context-engineering-kit")
$added = @()

foreach ($repo in $repos) {
    $commits = Invoke-RestMethod "https://api.github.com/repos/$repo/commits?path=skills&since=$since&per_page=100"
    foreach ($c in $commits) {
        $detail = Invoke-RestMethod "https://api.github.com/repos/$repo/commits/$($c.sha)"
        $added += $detail.files |
            Where-Object { $_.status -eq 'added' -and $_.filename -match '^skills/[^/]+/SKILL\.md$' } |
            ForEach-Object { "$repo  ->  " + ($_.filename -split '/')[1] }
    }
}
$added = $added | Sort-Object -Unique
Write-Host "Skills added since $since ($($added.Count)):"
$added
```

**Bash (macOS/Linux):**
```bash
SINCE="2026-09-11T00:00:00Z"   # <- set to the Catalog Synced date
REPOS=("hosseinmirzapur/opencode-skills" "NeoLabHQ/context-engineering-kit")

for REPO in "${REPOS[@]}"; do
    echo "### $REPO"
    curl -sL "https://api.github.com/repos/$REPO/commits?path=skills&since=$SINCE&per_page=100" \
        | grep -oE '"sha": "[a-f0-9]{40}"' | sed -E 's/.*"sha": "([a-f0-9]+)".*/\1/' | sort -u | while read sha; do
            curl -sL "https://api.github.com/repos/$REPO/commits/$sha" \
                | grep -oE '"filename": "skills/[^/]+/SKILL.md"' | sed -E 's|.*skills/([^/]+)/SKILL.md.*|\1|'
        done | sort -u
done
```

#### 1b. Catalog entries removed or renamed upstream

**PowerShell (Windows):**
```powershell
# All live skills across both upstream repos
$repos = @(
    @{ name = "hosseinmirzapur/opencode-skills";  branch = "main" },
    @{ name = "NeoLabHQ/context-engineering-kit"; branch = "master" }
)
$live = @()
foreach ($r in $repos) {
    $tree = Invoke-RestMethod "https://api.github.com/repos/$($r.name)/git/trees/$($r.branch)?recursive=1"
    $live += $tree.tree |
        Where-Object { $_.path -match '^skills/[^/]+/SKILL\.md$' } |
        ForEach-Object { ($_.path -split '/')[1] }
}
$live = $live | Sort-Object -Unique

# Skills already listed in this guide's catalog
$doc = Get-Content "AI_AGENT_SKILLS_IMPLEMENTATION.md" -Raw
$section = [regex]::Match($doc, '(?s)## Skills Catalog.*?(?=\n## )').Value
$catalog = [regex]::Matches($section, '(?m)^\| ([a-z0-9][a-z0-9-]*) \|') |
    ForEach-Object { $_.Groups[1].Value } |
    Sort-Object -Unique

# checklist-design comes from a third repo, so it is expected to be listed here
$removed = $catalog | Where-Object { $_ -notin $live -and $_ -ne 'checklist-design' }
Write-Host "Catalog entries no longer upstream ($($removed.Count)):"
$removed
```

**Bash (macOS/Linux):**
```bash
LIVE=$(
  curl -sL "https://api.github.com/repos/hosseinmirzapur/opencode-skills/git/trees/main?recursive=1" \
    | grep -oE '"path": "skills/[^/]+/SKILL.md"' | sed -E 's|.*skills/([^/]+)/SKILL.md.*|\1|'
  curl -sL "https://api.github.com/repos/NeoLabHQ/context-engineering-kit/git/trees/master?recursive=1" \
    | grep -oE '"path": "skills/[^/]+/SKILL.md"' | sed -E 's|.*skills/([^/]+)/SKILL.md.*|\1|'
)
LIVE=$(echo "$LIVE" | sort -u)

CATALOG=$(awk '/^## Skills Catalog/{f=1} f&&/^## /&&!/^## Skills Catalog/{exit} f' \
    AI_AGENT_SKILLS_IMPLEMENTATION.md \
    | grep -oE '^\| [a-z0-9][a-z0-9-]* ' | sed -E 's/^\| ([a-z0-9-]+) .*/\1/' | sort -u \
    | grep -v '^checklist-design$')

echo "Catalog entries no longer upstream:"
comm -13 <(echo "$LIVE") <(echo "$CATALOG")
```

If both checks come back empty, the catalog is current. Stop here.

> **Why commit-date detection:** the live-minus-catalog diff would also report the ~200 upstream skills that were deliberately left out of this curated catalog. Commit-date detection only reports what actually changed since the last sync.


### Step 2: Fetch Details for New Skills

For each new skill, read its `name` and `description` from the upstream `SKILL.md` frontmatter:

```bash
# Replace SKILL_NAME with each new skill from Step 1
curl -sL "https://raw.githubusercontent.com/hosseinmirzapur/opencode-skills/main/skills/SKILL_NAME/SKILL.md" \
    | sed -n '1,15p'
```

The first block is YAML frontmatter. Extract the `description:` value. This becomes the "Purpose" column. Trim it to one short phrase.

### Step 3: Classify Each New Skill

Match the skill name and description against these categories. Pick the first category whose keywords appear.

| Category | Match Keywords |
|----------|---------------|
| Design & UI/UX | design, ui, ux, figma, color, shadcn, frontend-design, css, layout, wireframe |
| Code Quality & Security | review, security, lint, audit, vulnerability, secure, guardian, code-smell |
| Development Workflow | plan, brainstorming, onboarding, workflow, tdd, test-driven, git, branch, review-feedback |
| Architecture & Design | architect, api, graphql, microservice, cloud, system-design, schema |
| Testing & Quality | test, debug, playwright, verification, qa, coverage |
| Infrastructure & DevOps | devops, kubernetes, terraform, docker, ci, cd, monitoring, sre, redis, postgres, sql, spark, database |
| Language & Frameworks | (language or framework name: python, javascript, typescript, vue, angular, react, next, nest, django, fastapi, laravel, rails, spring, golang, go, rust, java, kotlin, swift, php, csharp, cpp, dotnet, flutter, dart, wordpress, shopify) |
| Content & Marketing | copy, seo, email, marketing, content, blog, social, ads, cold-email |
| AI & Machine Learning | ml, ai, fine-tun, rag, prompt, llm, model, embedding, vector |
| Data & Visualization | data, pandas, visualization, chart, d3, report, analytics, etl |
| Token Optimization & Context Engineering | token, context, prompt, compress, compact, budget, window, subagent, memory, retrieval, cache, concis |
| CLI & Tools | cli, command, mcp, tool, terminal, shell |
| Game Development | game, unity, godot, unreal, shader, 3d |

If no category fits, add a new one at the end of the catalog.

### Step 4: Assign Packages

Add the new skill to role packages based on its category:

| Category | Default Packages |
|----------|-----------------|
| Design & UI/UX | frontend |
| Code Quality & Security | all |
| Development Workflow | all |
| Architecture & Design | fullstack, backend, architect |
| Testing & Quality | fullstack, backend |
| Infrastructure & DevOps | devops |
| Language & Frameworks | backend (or frontend, mobile, data, per language) |
| Content & Marketing | content |
| AI & Machine Learning | data |
| Data & Visualization | data |
| Token Optimization & Context Engineering | optimize (base: context-engineering, write-concisely, prompt-engineer, multi-agent-patterns) |
| CLI & Tools | fullstack, backend |
| Game Development | (standalone) |

Also add the skill to the matching role array inside the install scripts (the `$roleSkills` hashtable for PowerShell, the `case` blocks for bash).

### Step 5: Update the Catalog

1. Insert each new skill as a row in its category table: `| skill-name | purpose | packages |`
2. Update the sync marker at the top of the Skills Catalog section: set `Last synced` to today's date and bump `Tracked` to the new count.
3. Update the version block at the bottom of this document (bump the minor version, update the date).
4. Remove any rows reported as "no longer upstream" in Step 1.

### Step 6: Verify

Re-run Step 1. Both drift lists should be empty.

> **Note for non-agent runs:** These steps are written for an AI agent reading this guide. A human can run the same scripts, then manually classify and paste the rows.

## Contributing

To create custom skills for your team:

1. Create a directory: `<skills-root>/<skill-name>/`
2. Create `SKILL.md` with YAML frontmatter following the Agent Skills standard:
   ```yaml
   ---
   name: skill-name
   description: What this skill does and when to use it
   license: MIT
   metadata:
     author: Your Name
     version: "1.0.0"
   ---
   ```
3. Add a `references/` directory if the skill needs supporting documentation
4. Add a `scripts/` directory if the skill includes executable code
5. Test the skill loads correctly in your agent

### SKILL.md Best Practices
- Keep `description` specific — include keywords that help agents match tasks to skills
- Keep the `SKILL.md` body under 500 lines — move details to `references/`
- Use progressive disclosure: metadata → body → referenced files
- Stick to portable frontmatter fields for cross-agent compatibility

## Resources

### Agent Skills Standard
- Specification: https://agentskills.io/specification
- GitHub: https://github.com/agentskills/agentskills
- Example Skills: https://github.com/anthropics/skills

### Agent Documentation
- OpenCode Skills: https://opencode.ai/docs/skills/
- Claude Code Skills: https://code.claude.com/docs/en/skills
- Claude Code CLAUDE.md: https://code.claude.com/docs/en/memory
- Cursor Skills: https://cursor.com/help/customization/skills
- Cursor Rules: https://cursor.com/docs/rules
- Codex AGENTS.md: https://developers.openai.com/codex/guides/agents-md
- Windsurf Rules: https://cursor.com/help/customization/rules.md
- GitHub Copilot Instructions: https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/add-custom-instructions/add-repository-instructions

### Skill Sources
- Checklist-Design Skills: https://github.com/Checklist-Design/skills
- OpenCode Skills Collection: https://github.com/hosseinmirzapur/opencode-skills
- Context Engineering Kit: https://github.com/NeoLabHQ/context-engineering-kit

## Support

For issues or questions:
1. Check your agent's documentation (see Resources above)
2. Review skill `SKILL.md` files for usage instructions
3. Open issue in the relevant skill repository
4. Visit the Agent Skills Discord: https://discord.gg/MKPE9g8aUy

---

**Last Updated**: September 11, 2026
**Version**: 4.0.0
**Author**: Ricardo Moses
**Catalog Synced**: 2026-09-11 (114 skills tracked)
**Self-Update**: Run the "Keeping the Catalog Updated" section to pull new upstream skills
