# Project Extractor Skill

Capture and structure Kento's new project ideas for Sunday review.

## Triggers

Detects when Kento mentions:
- `〜したいな` / `〜したい` / `〜作ってみたい`
- `〜やってみたい` / `〜できないかな`
- "I want to build..."

**Confirm before extracting**: "新しいプロジェクトアイデアっぽいですね。構造化して保存しますか？"

## Quick Reference

### Ask (Max 3 Questions)
1. "これ、何がきっかけ？" (origin)
2. "誰が使う想定？" (target user)
3. "今の事業とどう繋がる？" (dependency)

### Output Directory
```
projects/emerging-projects/YYYY-MM-DD-[name]/
├── brief.md      # Idea + Why Now + Dependencies
├── timeline.json # Phases
└── questions.md  # Unknowns
```

### brief.md Template
```markdown
# [Project Name]

**Created**: YYYY-MM-DD
**Status**: Emerging (未レビュー)
**Origin**: [Trigger]

## Core Idea
[2-3 sentences]

## Why Now
[Connection to current work]

## Dependencies
- Requires: [existing project/resource]
- Builds on: [skill from current role]

## Value Alignment
- 自由: [Does this increase freedom?]
- 精神的安定: [Does this support stability?]
- 評価されるものづくり: [Creates recognized value?]

## Next Step (if approved Sunday)
[One concrete action]
```

## Sunday Review

During weekly review, for each emerging project:
- **Promote** → Move to `projects/[name]/`
- **Hold** → Keep in emerging
- **Archive** → Move to `_archived/`
- **Kill** → Delete

## Guard Rails
- Don't pressure immediate action (capture now, decide Sunday)
- Match depth of Kento's input (short idea → short brief)
- Flag if 3+ ideas in one week: "優先度を絞りましょう"

## Git (Never Commit)
Emerging projects are in `.gitignore` until promoted.
