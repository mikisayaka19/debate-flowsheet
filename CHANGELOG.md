# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Known Issues
- **2CON形式**: 横スクロール時にタイマーが隠れてしまう問題
  - 12列の横スクロールが必要な2CON形式では、スクロール時にヘッダー内のタイマーが画面外に移動する
  - ヘッダー固定化の実装が複雑なため、将来的な改善課題として記録

## [1.0.0] - 2025-12-28

### Added
- **1CON形式フローシート** - 1立論形式（中学・高校ディベート）対応
  - 8列構成（AC, NQ, NC, AQ, 1NR, 1AR, 2NR, 2AR）
  - 上段・下段の2行レイアウト
  - タイマー機能（肯定側・否定側別々）
  - コミュニケーション点記録（5項目：立論、質疑、応答、第1反駁、第2反駁）

- **2CON形式フローシート** - 2立論形式（大学・社会人ディベート）対応
  - 12列構成（1AC, 1NQ, 1NC, 1AQ, 2AC, 2NQ, 2NC, 2AQ, 1NR, 1AR, 2NR, 2AR）
  - 上段・下段の2行レイアウト
  - タイマー機能（肯定側・否定側別々）
  - コミュニケーション点記録（8項目：立論1, 立論2, 質疑1, 質疑2, 応答1, 応答2, 第1反駁, 第2反駁）

- **共通機能**
  - 完全オフライン動作（外部通信なし）
  - ブロック記法（`#`）による議論の構造化
  - 参照記法（`>`）によるブロック間リンク（例: `> AC-0`）
  - データ保存・読込（JSON形式）
  - 試合結果出力（Markdown / テキスト形式）
  - ダークモード・ライトモード切り替え
  - 判定・評価記録機能
  - 講評コメント機能

- **タイマー機能**
  - プリセットボタン（1分, 2分, 3分, 4分, 5分, 6分）
  - 警告表示（残り60秒以下で黄色、30秒以下で赤色）
  - 開始・停止・リセット機能

- **ランディングページ**
  - 形式選択画面（1CON / 2CON）
  - GitHub Pagesでのデモ提供

### Security
- XSS対策としてHTMLエスケープ処理を実装
- ユーザー入力のサニタイズ処理

### Documentation
- README.md（使い方、機能説明、ブロック記法の解説）
- スクリーンショット追加
- MIT License適用

[unreleased]: https://github.com/mikisayaka19/debate-flowsheet/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/mikisayaka19/debate-flowsheet/releases/tag/v1.0.0
