# Weekly Review Workflow

毎週日曜20:00、4レイヤーの包括的な週次レビューを生成する。

## Trigger

- Sunday 20:00 (prompted or self-initiated)
- Kento says: "Weekly review", "週次レビュー", "今週の振り返り"

## Input Files (Must Read All)

### Required
1. `life-timeline/daily-logs/` - all entries from past 7 days
2. `core/life-context.json` - goals, values, roles
3. `core/current-state.json` - current state

### Metrics (read if exists)
4. `metrics/tokoro-era.json` - business KPIs
5. `metrics/content-performance.json` - Note article data
6. `metrics/wellbeing.json` - health/mood tracking

### Projects (read if exists)
7. `projects/tokoro-era/2026-targets.json` - annual targets
8. `projects/note-publication/articles/index.md` - published articles
9. `projects/note-publication/backlog/article-ideas.md` - pipeline
10. `projects/emerging-projects/` - all subdirectories from this week

### Previous Week
11. Previous weekly digest in `life-timeline/weekly-digests/` - for trend comparison

## Processing Logic

### Step 1: Aggregate Daily Logs

Parse all daily logs from the week and compile:

```
week_data = {
  days_logged: N/7,
  energy_levels: [6, 7, 5, 7, 8, 6, 7],
  energy_average: 6.6,
  energy_trend: "stable" | "declining" | "improving",
  ran_days: N/7,
  sleep_targets: ["23:00", "23:30", ...],
  roles_active: { "Recruit PM": 5, "tokoro CEO": 4, "匠技研": 2 },
  accomplishments_by_layer: {
    business: [...],
    content: [...],
    development: [...],
    wellbeing: [...]
  },
  learnings: [...],
  cross_layer_patterns: [...]
}
```

### Step 2: Compare Against Targets

Pull targets from `core/life-context.json` and project files:

| Target | Goal | This Week | Status |
|--------|------|-----------|--------|
| Note articles | 3/week | [N] published | [On track / Behind / Ahead] |
| Properties | 3 hotels + 10 rentals by EOY | [Status] | [Phase: Waiting/Active/Closing] |
| Monthly profit | 200万円 | [Current if known] | [Progress] |
| Running | Daily 2km | [N]/7 days | [Streak: Day N] |
| Sleep | 23:00 target | Avg [HH:MM] | [On/Off target] |

### Step 3: Identify Cross-Layer Patterns

Scan all daily logs' "Cross-Layer Patterns" and "Learning" sections. Look for:

- Skills transferring between roles (Recruit UX → tokoro design)
- Ideas emerging from physical activity (running → creative insights)
- Content ideas born from operational work (tokoro operations → Note articles)
- Emotional patterns (energy correlating with specific activities)

### Step 4: Review Emerging Projects

List all directories in `projects/emerging-projects/`:
- New this week → summarize brief.md
- From previous weeks → check if still relevant
- Prepare decision prompt for Kento (Promote / Hold / Archive / Kill)

### Step 5: Assess Wellbeing

Compile from daily logs:
- Running streak status
- Average energy level + trend
- Sleep pattern
- Relationship mentions (girlfriend time)
- Stress/frustration indicators
- Rest days taken

## Output File

Create `life-timeline/weekly-digests/YYYY-wWW.md`:

```markdown
# Weekly Digest - Week [WW], 2026

**Period**: [Monday date] - [Sunday date]
**Days Logged**: [N]/7
**Average Energy**: [N.N]/10 ([trend emoji] [stable/declining/improving])

---

## 🏢 Business Layer

### tokoro/ERA
- **Ichihara**: [Status update, days until March 1 opening]
- **Isumi**: [Occupancy rate, operational notes]
- **Property hunting**: [Properties scouted, verdicts, pipeline status]
- **Progress vs 2026 target**: [N] hotels / 3 target, [N] rentals / 10 target

#### Key Actions This Week
- [Specific accomplishment 1]
- [Specific accomplishment 2]

#### Blockers
- [If any, with analysis]

### Recruit
- **Workload**: [Hours/day estimate from roles_active frequency]
- **Transition status**: [Progress toward year-end exit]
- **Notable work**: [Key accomplishments]

### 匠技研
- [Status if active this week]

---

## 📝 Content Layer

### Note Publication
- **Articles published**: [N] / 3 target [✅ or ⚠️]
- **Articles in progress**: [List with % completion]
- **Backlog health**: [N] ideas queued

#### Published This Week
| Title | Date | [Performance if known] |
|-------|------|----------------------|
| [Title] | [Date] | [Views/likes if tracked] |

#### Pipeline
| Title | Status | Next Step |
|-------|--------|-----------|
| [Title] | [N]% draft | [What's needed to finish] |

#### Pace Analysis
- Week [W-1]: [N] articles
- Week [W]: [N] articles
- Trend: [Improving / Stable / Declining]
- To hit 3/week: [Specific suggestion based on root cause analysis]

---

## 🛠 Development Layer

### Emerging Projects This Week
[For each new project in emerging-projects/:]

#### [Project Name] (created [date])
- **Core idea**: [One sentence from brief.md]
- **Dependencies**: [Key connections to existing projects]
- **Sunday Decision**: ⬜ Promote / ⬜ Hold / ⬜ Archive / ⬜ Kill

### Previous Emerging Projects
[For each existing project from prior weeks:]
- **[Name]** ([created date]): [Current status, still relevant?]

### Skills & Learning
- [Key insights from daily logs' Learning sections]
- [New skills practiced or discovered]

---

## 💪 Wellbeing Layer

### Health Metrics
| Metric | This Week | Target | Status |
|--------|-----------|--------|--------|
| Running | [N]/7 days | Daily 2km | [Streak Day N] |
| Avg Energy | [N.N]/10 | 7+ | [emoji] |
| Avg Sleep Target | [HH:MM] | 23:00 | [On/Off target] |
| Rest Days | [N] | 1-2/week | [Sufficient?] |

### Energy Trajectory
```
Mon: ██████░░░░ 6/10
Tue: ███████░░░ 7/10
Wed: █████░░░░░ 5/10
Thu: ███████░░░ 7/10
Fri: ████████░░ 8/10
Sat: ██████░░░░ 6/10
Sun: ███████░░░ 7/10
```
**Pattern**: [Observation about energy pattern, e.g., "Mid-week dip, recovers by Friday"]

### Relationships
- Girlfriend time: [Mentioned in N daily logs]
- Social connections: [Any notable interactions]

### Mental State Assessment
- [Overall mood trajectory]
- [Stress indicators if any]
- [Is 精神的安定 being maintained?]

---

## ✨ Cross-Layer Insights

This section identifies connections between Kento's different life domains that compound value.

[For each pattern identified:]

### [Insight Title]
- **Observation**: [What was noticed]
- **Domains connected**: [Layer A] → [Layer B]
- **Actionable**: [How to leverage this connection]

**Examples of patterns to surface:**
- "Recruit UXレビュー中に、市原のゲスト導線改善のアイデアが3つ出た" (Business → Business cross-pollination)
- "ランニング後にNote記事のアウトラインが浮かんだ（2回）" (Wellbeing → Content)
- "市原の内装調査 → Note記事「古民家照明設計」のネタに" (Business → Content)

---

## ⚠️ Blockers & Risks

### Active Blockers
[List only real blockers, not vague concerns]

| Blocker | Impact | Owned By | Next Action |
|---------|--------|----------|-------------|
| [Description] | [What it blocks] | [Kento / External] | [Specific next step] |

### Risks to Watch
- [Emerging risk with early warning signs]

### Market Conditions (Property)
- **Supply**: [Current market observation]
- **Strategy**: [Waiting / Active / Adjusting]
- **Agent network**: [N] active agents, last contact [dates]

---

## 🎯 Next Week's 3 Priorities

Based on this week's data, targets, and blockers:

### 1. [Priority - Concrete Action]
- **Layer**: [Layer]
- **Why**: [Data-driven reasoning]
- **Success looks like**: [Measurable outcome]

### 2. [Priority - Concrete Action]
- **Layer**: [Layer]
- **Why**: [Data-driven reasoning]
- **Success looks like**: [Measurable outcome]

### 3. [Priority - Concrete Action]
- **Layer**: [Layer]
- **Why**: [Data-driven reasoning]
- **Success looks like**: [Measurable outcome]

---

## 💚 Rest & Recovery

[Personalized message based on this week's data]

**This week you accomplished:**
- [Highlight 1 - celebrate]
- [Highlight 2 - celebrate]
- [Highlight 3 - celebrate]

**Reminder**: [Specific rest suggestion for next week]

[If energy declining]: "今週のエネルギーが先週より下がっています。来週は1日、完全に仕事をしない日を作りましょう。"

[If energy stable/good]: "いいペースで進んでいます。このリズムを維持しつつ、週末は意識的にリラックスの時間を。"

[Always include]: "精神的安定が全ての土台です。成果は安定の上に積み上がります。"

---

_Generated: [Sunday date and time]_
_Next review: [Next Sunday date]_
```

## Post-Generation: Emerging Projects Review

After generating the digest, if there are projects in `projects/emerging-projects/`, facilitate the decision:

```
Claude: "今週のemerging projectsをレビューしましょう。"

[For each project:]

Claude: "[Project Name]（[created date]）
        概要: [One sentence]
        依存関係: [Key dependencies]

        どうしますか？
        1. Promote（正式プロジェクト化）
        2. Hold（来週もう一度考える）
        3. Archive（保留、いつか戻る）
        4. Kill（やらない）"
```

Update `timeline.json` with Kento's decision.

If promoted:
```bash
mv "projects/emerging-projects/[name]" "projects/[name]"
git add "projects/[name]/"
```

If archived:
```bash
mkdir -p "projects/emerging-projects/_archived"
mv "projects/emerging-projects/[name]" "projects/emerging-projects/_archived/"
git add "projects/emerging-projects/_archived/[name]/"
```

If killed:
```bash
# Confirm with Kento first
rm -rf "projects/emerging-projects/[name]"
```

## Git Commit

```bash
WEEK_NUM=$(date +%V)
git add "life-timeline/weekly-digests/2026-w${WEEK_NUM}.md"

# Include any emerging project decisions
git add projects/emerging-projects/ 2>/dev/null
git add projects/ 2>/dev/null

git commit -m "Weekly digest: Week ${WEEK_NUM}, 2026"
```

## Week-Over-Week Comparison

When previous weekly digest exists, include trend comparison:

```markdown
### Week-Over-Week
| Metric | Week [W-1] | Week [W] | Trend |
|--------|-----------|----------|-------|
| Articles published | 2 | 3 | ↑ |
| Avg energy | 6.2 | 6.6 | ↑ |
| Running days | 6/7 | 7/7 | ↑ |
| Properties scouted | 1 | 0 | → (market dependent) |
| Sleep avg | 23:30 | 23:15 | ↑ |
```

## Rules

1. **Celebrate all 4 layers**: Business progress is not more important than running streak or relationship time. Give equal weight.
2. **Never shame missed targets**: Instead of "Note目標未達", say "2/3本。3本目のボトルネックは何でしょう？" Analyze root cause.
3. **Mental stability first**: If wellbeing metrics show decline, make rest the #1 priority for next week regardless of business urgency.
4. **Property hunting is market-dependent**: Never frame waiting as failure. "待機中" is a valid and correct strategy. Frame it as "ネットワーク最適化フェーズ".
5. **Data over opinion**: Every claim should reference a specific log entry or metric. "なんとなく忙しそう" ではなく "今週のエネルギー平均5.8、先週比-0.4".
6. **Cross-layer patterns are gold**: These are unique insights only visible through structured logging. Always highlight them prominently.
7. **Keep it actionable**: Next week's priorities must be concrete enough to become Monday's morning intention.
8. **Respect the transition timeline**: Year-end Recruit exit. Never suggest accelerating unless Kento initiates.
9. **Sunday is reflection, not pressure**: The tone should be reflective and appreciative, not demanding.
