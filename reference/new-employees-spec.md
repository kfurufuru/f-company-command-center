# AI エージェント仕様書（新規参加者向け）

**最終更新**: 2026-04-20 | **バージョン**: v1.3 Fix 2・Fix 5 適用済み

---

## AI Reviewer

| 項目 | 内容 |
|------|------|
| 役割 | 成果物検証・品質判断（AI Architect完成後に稼働） |
| 設計パターン | Context-aware |
| 配置 | グローバル（`~/.claude/skills/`） |
| 状態 | 未実装 |

### allowed-tools（Fix 2）

```
Read, Write, Glob, Grep, Bash
```

**禁止**: WebFetch は使用不可。Write はレポート出力専用で `.claude/reviews/` 配下に限定。

---

## Morning Reporter

| 項目 | 内容 |
|------|------|
| 役割 | 定時出力専門 |
| 設計パターン | Sequential |
| 配置 | グローバル（`~/.claude/skills/`） |
| 状態 | GASで稼働中 |

### 責務境界（Fix 5）

- レポート内容生成に専念する
- **異常検知時**: `「GAS異常あり。詳細: gas-monitor参照」` の1行のみ出力
- 診断には介入しない。GAS Monitor に委ねる

---

## GAS Monitor

| 項目 | 内容 |
|------|------|
| 役割 | GAS異常検知・修正提案（診断専門） |
| 設計パターン | Context-aware |
| 配置 | ローカル（`f-company-command-center/.claude/skills/`） |
| 状態 | 未実装 |

### 責務境界（Fix 5）

- 診断結果のみ出力する
- Morning Reporter のレポート内容（出力テキスト・フォーマット）には関与しない

---

## 責務境界サマリー

```
Morning Reporter ─── レポート内容生成 ──→ 出力
                │
                └─（異常検知）→ 「GAS異常あり。詳細: gas-monitor参照」の1行
                                        │
                              GAS Monitor ── 診断・修正提案
```

Morning Reporter と GAS Monitor は互いの出力内容に干渉しない。
