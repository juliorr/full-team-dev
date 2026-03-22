# Testing Department Protocol

## Department Overview

The Testing department is responsible for quality assurance across all dimensions: functional testing, security, performance, workflow optimization, tool evaluation, and results analysis. They operate primarily during the TEST phase but also participate in RESEARCH, INTEGRATE, OPTIMIZE, and DEPLOY.

## Department Lead

**Test Results Analyzer** — Makes final quality decisions for the department, aggregates all test results into a quality dashboard, and determines if the project meets quality gates.

## Roles and Responsibilities

| Role | Primary Focus | Phases |
|------|--------------|--------|
| tool-evaluator | Evaluate frameworks, libraries, tools | RESEARCH, TEST |
| api-tester | API endpoint validation, contract testing | TEST, INTEGRATE, DEPLOY |
| workflow-optimizer | CI/CD optimization, build optimization | TEST, OPTIMIZE |
| performance-benchmarker | Load testing, performance baselines | TEST, OPTIMIZE |
| test-results-analyzer | Aggregate results, quality dashboard | TEST |
| security-benchmark | Security scanning, vulnerability assessment | TEST, DEPLOY |

## Testing Workflow

```
Read contracts + code → Run specialized tests → Write report → Escalate failures if critical
```

## Quality Gates

The test-results-analyzer produces a quality dashboard with a verdict:

| Verdict | Meaning | Action |
|---------|---------|--------|
| `approved` | All quality gates passed | Proceed to next phase |
| `approved-with-warnings` | Minor issues found | Proceed, but log warnings |
| `changes-requested` | Significant issues found | Loop back to DEVELOP for fixes |
| `blocked` | Critical issues found | Stop and escalate to user |

## Report Schemas

### test-results.json (api-tester)
```json
{
  "type": "test-results",
  "phase": "test | integrate | deploy",
  "summary": { "passed": 0, "failed": 0, "skipped": 0 },
  "failures": [
    {
      "test": "test name",
      "error": "error message",
      "file": "src/api/users.ts",
      "assignedTo": "TASK-003",
      "severity": "critical | high | medium | low"
    }
  ],
  "contractViolations": []
}
```

### security-report.json (security-benchmark)
```json
{
  "type": "security-report",
  "vulnerabilities": [
    {
      "severity": "critical | high | medium | low",
      "category": "injection | xss | auth | config | dependency",
      "file": "src/api/users.ts",
      "line": 42,
      "description": "",
      "remediation": ""
    }
  ],
  "dependencyAudit": { "total": 0, "vulnerabilities": 0, "outdated": 0 },
  "verdict": "approved | changes-requested | blocked"
}
```

### performance-report.json (performance-benchmarker)
```json
{
  "type": "performance-report",
  "benchmarks": [
    {
      "name": "API /users GET",
      "avgResponseMs": 0,
      "p95ResponseMs": 0,
      "throughput": "",
      "memoryMb": 0,
      "status": "pass | warn | fail"
    }
  ],
  "bundleAnalysis": { "totalSizeKb": 0, "largestChunks": [] },
  "recommendations": []
}
```

### quality-dashboard.json (test-results-analyzer)
```json
{
  "type": "quality-dashboard",
  "overall": { "score": 0, "grade": "A|B|C|D|F", "verdict": "approved | changes-requested | blocked" },
  "categories": {
    "functional": { "passed": 0, "failed": 0, "coverage": "" },
    "security": { "critical": 0, "high": 0, "medium": 0, "low": 0 },
    "performance": { "passedBenchmarks": 0, "failedBenchmarks": 0 }
  },
  "blockers": [],
  "recommendations": []
}
```

### tool-evaluation.json (tool-evaluator)
```json
{
  "type": "tool-evaluation",
  "evaluations": [
    {
      "category": "frontend-framework | backend-framework | database | testing | ci-cd",
      "candidates": [
        {
          "name": "",
          "version": "",
          "score": 0,
          "pros": [],
          "cons": [],
          "communityHealth": "",
          "recommendation": true
        }
      ]
    }
  ]
}
```

### workflow-optimization.json (workflow-optimizer)
```json
{
  "type": "workflow-optimization",
  "currentState": { "buildTimeMs": 0, "testTimeMs": 0, "deployTimeMs": 0 },
  "optimizations": [
    {
      "area": "build | test | deploy | dx",
      "description": "",
      "expectedImprovement": "",
      "implementation": ""
    }
  ],
  "recommendations": []
}
```

## Communication

- **Read from**: `.team/reports/contracts.json`, code, test outputs
- **Write to**: `.team/reports/` (test results, security, performance, quality dashboard)
- **Consumed by**: developers (for fixes), devops (for optimization), sprint-prioritizer (for next iteration)
