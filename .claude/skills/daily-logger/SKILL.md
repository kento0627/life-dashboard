# Daily Logger Skill

Record Kento's daily accomplishments, learnings, and intentions via voice-to-text logging.

## Triggers

This skill activates when Kento says any of:
- "今日の記録" / "Let me record today"
- "Evening review" / "夜のレビュー"
- "朝の振り返り" / "昨日のレビュー"
- "Morning review"

## Prerequisites

Before running, always read:
1. `core/current-state.json` - today's energy level and active roles
2. `core/life-context.json` - current phase and goals
3. Last 2 entries in `life-timeline/daily-logs/` - for continuity

## Workflow

### Step 1: Detect Date & Check for Existing Log

```bash
TODAY=$(date +%Y-%m-%d)
LOG_FILE="life-timeline/daily-logs/${TODAY}.md"
```

- If `$LOG_FILE` already exists, read it and offer to **update** (append new sections or edit existing ones)
- If it does not exist, create a new file from the template below

### Step 2: Gather Input from Kento

Ask Kento these questions in natural conversation (Japanese or English, match his language):

**Morning flow** (朝):
1. "昨日どうだった？ エネルギーは？" (energy level 1-10)
2. "今日のフォーカスは？" (what roles are active today)
3. "今日の意図は？" (1-3 intentions for the day)

**Evening flow** (夜):
1. "今日できたことは？" (done today - list accomplishments)
2. "何か学んだことは？" (learnings - insights, patterns)
3. "明日の意図は？" (tomorrow's intention)
4. "疲労度は？ 気分は？" (energy snapshot)

Accept voice-dictated text as-is. Clean up obvious transcription errors but preserve Kento's natural phrasing (Japanese mixed with English is normal).

### Step 3: Write the Daily Log

Create/update `life-timeline/daily-logs/YYYY-MM-DD.md` using this format:

```markdown
---
date: YYYY-MM-DD
day_of_week: [Day]
energy_level: [1-10]
roles_active: ["Role 1", "Role 2"]
---

## Done Today
- [Accomplishment 1]
- [Accomplishment 2]
- [Accomplishment 3]

## Learning
- [Insight or pattern discovered]
- [Connection between projects/layers]

## Tomorrow's Intention
1. [Priority 1]
2. [Priority 2]
3. [Priority 3]

## Energy Snapshot
- Fatigue: [Low/Moderate/High]
- Mood: [Description]
- Rest needed: [Yes/No + suggestion if Yes]
```

### Step 4: Update current-state.json

After writing the daily log, update `core/current-state.json` with:
- Today's date
- Day of week
- Energy level from the log
- Roles active today
- Current focus (derived from intentions)
- Next major deadline (carry forward unless changed)

```json
{
  "date": "YYYY-MM-DD",
  "day_of_week": "Thursday",
  "energy_level": 7,
  "comment": "Derived from Kento's own words",
  "roles_active_today": ["PM at Recruit", "CEO (tokoro/ERA)"],
  "current_focus": "From today's intentions",
  "next_major_deadline": "Carry forward from previous"
}
```

### Step 5: Git Commit

```bash
git add life-timeline/daily-logs/YYYY-MM-DD.md core/current-state.json
git commit -m "Daily log: YYYY-MM-DD"
```

## Rest Detection

After recording, evaluate Kento's responses for rest signals:

| Signal | Action |
|--------|--------|
| Energy <= 4 | Add "Rest Reminder" section. Suggest specific rest action. |
| Energy 5-6 + "restless" or "疲れた" | Gentle note: "Process > Output today." |
| 3+ consecutive days energy <= 6 | Flag in log: "3日連続エネルギー低め。週末に完全休息を。" |
| Mood mentions guilt about resting | Remind: "休むことは生産的。精神的安定 > アウトプット。" |

## Error Handling

- **File already exists (evening update to morning log)**: Read existing content, merge new sections, preserve morning data
- **Missing energy level**: Default to previous day's level, ask to confirm
- **Empty input**: Prompt again with "何か一つでも、小さなことでもOK"
- **Git conflict**: Show diff, let Kento choose which version to keep

## Cross-Layer Tracking

When writing "Done Today", tag accomplishments by layer for weekly digest aggregation:

- `[Business]` - tokoro/ERA, Recruit, property hunting
- `[Content]` - Note articles, writing
- `[Development]` - New projects, learning, skills
- `[Wellbeing]` - Running, rest, relationships

Example:
```markdown
## Done Today
- [Business] tokoro: Ichihara pre-opening checklist 50% complete
- [Content] Note article draft: "Design Systems for Hospitality" - 75% done
- [Wellbeing] Running streak Day 1,042 maintained
- [Business] Recruit: Design review for Q2 feature
```

## Example Session

```
Kento: "夜のレビューしよう"

Claude: "お疲れさまです。今日できたことを教えてください。"

Kento: "えーと、Noteの記事を1本書き上げた。あと市原の準備でチェックリスト作った。
       ランニングもした。あ、あと不動産エージェントに2件メール送った。"

Claude: "いいですね。学んだことや気づきはありますか？"

Kento: "民泊のUX設計、Recruitで学んだことがそのまま使えるなって思った。"

Claude: "なるほど、クロスレイヤーの知見ですね。疲労度はどうですか？"

Kento: "6くらいかな。まあまあ。"

Claude: "記録しました。"
```

→ Creates `life-timeline/daily-logs/2026-02-05.md` with structured content
→ Updates `core/current-state.json`
→ Commits both files

## File References

- Log output: `life-timeline/daily-logs/YYYY-MM-DD.md`
- State update: `core/current-state.json`
- Context: `core/life-context.json`
- Previous logs: `life-timeline/daily-logs/` (latest 2-3 entries)
