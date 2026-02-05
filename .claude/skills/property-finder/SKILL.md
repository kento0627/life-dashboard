# Property Finder Skill

Evaluate incoming property opportunities and manage the waiting-phase strategy for tokoro/ERA expansion.

## Context

**Current status**: Waiting phase. Market supply is limited and competition is high. Kento cannot force property acquisition - the strategy is to optimize the network and be ready when opportunities appear.

**2026 targets** (from `core/life-context.json`):
- 3 traditional hotels (古民家ホテル)
- 10 urban rentals (都市型賃貸)
- 200万円/month profit

**Key rule from CLAUDE.md**: Never pressure aggressive expansion. The bottleneck is supply, not effort.

## Triggers

This skill activates when:
- Kento shares new property information: "物件情報が来た", "この物件どう思う？"
- Kento asks about property strategy: "物件探しどうしよう"
- New property data is added to `projects/tokoro-era/property-hunt/`
- Weekly review identifies property-related updates

## Prerequisites

Before evaluating, read:
1. `core/life-context.json` - targets and current phase
2. `projects/tokoro-era/property-hunt/scouted-properties/` - previous evaluations
3. `projects/tokoro-era/property-hunt/scouted-properties/{why-rejected}/` - rejection patterns

## Property Evaluation Workflow

### Step 1: Gather Property Details

When Kento shares property info, collect these data points (ask if missing):

```markdown
## Property Overview
- **Name/ID**: [Property identifier]
- **Location**: [Address or area]
- **Type**: [古民家 / 戸建て / マンション / アパート / 土地]
- **Price**: [Purchase price]
- **Size**: [㎡ or 坪]
- **Current condition**: [そのまま使える / 要リフォーム / 要フルリノベ]
- **Source**: [Agent name / portal / direct]
```

### Step 2: Evaluate Against Standards

Run the property through this checklist. Score each criterion:

#### Financial Viability

| Criterion | Check | Score |
|-----------|-------|-------|
| Purchase price within budget | Target: < 2,000万円 for hotels, < 1,500万円 for rentals | Pass/Fail |
| Estimated renovation cost | Based on condition + type | ___万円 |
| Total investment (price + reno) | Must stay within limits | ___万円 |
| Projected monthly revenue | Based on comparable properties | ___万円 |
| Projected monthly costs | Management, maintenance, loan | ___万円 |
| Monthly profit estimate | Revenue - costs | ___万円 |
| ROI timeline | Target: < 5 years payback | ___年 |

#### Location Quality

| Criterion | Check | Score |
|-----------|-------|-------|
| Tourist demand | Is there existing visitor traffic? | High/Med/Low |
| Access from Tokyo | < 2 hours preferred for hotels | ___時間 |
| Competition density | Other 民泊/hotels in area | High/Med/Low |
| Local regulations | 民泊 permitted? Special zones? | OK/NG/要確認 |
| Kento's existing presence | Near Ichihara/Isumi? Synergies? | Yes/No |

#### Operational Fit

| Criterion | Check | Score |
|-----------|-------|-------|
| Aligns with tokoro/ERA brand | Design-forward, experiential | Yes/No |
| Manageable remotely | Can operate without Kento on-site daily | Yes/No |
| Renovation scope realistic | Given current team + timeline | Yes/No |
| Fits 2026 timeline | Can be operational by year-end | Yes/No |

### Step 3: Generate Verdict

Based on evaluation, classify as one of:

- **Pursue** - Meets criteria, recommend next steps
- **Watch** - Interesting but missing key criteria, monitor
- **Pass** - Does not meet standards, document why
- **Need More Info** - Cannot evaluate without additional data

### Step 4: Save Evaluation

#### If Pursuing or Watching

Create `projects/tokoro-era/property-hunt/scouted-properties/YYYY-MM-DD-[location-or-name].md`:

```markdown
---
date: YYYY-MM-DD
property_name: [Name]
location: [Location]
type: [Type]
price: [Price]
verdict: [pursue/watch]
---

## Overview
[Property details]

## Financial Analysis
[From evaluation checklist]

## Location Analysis
[From evaluation checklist]

## Operational Fit
[From evaluation checklist]

## Verdict: [Pursue/Watch]
[Reasoning]

## Next Steps
1. [Specific action]
2. [Specific action]
```

#### If Passing

Create `projects/tokoro-era/property-hunt/scouted-properties/why-rejected/YYYY-MM-DD-[location-or-name].md`:

```markdown
---
date: YYYY-MM-DD
property_name: [Name]
location: [Location]
rejection_reason: [Primary reason category]
---

## Property Summary
[Brief description]

## Why Rejected
- **Primary reason**: [e.g., Price too high, Location poor, Regulation issue]
- **Secondary factors**: [Other concerns]

## Pattern Note
[Does this rejection match a pattern? e.g., "3rd property rejected for regulation issues in this area"]
```

### Step 5: Git Commit

```bash
git add "projects/tokoro-era/property-hunt/scouted-properties/"
git commit -m "Property evaluation: [name] ([verdict])"
```

## Rejection Pattern Analysis

When saving a rejection, scan previous rejections and identify patterns:

```
Rejection Reasons Distribution:
├── Price too high: 40% (4/10)
├── Location poor: 20% (2/10)
├── Regulation issues: 20% (2/10)
├── Renovation too expensive: 10% (1/10)
└── Operational complexity: 10% (1/10)
```

Report patterns to Kento during Sunday review:
> "最近の物件、40%が価格で不合格です。予算の見直し、もしくは価格帯の違うエリアを検討する価値があるかもしれません。"

## Waiting Phase Strategy

When Kento asks "物件探しどうしよう" or during weekly review, provide strategic guidance instead of pressure:

### Network Optimization Actions

These are productive actions during the waiting phase:

1. **Agent relationship maintenance**
   - Send quarterly updates to trusted agents about what you're looking for
   - Track which agents have sent properties and their hit rate
   - Target: Maintain 3-5 active agent relationships

2. **Market intelligence**
   - Monitor listing portals for price trends in target areas
   - Note seasonal patterns (when do good properties appear?)
   - Track comparable property sale prices

3. **Readiness preparation**
   - Property evaluation criteria refined (this checklist)
   - Financing pre-approved or ready to activate
   - Renovation team on standby (contractors identified)
   - Legal/regulation research completed for target areas

4. **Existing operations optimization**
   - Isumi: Push toward 80% occupancy (currently 70%)
   - Ichihara: Ensure smooth March 2026 opening
   - Document operational learnings for next property

### What NOT to Suggest

- "もっと積極的に探しましょう" (supply is the bottleneck, not effort)
- "予算を上げれば見つかります" (don't encourage overextension)
- "他のエリアも見ましょう" (only if Kento initiates geographic expansion)
- "6月退職を早めれば時間が..." (year-end transition plan is firm)

## Integration with Weekly Review

During Sunday review, the property section should include:

```markdown
## Property Hunting Update

### This Week
- Properties scouted: [N]
- Verdicts: [N] passed, [N] watching, [N] pursuing
- New agent contacts: [N]

### Pipeline
- Watching: [List of properties still being monitored]
- Pursuing: [List of properties with active next steps]

### Pattern Insights
- [Any trends from rejection analysis]

### Network Health
- Active agents: [N] / Target: 5
- Last contact with each: [dates]

### Waiting Phase Actions Completed
- [x] [Action taken]
- [ ] [Action pending]
```

## Example Session

```
Kento: "不動産エージェントから物件情報来た。千葉の古民家、1,800万円、
       120㎡、リフォーム必要。勝浦エリア。"

Claude: "評価してみましょう。いくつか確認させてください。
        1. リフォームの程度は？（軽微 / 中規模 / フルリノベ）
        2. 民泊許可エリアですか？
        3. 東京からのアクセスは？"

Kento: "中規模リフォームかな。民泊は要確認。東京から2時間くらい。"

Claude: "評価結果です：

        ## 千葉・勝浦 古民家 - 評価

        **Verdict: Need More Info**

        ### 良い点
        - 価格1,800万円は予算内
        - 120㎡は古民家ホテルとして十分
        - 東京2時間はギリギリ許容範囲

        ### 懸念点
        - 民泊規制が未確認 ← これが最大のブロッカー
        - 中規模リフォーム費用の見積もりが必要（推定500-800万円）
        - 勝浦エリアの観光需要データが不足

        ### Next Steps
        1. エージェントに民泊規制を確認依頼
        2. リフォーム概算見積もりを取る
        3. 勝浦エリアの民泊稼働率を調査

        物件情報を保存しました。規制確認が取れたら再評価しましょう。"
```

## File References

- Evaluations: `projects/tokoro-era/property-hunt/scouted-properties/`
- Rejections: `projects/tokoro-era/property-hunt/scouted-properties/why-rejected/` (currently `{why-rejected}/`, rename needed)
- Context: `core/life-context.json`
- KPIs: `projects/tokoro-era/2026-targets.json` (when created)
