# Design Department Protocol

## Department Overview

The Design department is responsible for UI/UX design, brand consistency, and visual storytelling. They operate primarily during the DESIGN phase and produce specifications that engineering roles consume during development.

## Department Lead

**UI Designer** — Makes final design decisions for the department, resolves visual conflicts, and ensures design system consistency.

## Roles and Responsibilities

| Role | Primary Focus | Phase |
|------|--------------|-------|
| ui-designer | Component specs, design system, responsive layouts | DESIGN |
| ux-researcher | User flows, information architecture, interaction patterns | DESIGN |
| brand-guardian | Visual identity, style guide, accessibility | DESIGN |
| visual-storyteller | Documentation visuals, architecture diagrams | DESIGN |

## Design Workflow

Design roles operate after the architect has defined contracts:

```
Read contracts → Read research outputs → Create design specifications → Write to reports/artifacts
```

## Artifacts Directory

Design roles produce artifacts in `.team/artifacts/`:

```
.team/artifacts/
├── design-tokens.json          # Colors, typography, spacing, breakpoints
├── component-specs/            # Individual component specifications
│   ├── header.json
│   ├── user-card.json
│   └── ...
└── prototypes/                 # Prototype descriptions or references
```

## Report Schemas

### design-spec.json (ui-designer)
```json
{
  "type": "design-spec",
  "designSystem": {
    "colors": { "primary": "", "secondary": "", "error": "", "background": "", "surface": "" },
    "typography": { "fontFamily": "", "headings": {}, "body": {} },
    "spacing": { "unit": "4px", "scale": [0, 1, 2, 3, 4, 5, 6, 8, 10, 12, 16] },
    "breakpoints": { "mobile": "320px", "tablet": "768px", "desktop": "1024px", "wide": "1440px" }
  },
  "components": [
    {
      "name": "ComponentName",
      "description": "",
      "props": [],
      "states": ["default", "hover", "active", "disabled", "loading", "error"],
      "responsive": { "mobile": "", "desktop": "" },
      "accessibility": ""
    }
  ],
  "layouts": []
}
```

### ux-flows.json (ux-researcher)
```json
{
  "type": "ux-flows",
  "userJourneys": [
    {
      "name": "User Registration",
      "persona": "",
      "steps": [{ "step": 1, "action": "", "screen": "", "notes": "" }],
      "successMetrics": []
    }
  ],
  "informationArchitecture": {
    "navigation": [],
    "hierarchy": []
  },
  "interactionPatterns": []
}
```

### brand-guidelines.json (brand-guardian)
```json
{
  "type": "brand-guidelines",
  "identity": {
    "name": "",
    "tagline": "",
    "toneOfVoice": "",
    "personality": []
  },
  "visual": {
    "colorPalette": {},
    "typography": {},
    "iconography": "",
    "imagery": ""
  },
  "accessibility": {
    "contrastRatio": "4.5:1 minimum",
    "focusIndicators": true,
    "ariaLabels": true,
    "keyboardNavigation": true
  },
  "doAndDont": {
    "do": [],
    "dont": []
  }
}
```

## Communication

- **Read from**: `.team/reports/contracts.json`, `.team/reports/research-brief.json`, plan/spec
- **Write to**: `.team/reports/` (design specs), `.team/artifacts/` (tokens, component specs)
- **Consumed by**: frontend-developer, mobile-app-developer, visual-storyteller
