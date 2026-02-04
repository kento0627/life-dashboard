# Kento's Life Dashboard

## 概要

人生全体を管理するための統合システム。4つのレイヤー（Business / Content / Development / Wellbeing）をバランスよく追跡・最適化する。
```
Life Dashboard
├── 🏢 Business Layer
│   ├── tokoro/ERA（古民家ホテル + 都市型民泊）
│   ├── Recruit Transition（今年末に退職予定）
│   └── Independence Plan（留学 → 再起業）
│
├── 📝 Content Layer
│   └── Architecture of Life（Note発信 3記事/週目標）
│
├── 🛠 Development Layer
│   └── Emerging Projects（新規アイデアの実験場）
│
└── 💪 Wellbeing Layer
    ├── Daily Running（2km × 1000+ days）
    ├── Sleep & Rest
    ├── Relationships（彼女・友達・母親）
    └── Mental Stability
```

---

## 使い方

### 🌅 朝のルーチン（7:00-8:00）

1. **ランニング後**（8:00-8:30）: Mac Dictation で昨日の振り返りを記録
```
   「昨日は〇〇をやった、学んだことは△△」
   → daily-logs/2026-02-04.md に自動保存される
```

2. **朝食後**（8:30-9:00）: Claude に「今日の3優先事項は？」と聞く
   - core/life-context.json と前日の daily-log を読んで提案
   - エネルギーレベルの確認

### 🌙 夜のルーチン（22:00-23:00）

1. **就寝前**: 今日のできたことと明日への intention を音声メモ
```
   「今日はNote記事50%進んだ、tokoro物件2件見た。明日は記事完成させる」
   → 自動テキスト化 & git commit
```

### 📊 日曜レビュー（20:00）

1. **週次レビュー自動生成**
   - 4レイヤーごとの進捗をサマリー
   - ボトルネック分析
   - 「ここは止まっても大丈夫」というメッセージ
   - 来週の3優先事項

---

## ファイル構造

### `core/` - 常時参照（毎回 <5KB）
- `life-context.json`: 役割・目標・価値観（週1更新）
- `current-state.json`: 今日のエネルギー・フォーカス（毎朝更新）
- `index.md`: 各ファイルのナビゲーション

### `life-timeline/`
- `daily-logs/`: 毎朝・毎晩の音声記録（毎日更新）
- `weekly-digests/`: 日曜の自動レビュー（週1更新）

### `projects/`
- `tokoro-era/`: ホテル事業（KPI・物件探し）
- `note-publication/`: 執筆活動（architecture-of-life リポから統合）
- `recruit-transition/`: リクルート退職準備
- `independence-plan/`: 独立計画（留学含む）
- `emerging-projects/`: 新規アイデア蓄積場

### `metrics/`
- `tokoro-era.json`: 事業KPI（月稼働率・売上・利益）
- `content-performance.json`: Note記事のパフォーマンス
- `wellbeing.json`: ランニング継続・睡眠・精神状態
- `independence-tracker.json`: 独立準備の進捗

### `.claude/`
- `skills/`: 再利用可能なSkill定義
  - `daily-logger/`: 音声 → テキスト化
  - `project-extractor/`: アイデア → プロジェクト化
  - `property-finder/`: 物件情報の評価・分類
- `workflows/`: 定期実行するワークフロー
  - `morning-intention.md`: 朝の優先事項提案
  - `daily-evening-log.md`: 夜のログ記録
  - `weekly-review.md`: 日曜の自動レビュー

---

## 実装状況

- [x] フォルダ構造
- [x] architecture-of-life リポ統合
- [x] core/ ファイル作成
- [ ] .claude/CLAUDE.md 作成
- [ ] .claude/skills/ 実装
- [ ] .claude/workflows/ 実装
- [ ] GitHub プッシュ

---

## GitHub 連携
```bash
# リモート設定（プライベート設定）
git remote add origin https://github.com/kento0627/life-dashboard.git
git branch -M main
git push -u origin main
```

毎朝・毎晩のコミットで、人生全体のコンテキストが蓄積される。