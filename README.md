# 📝 Debate Flowsheet

[![GitHub Stars](https://img.shields.io/github/stars/mikisayaka19/debate-flowsheet?style=flat&logo=github)](https://github.com/mikisayaka19/debate-flowsheet/stargazers)
[![GitHub Forks](https://img.shields.io/github/forks/mikisayaka19/debate-flowsheet?style=flat&logo=github)](https://github.com/mikisayaka19/debate-flowsheet/network/members)
[![Last Commit](https://img.shields.io/github/last-commit/mikisayaka19/debate-flowsheet?style=flat)](https://github.com/mikisayaka19/debate-flowsheet/commits/main)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Demo](https://img.shields.io/badge/demo-GitHub%20Pages-blue?style=flat&logo=github)](https://mikisayaka19.github.io/debate-flowsheet/)
[![Download](https://img.shields.io/badge/download-Latest%20Release-brightgreen?style=flat&logo=github)](https://github.com/mikisayaka19/debate-flowsheet/releases/latest)

オフラインで動作するディベートフローシートアプリ（NADE非公式）

![メイン画面](screenshots/001.png)


## 📖 概要

ディベート試合のフロー記録に特化したWebアプリです。

### 🎯 ディベートフォーマット

- **1CON形式** - 1立論形式（中学・高校ディベート） ✅ 利用可能
- **2CON形式** - 2立論形式（大学・社会人ディベート） ✅ 利用可能

## 👉 デモページ
🔗 [https://mikisayaka19.github.io/debate-flowsheet/](https://mikisayaka19.github.io/debate-flowsheet/)

ブラウザで直接お試しいただけます。フロー内容はローカルで完結しサーバーに送信されません。


## ✨ 特徴

- **通信不要** - オフライン/PCブラウザのローカルで動作が完結。外部に漏れる心配なく、一般的なディベートのルール「通信の禁止」に抵触しません。
- **インターネット不要** - 上のデモページからではなく、あらかじめHTMLファイルをお手持ちのPCにダウンロードすることで、インターネット通信せずにアプリを動作できます。
- **追加アプリ不要** - PCのブラウザで開くだけでアプリが使えるため、別途アプリやツールをインストールする必要はありません。ディベートフローアプリ自体は単一のHTMLファイルであり、外部依存はありません。
- **タイマー・判定・評価機能** - ジャッジやタイムキーパー向けに、タイマー機能、勝敗判定、コミュニケーション点、講評の記録が可能です。
- **データ保存/読込** - フロー記録をエクスポート/インポートできます。フォーマットは以下理由により、シンプルで汎用的な形式であるJSONを採用しています。
   - **高い移植性** - 将来的に他のディベートフローアプリやNADE公式アプリが登場した際も、データ変換が容易です。データ変換の詳細は [DATA_FORMAT.md](DATA_FORMAT.md) をご覧ください。
   - **AI活用** - JSONはAI (LLM) と相性が良い形式であり、将来的にAI活用する際に便利です。
- **試合結果出力** - 試合結果を、テキスト（`.txt`）かマークダウン（`.md`）で出力可能です。
- **論点と論点を繋げる** - `#` マークダウン記法でブロックを定義し、`>` 記法で参照が可能です。
- **ダークモード対応** - ライト/ダークテーマを切り替えることができます。


## 🚀 使い方

### 🌐 アクセス方法

#### 💻 オフライン利用（インターネット不要・通信禁止ルール対応）

**📥 最新版のダウンロード**: [Releases](https://github.com/mikisayaka19/debate-flowsheet/releases/latest)

1. 上記リンクから使用したい形式のHTMLファイルをダウンロード
   - **debate-flowsheet-1con.html** - 1立論形式（中学・高校ディベート）
   - **debate-flowsheet-2con.html** - 2立論形式（大学・社会人ディベート）
2. ダウンロードしたHTMLファイルをダブルクリック
3. ブラウザが開いたら、すぐに使用開始

#### 🌐 オンライン（GitHub Pages）
1. https://mikisayaka19.github.io/debate-flowsheet/ にアクセス
2. 使用したい形式（1CON/2CON）を選択
3. アプリが起動

ブラウザで直接お試しいただけます。フロー内容はローカルで完結しサーバーに送信されません。

### 💡 基本的な使用方法

1. 論題、チーム名、日時、記入者を入力
2. ディベートの進行に合わせて各列に記録
3. 【応用】ブロック記法（`#`）で議論を構造化
4. 【応用】参照記法（`>`）でブロック間の関連を記録
5. 試合終了後、判定・評価を記入
6. 「データを保存」でJSONファイルとしてダウンロード

### 🔗 【応用】論点と論点を繋げる際の記法
できる限りシンプルな作りのアプリにするため、フローの矢印機能は実装していません。

ただし、以下のブロック記法で、**論点と論点を繋げる**ことができます。


#### 📌 ブロックの定義
```
# 経済成長のメリット
GDP向上により雇用が増加する
```
`#` で始まる行が新しいブロックを作成します。各ブロックには位置ベースのID（AC-0、AC-1...）が自動的に割り当てられます。

#### 🔀 ブロック参照
```
> AC-0
この反論は肯定側立論の経済成長メリットに対するものです
```
`> AC-0` または、`> ac-0`のように記述すると、該当ブロックへのクリック可能なリンクが生成されます。

![論点参照](screenshots/002.png)

## 📋 省略記号について

### 🏷️ 1立論形式（1con）
- **AC** - 肯定側立論
- **NQ** - 否定側質疑
- **NC** - 否定側立論
- **AQ** - 肯定側質疑
- **1NR** - 否定側第1反駁
- **1AR** - 肯定側第1反駁
- **2NR** - 否定側第2反駁
- **2AR** - 肯定側第2反駁

### 🏷️ 2立論形式（2con）
- **1AC** - 肯定側第1立論
- **1NQ** - 否定側第1質疑
- **1NC** - 否定側第1立論
- **1AQ** - 肯定側第1質疑
- **2AC** - 肯定側第2立論
- **2NQ** - 否定側第2質疑
- **2NC** - 否定側第2立論
- **2AQ** - 肯定側第2質疑
- **1NR** - 否定側第1反駁
- **1AR** - 肯定側第1反駁
- **2NR** - 否定側第2反駁
- **2AR** - 肯定側第2反駁


## 💾 データの保存と読込

- **保存**: 「データを保存」ボタンをクリックし、JSON形式でダウンロード
- **読込**: 「データを読込」ボタンをクリックし、保存したJSONファイルを選択

ファイル名形式: `debate-flow-YYYYMMDD--<論題>-<肯定側>-<否定側>.json`

## 📤 出力形式

「フローシートを出力」ボタンから以下の形式でエクスポート可能:
- **Markdown** (.md) - 構造化された読みやすい形式
- **テキスト** (.txt) - プレーンテキスト形式

## 🛠️ 技術仕様

- **HTML5** + **CSS3** + **Vanilla JavaScript**
- フレームワーク不使用
- 外部CDN依存なし
- システムフォント使用
- LocalStorage（テーマ設定のみ）


## 🔒 プライバシー

このアプリケーションは:
- ✅ 完全オフラインで動作
- ✅ データを外部に送信しない
- ✅ トラッキングなし
- ✅ 外部リソース読み込みなし

ディベート大会の通信禁止ルールに完全準拠しています。

## 🌍 ブラウザ対応

モダンブラウザの最新版を推奨:
- Google Chrome
- Microsoft Edge
- Mozilla Firefox
- Safari

## 📜 ライセンス

MIT License - 詳細は [LICENSE](LICENSE) をご覧ください。

## ⚠️ 免責事項

このアプリケーションは無保証で提供されます。以下の点にご注意ください：

- **データ損失のリスク**: ブラウザのクラッシュ、誤操作、端末の不具合等により、記録したフローシートのデータが失われる可能性があります
- **保存の推奨**: 重要な試合の記録は、こまめに「💾 保存」ボタンでJSONファイルとしてダウンロードすることを強く推奨します
- **動作保証なし**: すべてのブラウザ・OS環境での完全な動作を保証するものではありません
- **責任の範囲**: このアプリケーションの使用により生じたいかなる損害（フロー記録の損失、試合結果への影響等）についても、開発者は一切の責任を負いません

**使用前の確認事項:**
- ✅ 試合開始前に動作確認を行ってください
- ✅ 定期的にデータ保存を行ってください
- ✅ 重要な試合では予備の記録手段を用意してください

本アプリケーションは、あくまでディベート活動を支援するための補助ツールです。自己責任のもとでご使用ください。