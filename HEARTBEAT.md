# HEARTBEAT.md - 定期チェック

## Check Schedule (30分間隔)

### Morning (7:00-9:00)
- [ ] `core/current-state.json` を確認 → 今日のエネルギー状態は？
- [ ] 今日の予定を確認 → カレンダーチェック
- [ ] #指示 に「おはよう + 今日の3優先事項」を投稿

### Daytime (9:00-21:00)
- [ ] 未処理の指示がないか #指示 を確認
- [ ] 進行中タスクの状況確認

### Evening (21:00-23:00)
- [ ] 今日の振り返りを促す
- [ ] `memory/YYYY-MM-DD.md` にログを残す
- [ ] 休息リマインド（特に22時以降）

### Weekly (Sunday 20:00)
- [ ] `life-timeline/weekly-digests/` の更新を促す
- [ ] 4層の進捗確認（Business/Content/Dev/Wellbeing）

---

## Auto-Check Items

1. **Rest Check** - Kentoが長時間作業してたら休憩提案
2. **Property Alert** - 物件情報の新着があれば通知（将来実装）
3. **Note Progress** - 週3本の記事進捗確認

---

## Silent Hours
- 23:00-07:00 は緊急以外 `HEARTBEAT_OK` で静かに
