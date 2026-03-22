# Shared Protocols — Full Team Dev

## Team Communication Protocol

All agents communicate through the `.team/` directory in the project root:

- **State**: Read/write `.team/state.json` to track phase and progress
- **Backlog**: Read `.team/backlog.json` for task assignments
- **Comms**: Write messages to `.team/comms/` as JSON files
- **Reports**: Write reports to `.team/reports/` as JSON files
- **Artifacts**: Write design artifacts to `.team/artifacts/` (design tokens, component specs, etc.)

### Message Format (comms/)

```json
{
  "id": "MSG-{timestamp}-{from}-{to}",
  "from": { "role": "api-tester", "department": "testing" },
  "to": { "role": "backend-developer", "department": "engineering" },
  "type": "test-failure | blocker | escalation | question | info",
  "taskId": "TASK-003",
  "timestamp": "2026-01-15T10:30:00Z",
  "content": {
    "summary": "Brief description of the issue",
    "details": "Full explanation with context",
    "files": ["src/api/users.ts"],
    "testOutput": "..."
  }
}
```

### Report Format (reports/)

```json
{
  "type": "report-type",
  "department": "engineering | product | design | testing",
  "role": "role-name",
  "phase": "research | design | develop | test | integrate | optimize | deploy",
  "timestamp": "2026-01-15T10:30:00Z",
  "summary": {},
  "details": {},
  "recommendations": []
}
```

## Task Format (backlog.json)

```json
{
  "id": "TASK-001",
  "title": "Implement user authentication API",
  "description": "Create REST endpoints for login, register, and token refresh",
  "department": "engineering",
  "assignedRole": "backend-developer",
  "assignedAgent": null,
  "instanceIndex": 0,
  "status": "pending",
  "priority": "critical | high | medium | low",
  "phase": "develop | deploy",
  "dependencies": ["TASK-002"],
  "crossDepartmentDeps": ["TASK-DESIGN-001"],
  "worktree": null,
  "autoFixRetries": 0,
  "files": [],
  "tags": []
}
```

## Task Status Values

| Status | Meaning |
|--------|---------|
| `pending` | Not started |
| `in-progress` | Agent actively working |
| `testing` | Implementation done, tests running |
| `auto-fixing` | Test failed, developer retrying (track retry count) |
| `escalated` | Exceeded retry limit, needs higher-level review |
| `blocked` | Waiting on dependency or external input |
| `review` | Code review by architect or department lead |
| `done` | Completed and verified |

## Escalation Chain

When a problem cannot be resolved at the current level:

```
Role (auto-fix, up to maxAutoFixRetries)
  → Department Lead:
     - Engineering: architect
     - Product: sprint-prioritizer
     - Design: ui-designer
     - Testing: test-results-analyzer
  → architect (final technical authority)
  → User (final decision)
```

Each escalation must include:
1. What was attempted
2. Why it failed
3. Suggested alternatives

## Department Leads

| Department | Lead Role | Responsibilities |
|------------|-----------|-----------------|
| Engineering | architect | Technical decisions, conflict resolution, code review |
| Product | sprint-prioritizer | Priority decisions, requirement clarification |
| Design | ui-designer | Design decisions, visual consistency |
| Testing | test-results-analyzer | Quality decisions, test strategy |

## Stack Detection Patterns

When the project already has code, detect the stack by checking for:

| File | Stack |
|------|-------|
| `package.json` | Node.js / JavaScript / TypeScript |
| `requirements.txt`, `pyproject.toml`, `setup.py` | Python |
| `go.mod` | Go |
| `Cargo.toml` | Rust |
| `pom.xml`, `build.gradle` | Java/Kotlin |
| `Gemfile` | Ruby |
| `composer.json` | PHP |
| `*.csproj`, `*.sln` | .NET/C# |
| `pubspec.yaml` | Dart/Flutter |
| `Podfile` | iOS (CocoaPods) |
| `build.gradle.kts` + `AndroidManifest.xml` | Android (Kotlin) |
| `docker-compose.yml` | Docker (infra) |
| `Dockerfile` | Docker (container) |
| `.github/workflows/` | GitHub Actions CI |
| `openapi.yaml`, `openapi.json` | API spec exists |

## Worktree Naming Convention

When dispatching developers to isolated worktrees:

```
Format: full-team-{department}-{role}-{task-scope}
Example: full-team-eng-backend-api-auth
         full-team-eng-frontend-dashboard
         full-team-eng-mobile-map-screen
         full-team-eng-ai-embeddings
```

## Phase Order

```
INIT → RESEARCH → DESIGN → DEVELOP → TEST → INTEGRATE → OPTIMIZE → DEPLOY
```

## Cross-Department Report Dependencies

Reports are the primary mechanism for cross-department communication. Each role knows which reports to read and which to write:

| Phase | Reports Written | Reports Read |
|-------|----------------|-------------|
| RESEARCH | research-brief, feedback-synthesis, tool-evaluation, priority-matrix | plan/spec |
| DESIGN | architecture-review, contracts, design-spec, brand-guidelines, ux-flows | research-brief, tool-evaluation, priority-matrix |
| DEVELOP | (code in worktrees) | contracts, design-spec, brand-guidelines, ux-flows |
| TEST | test-results, security-report, performance-report, quality-dashboard, workflow-optimization | contracts, code |
| INTEGRATE | review-notes | test-results, quality-dashboard |
| OPTIMIZE | optimization-report | performance-report, workflow-optimization |
| DEPLOY | deployment-status | optimization-report, security-report |

## Rules for ALL Agents

| Rule | Reason |
|------|--------|
| Never modify `.team/config.json` | Only the coordinator manages config |
| Always read your inputs before starting | Prevents duplicate or conflicting work |
| Report blockers immediately via comms/ | Don't guess — communicate |
| Write structured JSON reports | Other agents and the coordinator parse them |
| Follow contracts exactly | The architect defined them for cross-team consistency |
| Stay within your role scope | Don't do another role's job |
