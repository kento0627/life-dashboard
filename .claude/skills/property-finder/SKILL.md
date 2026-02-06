# Property Finder Skill

Evaluate incoming properties and manage waiting-phase strategy.

## Context

**Current phase**: Waiting. Market supply limited, competition high.
**Strategy**: Optimize network, be ready when opportunities appear.
**Rule**: Never pressure aggressive expansion.

→ Business context: `core/life-context.json`

## Triggers

- "物件情報が来た" / "この物件どう思う？"
- New property data shared

## Quick Evaluation Checklist

### Financial
- [ ] Purchase price < 2,000万円 (hotels) / < 1,500万円 (rentals)
- [ ] Total investment (price + renovation) within limits
- [ ] ROI timeline < 5 years

### Location
- [ ] Tourist demand exists
- [ ] Access from Tokyo < 2 hours (hotels)
- [ ] 民泊 regulations OK
- [ ] Near existing properties (Ichihara/Isumi)?

### Operational
- [ ] Fits tokoro/ERA brand
- [ ] Manageable remotely
- [ ] Can be operational by year-end 2026

## Verdicts

| Verdict | Action |
|---------|--------|
| **Pursue** | Create evaluation file, define next steps |
| **Watch** | Save to scouted-properties, monitor |
| **Pass** | Save to `why-rejected/` with reason |
| **Need More Info** | List what's missing |

## Output Files
- Evaluations: `projects/tokoro-era/property-hunt/scouted-properties/`
- Rejections: `projects/tokoro-era/property-hunt/scouted-properties/why-rejected/`

## Waiting Phase Actions (Don't Pressure)

Instead of "find more properties", suggest:
1. Agent relationship maintenance (3-5 active agents)
2. Market intelligence (price trends)
3. Readiness preparation (financing, contractors)
4. Optimize existing operations (Isumi 70%→80%)

## What NOT to Suggest
- "もっと積極的に探しましょう" (supply is bottleneck)
- "予算を上げれば" (don't encourage overextension)
- "6月退職を早めれば" (year-end plan is firm)
