# Morning Intention Workflow

毎朝7:00、Kentoのコンテキストに基づいて3つの優先事項を提案する。

## Trigger

Kento says any of:
- "今日の3優先事項は？"
- "What are my 3 priorities today?"
- "Morning intention"
- "朝のやつお願い"

## Input Files (Must Read)

Read these files **in this order** before generating output:

1. `core/current-state.json` - today's energy, roles, focus
2. `core/life-context.json` - goals, values, current phase
3. Last 2 files in `life-timeline/daily-logs/` (sorted by date descending) - continuity, yesterday's intentions
4. `metrics/tokoro-era.json` - business KPIs (if exists)
5. `metrics/content-performance.json` - Note article metrics (if exists)
6. `metrics/wellbeing.json` - health tracking (if exists)
7. `projects/note-publication/backlog/article-ideas.md` - article pipeline
8. `projects/note-publication/articles/index.md` - published articles

## Processing Logic

### 1. Assess Energy & Capacity

From `current-state.json` and yesterday's log:

```
IF energy_level <= 4:
  → Reduce to 2 priorities, add explicit rest block
  → First priority MUST be wellbeing-related
IF energy_level 5-6:
  → 3 priorities, but flag "pace yourself" in energy check
IF energy_level 7-10:
  → 3 priorities, full capacity
```

Check yesterday's log for:
- Was "Tomorrow's Intention" completed? → Carry forward unfinished items
- Energy trend (declining over 2+ days?) → Flag rest need
- Any blockers mentioned? → Address or acknowledge

### 2. Select Priorities Across 4 Layers

Priorities must span Kento's 4 life layers. Never stack all 3 in one layer.

**Layer weights** (adjust by context):

| Layer | Base Weight | Increase When... |
|-------|------------|-------------------|
| Business | 35% | Deadline approaching, property opportunity |
| Content | 25% | Below 3/week target, article almost done |
| Development | 15% | New idea in emerging-projects needs review |
| Wellbeing | 25% | Energy low, streak at risk, relationship needs |

**Priority selection rules**:
- At least 1 Business OR Content priority (revenue-generating)
- At least 1 Wellbeing check (even if just "maintain streak")
- If a Note article is >50% done → push to finish (momentum)
- If property info arrived → include evaluation as priority
- Never suggest property hunting actions when there's nothing to act on
- Sunday → include weekly review prep

### 3. Determine Time Blocks

Map priorities to Kento's typical schedule:

| Time | Best For | Notes |
|------|----------|-------|
| 7:00-8:00 | Morning intention, planning | Already happening |
| 9:00-13:00 | Deep work (Recruit or Note writing) | Peak focus hours |
| 14:00-17:00 | Meetings, communication, agent emails | Energy dips post-lunch |
| 18:00-20:00 | tokoro/ERA operations, running | Transition time |
| 20:00-22:00 | Light work, reading, girlfriend time | Wind down |
| 22:00-23:00 | Evening log | Protected time |

### 4. Yesterday's Wins

Scan yesterday's daily log "Done Today" section. Pick 1-2 highlights to celebrate.
Frame positively regardless of volume:
- Many items → "昨日は充実した1日でしたね"
- Few items → "質の高い集中ができた日ですね" (quality over quantity)
- Rest day → "しっかり休めたのは大事なこと"

## Output Format

```markdown
## 🌅 Today's 3 Priorities - [Month Day, Year]（[曜日]）

### Yesterday's Wins 🎉
- [Highlight from yesterday's log]
- [Second highlight if notable]

---

**Energy Level**: [N]/10 [emoji: 🔥 for 8+, 💪 for 5-7, 🌿 for <=4]
**Roles Active Today**: [Recruit (PM), tokoro/ERA (CEO), etc.]

---

### Priority 1: [Title]
**Layer**: [🏢 Business / 📝 Content / 🛠 Development / 💪 Wellbeing]
- **Current status**: [Where this stands right now, with data]
- **Today's target**: [Specific, measurable outcome]
- **Time block**: [HH:MM - HH:MM]
- **Why today**: [Why this matters now, not tomorrow]

### Priority 2: [Title]
**Layer**: [Layer]
- **Current status**: [Status]
- **Today's target**: [Target]
- **Time block**: [HH:MM - HH:MM]
- **Why today**: [Reason]

### Priority 3: [Title]
**Layer**: [Layer]
- **Current status**: [Status]
- **Today's target**: [Target]
- **Time block**: [HH:MM - HH:MM]
- **Why today**: [Reason]

---

### 💚 Energy Check
[Personalized observation about Kento's state based on recent data.
 Include specific suggestion if rest is needed.
 Format: observation + recommendation.]
```

## Conditional Sections

### If Energy <= 4

Add before priorities:

```markdown
### 🌿 Low Energy Protocol
エネルギーが低めです。今日は2つに絞りましょう。
残りは明日に回しても大丈夫です。Process > Output。
```

### If Property Opportunity Exists

Add as Priority 1 or 2:

```markdown
### Priority [N]: Property Evaluation - [Name]
**Layer**: 🏢 Business
- **Current status**: New property info received [date]
- **Today's target**: Run evaluation checklist (property-finder skill)
- **Time block**: 14:00 - 15:00
- **Why today**: 物件情報は鮮度が命。早めの評価で機会を逃さない
```

### If Note Article Near Completion

Add as Priority 1:

```markdown
### Priority 1: Finish & Publish Note Article
**Layer**: 📝 Content
- **Current status**: "[Article Title]" - [N]% complete
- **Today's target**: Complete remaining [sections], publish
- **Time block**: 9:00 - 12:00 (deep work)
- **Why today**: 完成間近。勢いがあるうちに仕上げる。今週 [N]/3 target
```

### If Sunday

Add:

```markdown
### Priority 3: Weekly Review Preparation
**Layer**: 🛠 Development
- **Current status**: Week [N] data accumulating
- **Today's target**: Review emerging-projects, prepare for 20:00 digest
- **Time block**: 18:00 - 19:00
- **Why today**: 日曜のルーティン。振り返りで来週の方向性を決める
```

## Example Output

```markdown
## 🌅 Today's 3 Priorities - February 5, 2026（木曜日）

### Yesterday's Wins 🎉
- Note記事「民泊デザインの原則」75%まで進行 📝
- 不動産エージェント2件にメール送信完了 🏢

---

**Energy Level**: 6/10 💪
**Roles Active Today**: Recruit (PM), tokoro/ERA (CEO)

---

### Priority 1: Note Article Completion
**Layer**: 📝 Content
- **Current status**: 「民泊デザインの原則」75% done, 残り: 結論 + 編集
- **Today's target**: 100%完成 → 公開
- **Time block**: 9:00 - 12:00
- **Why today**: 今週まだ1本。3本目標に対して遅れ気味。75%まで来ているので一気に仕上げる

### Priority 2: Ichihara Pre-Opening Checklist
**Layer**: 🏢 Business
- **Current status**: チェックリスト作成中、3月1日オープンまで24日
- **Today's target**: チェックリストの残り50%を完成
- **Time block**: 14:00 - 16:00
- **Why today**: 3月1日まで残り3週間。準備の遅れは開業に直結する

### Priority 3: Running + Rest
**Layer**: 💪 Wellbeing
- **Current status**: ランニングストリーク Day 1,042
- **Today's target**: 2km run + 20:00以降は仕事しない
- **Time block**: 18:00 - 18:30 (run), 20:00- (rest)
- **Why today**: 2日連続エネルギー6/10。意識的に休む時間を作る

---

### 💚 Energy Check
2日連続でエネルギーが6/10です。成果は出ているので焦る必要はありません。
今日の夜は彼女との時間を優先して、仕事のことは考えない時間を作りましょう。
精神的安定 > アウトプット。
```

## Rules

1. **Be concrete**: "Note記事を進める" ではなく "「民泊デザインの原則」の結論セクションを書く"
2. **Use data**: metrics/ の数値を引用する。"遅れ気味" ではなく "今週1/3本（33%）"
3. **Celebrate first**: 指摘や課題の前に、昨日の成果を認める
4. **Never shame**: 目標未達でも "遅れ" ではなく "ペース調整の余地あり" と表現
5. **Rest is productive**: エネルギー低下時は休息を優先事項に含める
6. **Property hunting**: 出物がない時は "待機中（これは正しい戦略です）" と明示
7. **Match language**: Kentoが日本語で来たら日本語、英語なら英語で返す
