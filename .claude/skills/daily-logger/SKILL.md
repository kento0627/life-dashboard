# Daily Logger Skill

Record Kento's daily accomplishments via voice-to-text logging.

→ Full workflow context: `.claude/workflows/daily-evening-log.md`

## Triggers

- "今日の記録" / "Let me record today"
- "Evening review" / "夜のレビュー"
- "朝の振り返り" / "Morning review"

## Quick Reference

### Always Ask
1. "今日できたことは？"
2. "今日は走れた？" (Running streak check)
3. "何時に寝る予定？" (Sleep tracking)
4. "エネルギーは10段階で？"

### Output Files
- Daily log: `life-timeline/daily-logs/YYYY-MM-DD.md`
- State update: `core/current-state.json`

### YAML Frontmatter
```yaml
date: YYYY-MM-DD
energy_level: [1-10]
roles_active: ["Role 1", "Role 2"]
ran_today: true/false
sleep_target: "HH:MM"
```

### Layer Tags for Done Today
- `[Business]` - tokoro/ERA, Recruit, property
- `[Content]` - Note articles
- `[Development]` - Projects, learning
- `[Wellbeing]` - Running, rest, relationships

## Rest Detection

| Signal | Action |
|--------|--------|
| Energy <= 4 | Add rest suggestion |
| 3+ days energy <= 6 | Flag: "週末に完全休息を" |
| Guilt about resting | "休むことは生産的" |

## Git (Never Commit)
Daily logs are in `.gitignore`. Only commit `core/current-state.json`.
