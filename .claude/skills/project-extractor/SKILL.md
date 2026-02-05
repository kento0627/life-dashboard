# Project Extractor Skill

Capture, structure, and store Kento's emerging project ideas for Sunday review.

## Triggers

This skill activates when Kento's input contains any of these patterns:
- `〜したいな` / `〜したい`
- `〜作ってみたい` / `〜作りたい`
- `〜やってみたい`
- `〜できないかな`
- `〜あったらいいな`
- "I want to build..." / "What if we..." / "I'm thinking about..."

When detected, confirm with Kento before extracting:
> "新しいプロジェクトアイデアっぽいですね。構造化して保存しますか？"

## Prerequisites

Before extracting, read:
1. `core/life-context.json` - current roles, goals, values
2. `projects/emerging-projects/` - existing ideas (avoid duplicates)
3. `projects/` directory listing - all active projects (for dependency mapping)

## Workflow

### Step 1: Ask Clarifying Questions (Max 3)

Keep it lightweight. Kento should not feel like he's filling out a form.

Good questions:
1. "これ、何がきっかけで思いついた？" (origin / why now)
2. "誰が使う想定？" (target user)
3. "今の事業（tokoro/ERAやRecruitの知見）とどう繋がる？" (dependency)

Bad questions (avoid):
- "ビジネスモデルは？" (too heavy for emerging idea)
- "いつまでに作る？" (premature pressure)

### Step 2: Create Project Directory

```bash
TODAY=$(date +%Y-%m-%d)
PROJECT_SLUG=$(echo "$PROJECT_NAME" | tr '[:upper:]' '[:lower:]' | tr ' ' '-' | tr -cd 'a-z0-9-')
PROJECT_DIR="projects/emerging-projects/${TODAY}-${PROJECT_SLUG}"
mkdir -p "$PROJECT_DIR"
```

### Step 3: Generate brief.md

Write `projects/emerging-projects/YYYY-MM-DD-[name]/brief.md`:

```markdown
# [Project Name]

**Created**: YYYY-MM-DD
**Status**: Emerging (未レビュー)
**Origin**: [What triggered the idea]

## Core Idea
[2-3 sentences describing what this is]

## Why Now
[Why this idea surfaced at this point in Kento's journey]
- Connection to current work: [How it relates to tokoro/ERA, Recruit, Note, etc.]
- Market timing: [If relevant]
- Personal readiness: [Skills/resources available]

## Target User
[Who would use/benefit from this]

## Dependencies on Existing Projects
- [ ] Requires: [existing project or resource]
- [ ] Builds on: [knowledge/skill from current role]
- [ ] Conflicts with: [time/resource competition]

## Rough Scope
- **Small** (side project, <1 month): [description if applicable]
- **Medium** (dedicated effort, 1-3 months): [description if applicable]
- **Large** (major initiative, 3+ months): [description if applicable]

## Value Alignment Check
- 自由（選択できる状態）: [Does this increase Kento's freedom?]
- 精神的安定: [Does this support or threaten mental stability?]
- 評価されるものづくり: [Is this something that creates recognized value?]

## Next Step (if approved Sunday)
[One concrete action to move from idea to validation]
```

### Step 4: Generate timeline.json

Write `projects/emerging-projects/YYYY-MM-DD-[name]/timeline.json`:

```json
{
  "project_name": "[Name]",
  "created": "YYYY-MM-DD",
  "status": "emerging",
  "phases": [
    {
      "phase": "Validation",
      "description": "Confirm the idea has legs",
      "actions": [
        "Research existing solutions",
        "Talk to 2-3 potential users"
      ],
      "depends_on": []
    },
    {
      "phase": "MVP Definition",
      "description": "Define minimum viable scope",
      "actions": [
        "Write 1-page spec",
        "Identify tech stack"
      ],
      "depends_on": ["Validation"]
    },
    {
      "phase": "Build",
      "description": "Create first version",
      "actions": [],
      "depends_on": ["MVP Definition"]
    }
  ],
  "sunday_review_date": "YYYY-MM-DD (next Sunday)",
  "decision": null
}
```

### Step 5: Generate questions.md

Write `projects/emerging-projects/YYYY-MM-DD-[name]/questions.md`:

```markdown
# Open Questions - [Project Name]

## Must Answer Before Starting
1. [Critical unknown #1]
2. [Critical unknown #2]

## Nice to Know
1. [Helpful but not blocking]

## Research Needed
- [ ] [Specific research task]
- [ ] [Market/competitor check]

## People to Talk To
- [ ] [Person and why]
```

### Step 6: Dependency Mapping

Scan existing projects and flag connections:

```
Existing Projects:
├── tokoro-era/          → [Related? How?]
├── note-publication/    → [Could this become Note content?]
├── recruit-transition/  → [Uses Recruit skills?]
├── property-hunt/       → [Property-related?]
└── independence-plan/   → [Supports independence timeline?]
```

Add dependency notes to `brief.md` under "Dependencies on Existing Projects".

### Step 7: Git Commit

```bash
git add "projects/emerging-projects/${TODAY}-${PROJECT_SLUG}/"
git commit -m "Emerging project: ${PROJECT_SLUG}"
```

### Step 8: Notify

Output to Kento:
```
Emerging project created: [name]
Location: projects/emerging-projects/YYYY-MM-DD-[name]/
Status: 日曜レビュー待ち

Sunday review で優先度を決めましょう。
それまでは、気になることがあれば questions.md に追記してください。
```

## Sunday Review Integration

During Sunday weekly review (see CLAUDE.md), all emerging projects are reviewed:

1. List all directories in `projects/emerging-projects/`
2. For each, read `brief.md` and present summary
3. Ask Kento to decide:
   - **Promote** → Move to `projects/[name]/` as official project
   - **Hold** → Keep in emerging, review next week
   - **Archive** → Move to `projects/emerging-projects/_archived/`
   - **Kill** → Delete (with confirmation)

Update `timeline.json` with the decision:
```json
{
  "decision": "promote",
  "decision_date": "2026-02-09",
  "reason": "Aligns with tokoro/ERA guest experience goals"
}
```

## Guard Rails

- **Do not pressure Kento to act on ideas immediately.** The whole point is: capture now, decide Sunday.
- **Do not over-formalize.** If Kento gives a one-sentence idea, the brief should be short too. Match the depth of his input.
- **Watch for idea overload.** If 3+ ideas emerge in one week, flag during Sunday review: "今週3つ新しいアイデアが出ています。優先度を絞りましょう。"
- **Check value alignment.** If an idea conflicts with 精神的安定 (e.g., too much scope, too many commitments), flag it gently.

## Example

```
Kento: "あ、Recruiter向けプロダクト知見と古民家民泊の体験を組み合わせて、
       民泊オーナー向けの『内装シミュレーターアプリ』作ってみたいな"

Claude: "面白いですね。構造化して保存しますか？"

Kento: "うん、お願い"

Claude: "3つだけ聞かせてください。
        1. きっかけは何ですか？
        2. 誰が使う想定？
        3. tokoro/ERAの運営とどう繋がりますか？"

Kento: "市原の内装決めるとき、完成イメージが湧かなくて困ったのがきっかけ。
       同じ悩み持つ民泊オーナーは多いと思う。
       tokoroの実績データを使えば、実際の改装コストとリターンも出せる。"

Claude: "プロジェクトを構造化しました。

        Emerging project created: interior-simulator-app
        Location: projects/emerging-projects/2026-02-05-interior-simulator-app/
        Status: 日曜レビュー待ち

        Dependencies:
        - tokoro-era: 改装実績データを活用
        - recruit-transition: UXデザインスキルを応用
        - note-publication: 開発過程を記事化できる可能性あり

        Sunday review で優先度を決めましょう。"
```

## File References

- Output directory: `projects/emerging-projects/YYYY-MM-DD-[name]/`
- Files created: `brief.md`, `timeline.json`, `questions.md`
- Context: `core/life-context.json`
- Existing projects: `projects/` (all subdirectories)
