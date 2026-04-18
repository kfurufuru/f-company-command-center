---
description: "Google Apps Script開発ルール"
globs: "*.gs,*.js"
---

# GAS開発ルール

## 必須
- 時間トリガーでは getActiveDocument() / getActiveSpreadsheet() 禁止 → openById() 使用
- APIキーはスクリプトプロパティに保存。ハードコード禁止
- try-catch必須。エラー時はログ出力 + メール通知

## 命名
- 関数名: camelCase
- 定数: UPPER_SNAKE_CASE
- トリガー関数: on〜 または 〜Trigger

## 構造
- 1ファイル1機能（単一責任）
- 共通関数はutils.gsに集約
- 設定値はconfig.gsに分離
