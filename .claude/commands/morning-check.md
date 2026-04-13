# 朝の自動チェック実行

fカンパニーのモーニングルーティンを確認・実行する手順。

## 概要

Morning Reporterが担当する朝の定期チェックの確認と手動実行。

## 確認項目

1. **GAS実行状況**: dailyAutoUpdate が正常に実行されたか確認
   - GASコンソールの実行ログを確認
   - エラー通知メールの有無を確認

2. **Wiki更新状況**: ei-wiki / denken-wiki の最新デプロイを確認
   - `gh run list --repo kfurufuru/ei-wiki --limit 3`
   - `gh run list --repo kfurufuru/denken-wiki --limit 3`

3. **Notion連携**: タスク・学習進捗の同期状況を確認

4. **Make.comシナリオ**: 自動化シナリオの実行履歴を確認

## 手動実行

GASスクリプトを手動実行する場合:
1. GASコンソールで対象プロジェクトを開く
2. `dailyAutoUpdate` 関数を選択
3. 「実行」ボタンをクリック
4. 実行ログで結果を確認

## 異常時の対応

- GASエラー → `/check-gas` コマンドで詳細確認
- デプロイ失敗 → `/deploy-wiki` コマンドで確認
- 連携エラー → Make.comダッシュボードで実行履歴を確認
