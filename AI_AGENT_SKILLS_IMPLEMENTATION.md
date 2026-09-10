# AI Agent Skills Implementation Guide

## Overview

This document describes the implementation of a comprehensive skill library following the [Agent Skills standard](https://agentskills.io), an open format installed globally across all projects. The skills enhance any compatible AI coding agent's ability to research, plan, and execute developer tasks with specialized knowledge.

This guide works with **OpenCode, Claude Code, Cursor, Codex, Windsurf, GitHub Copilot, Gemini CLI**, and any Agent Skills-compatible agent. The document itself is self-adapting: follow the Agent Detection section to find your agent's paths and commands.

## Goals

1. **Global Installation**: Skills installed in your agent's personal directory are available across all projects
2. **Comprehensive Coverage**: 22+ skills covering design, code quality, security, architecture, testing, DevOps, and more
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

## Skills Installed

### Design & UI/UX
| Skill | Purpose | Source |
|-------|---------|--------|
| checklist-design | 129 UI/UX checklists for web apps, mobile, design systems | Checklist-Design/skills |
| design-review | Visual audit with before/after screenshots | hosseinmirzapur/opencode-skills |

### Code Quality & Security
| Skill | Purpose | Source |
|-------|---------|--------|
| code-reviewer | PR reviews, security vulnerabilities, code smells | hosseinmirzapur/opencode-skills |
| security-reviewer | Vulnerability scanning, SAST, penetration testing | hosseinmirzapur/opencode-skills |
| best-practices | Security (CSP, SRI, Trusted Types), browser compatibility | hosseinmirzapur/opencode-skills |
| fullstack-guardian | Security-focused full-stack implementation | hosseinmirzapur/opencode-skills |

### Development Workflow
| Skill | Purpose | Source |
|-------|---------|--------|
| feature-forge | Requirements workshops, user stories, EARS specs | hosseinmirzapur/opencode-skills |
| executing-plans | Step-by-step plan execution | hosseinmirzapur/opencode-skills |
| brainstorming | Idea generation and exploration | hosseinmirzapur/opencode-skills |
| evaluation | Solution assessment and comparison | hosseinmirzapur/opencode-skills |

### Architecture & Design
| Skill | Purpose | Source |
|-------|---------|--------|
| architecture-designer | System design, ADRs, scalability planning | hosseinmirzapur/opencode-skills |
| api-designer | REST/GraphQL APIs, OpenAPI specs | hosseinmirzapur/opencode-skills |

### Testing & Quality
| Skill | Purpose | Source |
|-------|---------|--------|
| test-master | Unit, integration, E2E, performance testing | hosseinmirzapur/opencode-skills |
| debugging-wizard | Systematic debugging methodology | hosseinmirzapur/opencode-skills |

### Infrastructure & DevOps
| Skill | Purpose | Source |
|-------|---------|--------|
| devops-engineer | CI/CD, Docker, Kubernetes, Terraform | hosseinmirzapur/opencode-skills |
| database-optimizer | Query optimization, index design | hosseinmirzapur/opencode-skills |
| chaos-engineer | Resilience testing, failure injection | hosseinmirzapur/opencode-skills |

### Language-Specific
| Skill | Purpose | Source |
|-------|---------|--------|
| react-expert | React 19, Server Components, hooks | hosseinmirzapur/opencode-skills |
| typescript-pro | Advanced types, type guards, tRPC | hosseinmirzapur/opencode-skills |

### Content & Marketing
| Skill | Purpose | Source |
|-------|---------|--------|
| copywriting | Marketing copy, landing pages, CTAs | hosseinmirzapur/opencode-skills |
| copy-editing | Polishing existing copy | hosseinmirzapur/opencode-skills |

### CLI & Tools
| Skill | Purpose | Source |
|-------|---------|--------|
| cli-developer | CLI tools, argument parsing, completions | hosseinmirzapur/opencode-skills |

## Installation

### Prerequisites
- An AI coding agent installed (see Supported Agents table)
- Git installed
- PowerShell (Windows) or bash (macOS/Linux)

### Agent-Specific Installation

Determine your agent from the Agent Detection section, then follow its instructions:

---

#### OpenCode

**Personal (all projects):**
```bash
mkdir -p ~/.config/opencode/skills
```

**Install Checklist-Design:**
```bash
git clone https://github.com/Checklist-Design/skills.git /tmp/checklist-skills
cp -r /tmp/checklist-skills/skills/checklist-design ~/.config/opencode/skills/
```

**Install additional skills (PowerShell):**
```bash
$skills = @("code-reviewer", "security-reviewer", "best-practices", "fullstack-guardian",
            "feature-forge", "architecture-designer", "api-designer", "test-master",
            "debugging-wizard", "devops-engineer", "database-optimizer", "chaos-engineer",
            "react-expert", "typescript-pro", "copywriting", "cli-developer",
            "design-review", "executing-plans", "brainstorming", "evaluation")

foreach ($skill in $skills) {
    $url = "https://raw.githubusercontent.com/hosseinmirzapur/opencode-skills/main/skills/$skill/SKILL.md"
    $outputDir = "$env:USERPROFILE\.config\opencode\skills\$skill"

    New-Item -ItemType Directory -Force -Path $outputDir | Out-Null
    Invoke-WebRequest -Uri $url -OutFile "$outputDir\SKILL.md"
}
```

**Install references (optional):**
```bash
$skillsWithReferences = @("code-reviewer", "security-reviewer", "fullstack-guardian",
                          "feature-forge", "architecture-designer", "api-designer",
                          "test-master", "debugging-wizard", "devops-engineer",
                          "database-optimizer", "chaos-engineer", "react-expert",
                          "typescript-pro", "cli-developer")

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
SKILLS_DIR="$HOME/.claude/skills"  # or ".claude/skills" for project-local

# Checklist-Design
git clone https://github.com/Checklist-Design/skills.git /tmp/checklist-skills
cp -r /tmp/checklist-skills/skills/checklist-design "$SKILLS_DIR/"

# Additional skills
SKILLS=("code-reviewer" "security-reviewer" "best-practices" "fullstack-guardian"
        "feature-forge" "architecture-designer" "api-designer" "test-master"
        "debugging-wizard" "devops-engineer" "database-optimizer" "chaos-engineer"
        "react-expert" "typescript-pro" "copywriting" "cli-developer"
        "design-review" "executing-plans" "brainstorming" "evaluation")

for skill in "${SKILLS[@]}"; do
    mkdir -p "$SKILLS_DIR/$skill"
    curl -sL "https://raw.githubusercontent.com/hosseinmirzapur/opencode-skills/main/skills/$skill/SKILL.md" \
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
SKILLS_DIR="$HOME/.cursor/skills"  # or ".cursor/skills" for project-local

SKILLS=("code-reviewer" "security-reviewer" "best-practices" "fullstack-guardian"
        "feature-forge" "architecture-designer" "api-designer" "test-master"
        "debugging-wizard" "devops-engineer" "database-optimizer" "chaos-engineer"
        "react-expert" "typescript-pro" "copywriting" "cli-developer"
        "design-review" "executing-plans" "brainstorming" "evaluation")

# Checklist-Design
git clone https://github.com/Checklist-Design/skills.git /tmp/checklist-skills
cp -r /tmp/checklist-skills/skills/checklist-design "$SKILLS_DIR/"

for skill in "${SKILLS[@]}"; do
    mkdir -p "$SKILLS_DIR/$skill"
    curl -sL "https://raw.githubusercontent.com/hosseinmirzapur/opencode-skills/main/skills/$skill/SKILL.md" \
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
SKILLS_DIR="$HOME/.agents/skills"  # or ".agents/skills" for project-local

SKILLS=("code-reviewer" "security-reviewer" "best-practices" "fullstack-guardian"
        "feature-forge" "architecture-designer" "api-designer" "test-master"
        "debugging-wizard" "devops-engineer" "database-optimizer" "chaos-engineer"
        "react-expert" "typescript-pro" "copywriting" "cli-developer"
        "design-review" "executing-plans" "brainstorming" "evaluation")

# Checklist-Design
git clone https://github.com/Checklist-Design/skills.git /tmp/checklist-skills
cp -r /tmp/checklist-skills/skills/checklist-design "$SKILLS_DIR/"

for skill in "${SKILLS[@]}"; do
    mkdir -p "$SKILLS_DIR/$skill"
    curl -sL "https://raw.githubusercontent.com/hosseinmirzapur/opencode-skills/main/skills/$skill/SKILL.md" \
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
SKILLS_DIR=".agents/skills"

SKILLS=("code-reviewer" "security-reviewer" "best-practices" "fullstack-guardian"
        "feature-forge" "architecture-designer" "api-designer" "test-master"
        "debugging-wizard" "devops-engineer" "database-optimizer" "chaos-engineer"
        "react-expert" "typescript-pro" "copywriting" "cli-developer"
        "design-review" "executing-plans" "brainstorming" "evaluation")

# Checklist-Design
git clone https://github.com/Checklist-Design/skills.git /tmp/checklist-skills
cp -r /tmp/checklist-skills/skills/checklist-design "$SKILLS_DIR/"

for skill in "${SKILLS[@]}"; do
    mkdir -p "$SKILLS_DIR/$skill"
    curl -sL "https://raw.githubusercontent.com/hosseinmirzapur/opencode-skills/main/skills/$skill/SKILL.md" \
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
SKILLS_DIR="$HOME/.copilot/skills"  # or ".agents/skills" for project-local

SKILLS=("code-reviewer" "security-reviewer" "best-practices" "fullstack-guardian"
        "feature-forge" "architecture-designer" "api-designer" "test-master"
        "debugging-wizard" "devops-engineer" "database-optimizer" "chaos-engineer"
        "react-expert" "typescript-pro" "copywriting" "cli-developer"
        "design-review" "executing-plans" "brainstorming" "evaluation")

# Checklist-Design
git clone https://github.com/Checklist-Design/skills.git /tmp/checklist-skills
cp -r /tmp/checklist-skills/skills/checklist-design "$SKILLS_DIR/"

for skill in "${SKILLS[@]}"; do
    mkdir -p "$SKILLS_DIR/$skill"
    curl -sL "https://raw.githubusercontent.com/hosseinmirzapur/opencode-skills/main/skills/$skill/SKILL.md" \
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
SKILLS_DIR="$HOME/.agents/skills"  # or ".agents/skills" for project-local

SKILLS=("code-reviewer" "security-reviewer" "best-practices" "fullstack-guardian"
        "feature-forge" "architecture-designer" "api-designer" "test-master"
        "debugging-wizard" "devops-engineer" "database-optimizer" "chaos-engineer"
        "react-expert" "typescript-pro" "copywriting" "cli-developer"
        "design-review" "executing-plans" "brainstorming" "evaluation")

# Checklist-Design
git clone https://github.com/Checklist-Design/skills.git /tmp/checklist-skills
cp -r /tmp/checklist-skills/skills/checklist-design "$SKILLS_DIR/"

for skill in "${SKILLS[@]}"; do
    mkdir -p "$SKILLS_DIR/$skill"
    curl -sL "https://raw.githubusercontent.com/hosseinmirzapur/opencode-skills/main/skills/$skill/SKILL.md" \
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

To add more skills from the hosseinmirzapur/opencode-skills repository (322+ skills available):

1. Browse available skills: https://github.com/hosseinmirzapur/opencode-skills/tree/main/skills
2. Download SKILL.md and references
3. Place in your agent's skills directory under `<skill-name>/`

### Recommended Additional Skills
- **django-expert** — Django best practices
- **fastapi-expert** — FastAPI APIs
- **nestjs-expert** — NestJS APIs
- **spring-boot-engineer** — Spring Boot
- **kubernetes-specialist** — K8s deep dive
- **terraform-engineer** — Terraform IaC
- **sre-engineer** — Site reliability
- **monitoring-expert** — Observability

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

## Support

For issues or questions:
1. Check your agent's documentation (see Resources above)
2. Review skill `SKILL.md` files for usage instructions
3. Open issue in the relevant skill repository
4. Visit the Agent Skills Discord: https://discord.gg/MKPE9g8aUy

---

**Last Updated**: September 10, 2026
**Version**: 2.0.0
**Author**: Ricardo Moses
