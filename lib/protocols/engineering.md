# Engineering Department Protocol

## Department Overview

The Engineering department is responsible for all technical implementation: architecture, frontend, backend, mobile, AI/ML integration, infrastructure, and rapid prototyping.

## Department Lead

**Architect** — Makes final technical decisions for the department, resolves conflicts between engineering roles, and reviews code quality.

## Roles and Responsibilities

| Role | Primary Focus | Worktree | Phase |
|------|--------------|----------|-------|
| architect | System design, contracts, code review | No | INIT, DESIGN, INTEGRATE |
| frontend-developer | Web UI implementation | Yes | DEVELOP |
| backend-developer | API/server implementation | Yes | DEVELOP |
| mobile-app-developer | Mobile app development | Yes | DEVELOP |
| ai-engineer | AI/ML integration | Yes | DEVELOP |
| devops | CI/CD, infrastructure | No | OPTIMIZE, DEPLOY |
| rapid-prototyper | Quick POCs, MVPs | Yes | DEVELOP |

## Development Workflow

All engineering roles that implement code follow this workflow:

```
Read assigned tasks → Read contracts → Read design specs → Implement → Write tests → Run tests → Report progress
```

### Auto-Fix Loop

When tests fail:
1. Analyze failure (error message + stack trace)
2. Identify root cause (your code, dependency, or environment)
3. Fix with minimal change
4. Re-run tests
5. Track retry count in `autoFixRetries`
6. If retries >= maxAutoFixRetries → escalate to architect

### Worktree Rules

- Each developer works in an isolated git worktree
- Never modify files outside your task scope
- Keep commits atomic (one logical change per commit)
- Worktree naming: `full-team-eng-{role-short}-{task-scope}`

## Communication

- **Read from**: `.team/backlog.json`, `.team/reports/contracts.json`, `.team/reports/design-spec.json`, `.team/comms/`
- **Write to**: `.team/state.json` (progress), `.team/comms/` (blockers), `.team/backlog.json` (task status updates)

## Code Quality Standards

- Follow architecture contracts exactly
- Write tests for every feature implemented
- No over-engineering — implement exactly what the task requires
- Follow the testing strategy defined by the architect
- Report blockers via comms/ rather than guessing
