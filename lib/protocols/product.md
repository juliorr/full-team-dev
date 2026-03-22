# Product Department Protocol

## Department Overview

The Product department is responsible for market research, user feedback analysis, and sprint prioritization. They operate primarily during the RESEARCH phase and provide context that informs all subsequent phases.

## Department Lead

**Sprint Prioritizer** — Makes final priority decisions for the department, resolves conflicts between product roles, and validates business requirements during integration.

## Roles and Responsibilities

| Role | Primary Focus | Phase |
|------|--------------|-------|
| trend-researcher | Market & tech trends analysis | RESEARCH |
| feedback-synthesizer | User feedback analysis | RESEARCH |
| sprint-prioritizer | Task prioritization & dependency analysis | RESEARCH, INTEGRATE |

## Research Workflow

Product roles produce research outputs that inform the Design and Engineering departments:

```
Read plan/spec → Analyze domain → Produce structured report → Checkpoint approval
```

## Report Schemas

### research-brief.json (trend-researcher)
```json
{
  "type": "research-brief",
  "market": {
    "trends": ["trend 1", "trend 2"],
    "competitors": [{ "name": "", "strengths": [], "weaknesses": [] }],
    "opportunities": []
  },
  "technology": {
    "recommendations": [],
    "risks": []
  },
  "userInsights": {
    "targetAudience": "",
    "painPoints": [],
    "expectations": []
  }
}
```

### feedback-synthesis.json (feedback-synthesizer)
```json
{
  "type": "feedback-synthesis",
  "sources": ["source description"],
  "themes": [{ "theme": "", "frequency": "high|medium|low", "sentiment": "positive|negative|neutral" }],
  "featureRequests": [{ "feature": "", "demand": "high|medium|low", "feasibility": "" }],
  "painPoints": [{ "issue": "", "impact": "critical|high|medium|low", "suggestedSolution": "" }],
  "strategy": ""
}
```

### priority-matrix.json (sprint-prioritizer)
```json
{
  "type": "priority-matrix",
  "sprints": [
    {
      "id": 1,
      "goals": ["goal 1"],
      "mustHave": ["TASK-001"],
      "shouldHave": ["TASK-005"],
      "couldHave": ["TASK-008"],
      "risks": []
    }
  ],
  "dependencyGraph": {
    "nodes": [],
    "edges": []
  }
}
```

## Communication

- **Read from**: plan/spec, existing feedback data, issue trackers
- **Write to**: `.team/reports/` (research outputs)
- **Consumed by**: architect (for task decomposition), ui-designer (for user insights), sprint-prioritizer (for prioritization)
