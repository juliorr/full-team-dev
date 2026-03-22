# full-team-dev

Multi-department AI development orchestrator for Claude Code. Coordinates 20 specialized agents across 4 departments through 8 phases — from market research to production deployment.

## Quick Start

```bash
# Basic usage
/full-team-dev --plan docs/plan.md

# Web app with all departments
/full-team-dev --plan docs/plan.md

# Backend-only project
/full-team-dev --plan docs/plan.md --departments engineering,testing

# Specific roles only
/full-team-dev --plan docs/plan.md --roles architect,backend-developer,api-tester

# Skip research for internal tools
/full-team-dev --plan docs/plan.md --skip-phases research

# High autonomy mode
/full-team-dev --plan docs/plan.md --autonomy high-autonomy
```

## Departments & Roles

### Engineering (7 roles)

| Role | Description | Worktree |
|------|------------|----------|
| **architect** | System design, contracts, code review, conflict resolution | No |
| **frontend-developer** | Web UI (React, Vue, Angular, Next.js) | Yes |
| **backend-developer** | API/server (Node.js, Python, Go) | Yes |
| **mobile-app-developer** | Mobile (React Native, Flutter, Swift, Kotlin) | Yes |
| **ai-engineer** | AI/ML integration, LLM, embeddings, RAG | Yes |
| **devops** | CI/CD, Docker, deployment, infrastructure | No |
| **rapid-prototyper** | Quick POCs, MVPs, spike solutions | Yes |

### Product (3 roles)

| Role | Description |
|------|------------|
| **trend-researcher** | Market trends, competitor analysis, technology landscape |
| **feedback-synthesizer** | User feedback analysis, feature request prioritization |
| **sprint-prioritizer** | Sprint planning, MoSCoW prioritization, dependency analysis |

### Design (4 roles)

| Role | Description |
|------|------------|
| **ui-designer** | Design system, component specs, responsive layouts |
| **ux-researcher** | User flows, information architecture, interaction patterns |
| **brand-guardian** | Visual identity, style guide, accessibility compliance |
| **visual-storyteller** | Architecture diagrams, documentation visuals |

### Testing (6 roles)

| Role | Description |
|------|------------|
| **tool-evaluator** | Framework/library evaluation and benchmarking |
| **api-tester** | API testing, contract testing, smoke tests |
| **workflow-optimizer** | CI/CD optimization, build optimization |
| **performance-benchmarker** | Load testing, performance baselines |
| **test-results-analyzer** | Quality dashboard, test aggregation |
| **security-benchmark** | OWASP checks, vulnerability scanning |

## 8 Phases

```
INIT → RESEARCH → DESIGN → DEVELOP → TEST → INTEGRATE → OPTIMIZE → DEPLOY
```

| Phase | Departments Active | Parallel Agents |
|-------|--------------------|----------------|
| **INIT** | — (orchestrator only) | 0 |
| **RESEARCH** | Product + Testing/tool-evaluator | 3 parallel, then 1 sequential |
| **DESIGN** | Engineering/architect + Design | 1 sequential, then 4 parallel |
| **DEVELOP** | Engineering (5 dev roles) | Up to N per role (configurable) |
| **TEST** | Testing (all 6) | 5 parallel, then 1 sequential |
| **INTEGRATE** | Engineering + Testing + Product | 3 sequential |
| **OPTIMIZE** | Testing + Engineering/devops | 3 parallel |
| **DEPLOY** | Engineering/devops + Testing | 3 parallel |

## State Protocol

All agents communicate through `.team/` in the project root:

```
.team/
├── config.json        # Departments, roles, autonomy, retries
├── state.json         # Current phase, agent status, progress
├── backlog.json       # Task list with assignments and dependencies
├── comms/             # Inter-agent messages (JSON files)
├── reports/           # Structured reports from each role
│   ├── research-brief.json
│   ├── feedback-synthesis.json
│   ├── tool-evaluation.json
│   ├── priority-matrix.json
│   ├── architecture-review.json
│   ├── contracts.json
│   ├── design-spec.json
│   ├── brand-guidelines.json
│   ├── ux-flows.json
│   ├── test-results.json
│   ├── security-report.json
│   ├── performance-report.json
│   ├── quality-dashboard.json
│   ├── workflow-optimization.json
│   ├── optimization-report.json
│   └── deployment-status.json
└── artifacts/         # Design artifacts
    ├── design-tokens.json
    └── component-specs/
```

## Autonomy Levels

| Level | Checkpoints |
|-------|------------|
| **semi-autonomous** (default) | Research, design, phase-complete, test, integration, optimization, deploy, conflicts, auto-fix limits |
| **high-autonomy** | Deploy (always), unresolvable blockers |

## Escalation Chain

```
Role → Department Lead → Architect → User
```

| Department | Lead |
|------------|------|
| Engineering | architect |
| Product | sprint-prioritizer |
| Design | ui-designer |
| Testing | test-results-analyzer |

## Arguments

| Argument | Default | Description |
|----------|---------|-------------|
| `--plan` | Auto-detect in `docs/` | Path to project plan or spec |
| `--autonomy` | `semi-autonomous` | Autonomy level |
| `--max-retries` | `3` | Max auto-fix retries |
| `--departments` | All enabled | Departments to activate |
| `--roles` | All enabled | Specific roles to activate |
| `--skip-phases` | None | Phases to skip |

## Configuration

Default role counts in `config.json`:

| Role | Default Count | Default Enabled |
|------|--------------|----------------|
| architect | 1 | Yes |
| frontend-developer | 2 | Yes |
| backend-developer | 2 | Yes |
| mobile-app-developer | 1 | No |
| ai-engineer | 1 | No |
| devops | 1 | Yes |
| rapid-prototyper | 1 | No |
| All product roles | 1 | Yes |
| All design roles | 1 | Yes (except visual-storyteller) |
| All testing roles | 1 | Yes |

Enable/disable roles by modifying `.team/config.json` or using `--roles` flag.
