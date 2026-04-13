# GASスクリプト動作確認

Google Apps Scriptの動作状況を確認する手順。

## 手順

1. GASコンソール（https://script.google.com）で対象プロジェクトを開く
2. 「実行数」タブで最近の実行履歴を確認
3. エラーがある場合:
   - エラーメッセージを確認
   - 「The document is inaccessible」→ `openById()` を使用しているか確認
   - API quota exceeded → レート制限に達していないか確認
4. 時間トリガーの設定を確認（トリガータブ）

## よくあるエラーと対処

### "The document is inaccessible"
- 原因: 時間トリガーで `getActiveDocument()` を使用
- 対処: `DocumentApp.openById('ドキュメントID')` に変更

### "Quota exceeded"
- 原因: Gemini API 無料枠の上限超過（2 RPM / 1500 RPD）
- 対処: リトライ間隔を広げるか、課金プランに移行

### トリガーが実行されない
- 原因: トリガー設定の削除・無効化
- 対処: トリガータブで再設定
