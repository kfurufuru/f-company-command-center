# f-company-command-center

fカンパニーの司令塔リポジトリ。AI社員チームによる業務自動化を統括する。

## プロジェクト概要

- **リポジトリ**: kfurufuru/f-company-command-center
- **目的**: 個人AI活用プロジェクト「fカンパニー」の自動化ハブ
- **運営者**: ふるたち
- **ポータル**: `.secretary/portal-v2.html`（Fカンパニーの各種ツールへのリンク集）

## 現状

⚠️ **このリポジトリはClaude Code設定のみ存在。git未初期化、実装コード未作成。**

## 技術スタック

| レイヤー | 技術 |
|---------|------|
| 自動化スクリプト | Google Apps Script（GAS） |
| ワークフロー | Make.com |
| ナレッジ・タスク | Notion |
| メール・カレンダー | Gmail / Google Calendar |
| AI開発 | Claude Code（Skill実装） |
| CI/CD | GitHub Actions |

## AI社員チーム

### 稼働中

| AI社員 | 業務 | 実装 |
|--------|------|------|
| Morning Reporter | 朝の定期レポート配信 | GAS時間トリガー |
| Wiki Editor | ei-wiki / denken-wiki コンテンツ管理 | Claude Code |
| Study Coach | 電験3種学習進捗管理 | Claude Code + Notion |

### 計画中

| AI社員 | 業務 | 実装予定 |
|--------|------|---------|
| Inbox Manager | メール分類→対応提案 | Claude Code Skill + Gmail API |
| Schedule Optimizer | カレンダー最適化 | Claude Code Skill + GCal |
| Code Reviewer | PR自動レビュー | Claude Code Skill + GitHub |

### AI社員の実装方針
- 1社員 = 1 Claude Code Skill（Single Responsibility）
- 起動: スケジュールタスク or スラッシュコマンド
- パイプライン: GASトリガー → Make.com → Claude Code Skill

## 計画ファイル構造

```
f-company-command-center/
├── CLAUDE.md
├── README.md               # プロジェクト概要（未作成）
├── gas/                    # GASスクリプト（未作成）
│   └── dailyAutoUpdate.gs
├── docs/                   # ドキュメント（未作成）
├── .github/workflows/      # CI/CD（未作成）
└── .claude/
    ├── commands/           # check-gas, morning-check
    └── rules/              # japanese-content
```

## GASスクリプト注意事項

- 時間トリガーでは `DocumentApp.getActiveDocument()` 使用不可 → `DocumentApp.openById('ID')` を使用
- Gemini API: 無料枠レート制限 2 RPM / 1500 RPD に注意
- APIキーは `PropertiesService` 経由で取得（ハードコード禁止）
- エラー通知メール受信時はGASコンソールで実行ログ確認

## コーディング規約

### GAS
- 関数名: キャメルケース（例: `dailyAutoUpdate`）
- 定数: 大文字スネークケース（例: `DOCUMENT_ID`）

### 共通
- ドキュメント: 日本語
- ブランチ: `feature/機能名` または `fix/修正内容`
- コミット: 日本語可。`add:`, `fix:`, `update:` プレフィックス推奨
- AI社員Skill名: ケバブケース（例: `inbox-manager`）

## .secretary連携

| 機能 | .secretary側 | 方向 |
|------|-------------|------|
| ポータルUI | `portal-v2.html` | 参照 |
| ペルソナ定義 | `personas/` | → AI社員の性格設定に利用 |
| スキル定義 | `skills/` | → Skill実装の参考 |
