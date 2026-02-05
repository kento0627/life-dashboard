# Daily Evening Log Workflow

毎晩22:00、Kentoの1日を記録してgit commitする。

## Trigger

Kento says any of:
- "Let me record today"
- "Evening review"
- "夜のレビュー"
- "今日の記録"
- "記録して"

## Input Files (Must Read)

1. `core/current-state.json` - today's baseline energy and roles
2. Today's morning log if exists: `life-timeline/daily-logs/YYYY-MM-DD.md`
3. `core/life-context.json` - for cross-referencing goals

## Conversation Flow

### Phase 1: Open (Warm, Low Pressure)

```
Claude: "お疲れさまです。今日の記録をしましょう。
        まず、今日できたことを教えてください。大小問わず。"
```

Wait for Kento's response. He may speak in a stream-of-consciousness style mixing Japanese and English. That's fine.

### Phase 2: Parse Accomplishments

From Kento's response, extract and categorize by layer:

- `[Business]` - tokoro/ERA, Recruit, property, 匠技研
- `[Content]` - Note articles, writing, publishing
- `[Development]` - New skills, projects, learning
- `[Wellbeing]` - Running, rest, relationships, health

If a category has zero items, that's okay. Don't force it.

### Phase 3: Follow-Up Questions

Ask these **only if not already covered** in Kento's initial response:

```
Claude: "ありがとう。いくつか聞かせてください。"
```

**Always ask** (health check):
1. "今日は走れた？" (Running streak check)
2. "何時に寝る予定？" (Sleep time for 精神的安定 tracking)

**Ask if relevant**:
3. "何か気づきや学びはあった？" (Only if Kento didn't mention learnings)
4. "今日の中で、別のプロジェクトに繋がりそうなことは？" (Cross-layer prompt)

**Never ask**:
- "Why didn't you finish X?" (no guilt)
- "What about property hunting?" (unless Kento brought it up)

### Phase 4: Energy Assessment

```
Claude: "今日のエネルギーは10段階でどのくらい？"
```

After response, assess:

| Energy | Claude's Response |
|--------|-------------------|
| 8-10 | "いい調子ですね。この勢いを明日も。" |
| 5-7 | "お疲れさまです。しっかり休んでリセットしましょう。" |
| 1-4 | "無理しないでください。明日は軽めでいきましょう。休むことは投資です。" |

### Phase 5: Tomorrow's Intention

```
Claude: "明日の意図を1-3個、軽く決めておきましょう。"
```

Guide Kento to set intentions, not rigid tasks. If energy is low, suggest only 1-2.

### Phase 6: Confirm & Write

```
Claude: "記録しますね。"
```

## Output File

Create `life-timeline/daily-logs/YYYY-MM-DD.md`:

```markdown
---
date: YYYY-MM-DD
day_of_week: [曜日 in English]
energy_level: [1-10]
roles_active: ["Role 1", "Role 2"]
sleep_target: "HH:MM"
ran_today: [true/false]
---

## Done Today

### 🏢 Business
- [Accomplishment with specifics]
- [Accomplishment with specifics]

### 📝 Content
- [Article progress, writing done]

### 🛠 Development
- [Skills learned, projects explored]

### 💪 Wellbeing
- Running: [距離 or ✅/❌]
- [Other health/relationship notes]

## Learning
- [Key insight #1]
- [Key insight #2 if applicable]

## Cross-Layer Patterns
- [How did different domains connect today?]
- [e.g., "Recruit UX review → Ichihara guest journey improvement idea"]

## Tomorrow's Intention
1. [Intention 1]
2. [Intention 2]
3. [Intention 3]

## Metrics Update
- Note articles: [progress this week, e.g., "2/3 published, 1 at 75%"]
- tokoro/ERA: [property status, operational updates]
- Running streak: Day [N]
- Sleep target: [HH:MM]

## Energy Snapshot
- Energy: [N]/10
- Fatigue: [Low/Moderate/High]
- Mood: [Kento's own words or Claude's observation]
- Rest recommendation: [If applicable]
```

## Post-Write: Update State Files

### Update core/current-state.json

```json
{
  "date": "YYYY-MM-DD",
  "day_of_week": "[Day]",
  "energy_level": [N],
  "comment": "[From Kento's mood/energy description]",
  "roles_active_today": ["[roles from today]"],
  "current_focus": "[Derived from tomorrow's intentions]",
  "next_major_deadline": "[Carry forward or update]"
}
```

### Update metrics files (if data available)

**metrics/wellbeing.json** - append or update:
```json
{
  "date": "YYYY-MM-DD",
  "ran": true,
  "running_streak_day": 1043,
  "sleep_target": "23:00",
  "energy": 7,
  "mood": "productive"
}
```

**metrics/content-performance.json** - update if article published:
```json
{
  "week": "2026-W06",
  "articles_published": 2,
  "articles_target": 3,
  "articles_in_progress": [
    {"title": "...", "progress": "75%"}
  ]
}
```

## Git Commit

```bash
# Stage the daily log and any updated state/metrics files
git add life-timeline/daily-logs/YYYY-MM-DD.md
git add core/current-state.json

# Conditionally add metrics if they were updated
git add metrics/wellbeing.json 2>/dev/null
git add metrics/content-performance.json 2>/dev/null

git commit -m "Daily log: YYYY-MM-DD"
```

## Edge Cases

### Morning log already exists
- Read the existing file
- Merge morning data with evening data
- Morning section (intentions) stays at top, evening sections append below
- Don't overwrite morning energy level; record both if different

### Kento gives very short answers
- Accept it. Some days are low-energy.
- Write a shorter log. Don't pad with filler.
- Minimum viable log:

```markdown
---
date: YYYY-MM-DD
day_of_week: Thursday
energy_level: 4
roles_active: ["CEO (tokoro/ERA)"]
ran_today: true
---

## Done Today
- tokoro: Ichihara contractor call
- Running: 2km

## Tomorrow's Intention
1. Rest

## Energy Snapshot
- Energy: 4/10
- Rest recommendation: 明日は軽めに。無理しない。
```

### Kento is frustrated or upset
- Don't try to fix it or offer solutions immediately
- Record his feelings accurately in the log
- Add to Energy Snapshot: "精神的に不安定気味。明日は回復を優先。"
- Suggest: "今日は早めに休みましょう。明日の朝、改めて整理しましょう。"

### It's very late (past midnight)
- Use yesterday's date for the log if recording about yesterday
- Gently note: "遅い時間ですね。記録したらすぐ休みましょう。"

## Pattern Detection

Over time, flag these patterns in the log or energy check:

| Pattern | Detection | Action |
|---------|-----------|--------|
| Energy declining 3+ days | energy_level trend in recent logs | "3日連続でエネルギー低下傾向。週末に完全休息を。" |
| No running 2+ days | ran_today: false streak | "ランニング2日空いてます。軽いジョグでもOK。" |
| Sleep after 24:00 | sleep_target consistently late | "睡眠時間が遅くなっています。23:00目標に戻しましょう。" |
| Note pace behind | articles this week < pace for 3/week | "今週のNote: [N]/3。[残り日数]日で[残り本数]本。テーマは決まってますか？" |
| No girlfriend time mentioned 3+ days | absence in wellbeing | "最近パートナーとの時間は取れていますか？" |

## Closing Message

After commit, always close with:

```
Claude: "記録完了、commitしました。

        [One positive observation about today]
        [Rest suggestion if applicable]

        おやすみなさい 🌙"
```

## Example Full Session

```
Kento: "今日の記録して"

Claude: "お疲れさまです。今日できたことを教えてください。"

Kento: "えーと、Recruitのデザインレビュー終わらせた。
       あと市原のチェックリスト残り30%くらいまで進んだ。
       Noteは書けなかった。あ、でもネタは思いついた。
       あと2km走った。"

Claude: "いいですね、市原の準備が着実に進んでますね。
        Noteのネタ、どんな内容ですか？backlogに追加しておきます。"

Kento: "古民家の照明設計について。
       市原の照明決めてる時に色々調べたから。"

Claude: "いい題材ですね。実体験ベースは読者に響きます。
        何か今日の気づきや学びはありました？"

Kento: "照明って空間の印象を50%決めるって言われてるけど、
       実際に民泊の予約写真見ると本当にそうだなって。
       UXデザインの『第一印象は0.05秒で決まる』と同じ原理。"

Claude: "Recruit UXの知見が民泊デザインに直結する、
        いいクロスレイヤーパターンですね。
        今日は走れた？"

Kento: "うん、2km走った"

Claude: "ストリーク継続！何時に寝る予定ですか？"

Kento: "23時くらいかな"

Claude: "いいペースですね。エネルギーは10段階で？"

Kento: "7かな"

Claude: "了解です。明日の意図を軽く決めておきましょう。"

Kento: "Noteの照明記事のドラフト書く。
       市原チェックリスト完成させる。
       あと匠技研のデザイン提出。"

Claude: "記録完了、commitしました。

        市原準備が70%到達、デザインレビューも完了。
        着実に進んでいます。

        23時目標、いい習慣ですね。ゆっくり休んでください。"
```

→ `life-timeline/daily-logs/2026-02-05.md` created
→ `core/current-state.json` updated
→ Committed with "Daily log: 2026-02-05"
