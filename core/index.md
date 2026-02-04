# Core Index - Life Dashboard Navigation

## ファイル構造ガイド

### 🔑 常時参照（毎回読む）
- `life-context.json`: 役割・目標・価値観
- `current-state.json`: 今日のエネルギー・フォーカス

### 📁 毎日更新
- `life-timeline/daily-logs/YYYY-MM-DD.md`: 朝晩の音声記録

### 📊 毎週更新
- `life-timeline/weekly-digests/YYYY-Www.md`: 日曜夜の自動レビュー
- `core/current-state.json`: 週の初めに更新

### 🏢 ビジネス関連
- `projects/tokoro-era/`: ホテル事業
  - `brief.md`: 概要
  - `2026-targets.json`: KPI目標
  - `operational-metrics.json`: 現在の実績
  - `property-hunt/`: 物件探しログ
- `projects/note-publication/`: 執筆活動（architecture-of-life リポから統合）
- `projects/recruit-transition/`: リクルート退職準備

### 📝 プロジェクト管理
- `projects/emerging-projects/`: 新規アイデア蓄積
- `projects/independence-plan/`: 独立計画（留学含む）

### 📈 メトリクス
- `metrics/tokoro-era.json`: 事業KPI
- `metrics/content-performance.json`: Note記事パフォーマンス
- `metrics/wellbeing.json`: ランニング・睡眠・精神状態

### 🤖 Claude連携
- `.claude/CLAUDE.md`: メイン指示書（まだ未作成）
- `.claude/skills/`: スキル定義
- `.claude/workflows/`: ワークフロー定義

---

## 使い方フロー

### 朝（7:00-8:00）
1. `current-state.json` を開く
2. 今日のエネルギー・フォーカスを確認
3. Claude に「今日の3優先事項は？」と聞く

### 夜（22:00-23:00）
1. `daily-logs/` に今日のレビュー音声を記録
2. 自動テキスト化される

### 日曜（20:00）
1. `weekly-digest` が自動生成される
2. 4レイヤー（Business/Content/Development/Wellbeing）をレビュー

---

## 次のステップ
- [ ] `.claude/CLAUDE.md` 作成
- [ ] `.claude/skills/` 実装
- [ ] Mac Dictation 連携テスト
- [ ] GitHub プッシュ