# データフォーマット仕様書

このドキュメントでは、ディベートフローシートアプリのデータフォーマット（JSON）の仕様を定義します。将来的に他のディベートフローアプリやNADE公式アプリが登場した際、データを容易に移行できるよう、キー構造と対応表を記載しています。

## 📋 目次

- [基本方針](#基本方針)
- [データ構造](#データ構造)
- [JSONキー対応表](#jsonキー対応表)
- [移行ガイド](#移行ガイド)
- [バージョン管理](#バージョン管理)

---

## 基本方針

### 設計思想

1. **シンプルで汎用的な構造** - 他のアプリへの移行を容易にするため、可能な限りシンプルな構造を採用
2. **人間が読める形式** - JSONフォーマットを採用し、テキストエディタで確認・編集可能
3. **拡張性** - 将来的な機能追加に対応できる構造
4. **明確なキー名** - キー名は英語で記述し、意味が明確

### ファイル名規則

```
debate-flow-YYYYMMDD--<論題>-<肯定側>-<否定側>.json
```

例: `debate-flow-20241221--首相公選制-A高校-B高校.json`

---

## データ構造

### 完全なJSON構造（1CON形式の例）

```json
{
  "meta": {
    "topic": "日本は首相公選制を導入すべきである。是か非か",
    "affTeam": "A高校",
    "negTeam": "B高校",
    "dateTime": "2025/12/21",
    "author": "ジャッジ名"
  },
  "verdict": {
    "affVotes": "2",
    "negVotes": "1",
    "winner": "aff"
  },
  "judgeComments": "講評コメント...",
  "commPoints": {
    "aff": {
      "const": "5",
      "cx": "4",
      "response": "5",
      "1r": "4",
      "2r": "5",
      "penalty": "0"
    },
    "neg": {
      "const": "4",
      "cx": "4",
      "response": "4",
      "1r": "4",
      "2r": "4",
      "penalty": "-1"
    }
  },
  "columns": {
    "aff-const": "# メリット1: 経済成長\nGDP向上により雇用が増加する",
    "neg-cx": "質疑内容...",
    "neg-const": "# デメリット1: 政治の不安定化\n...",
    "aff-cx": "...",
    "neg-1r": "...",
    "aff-1r": "...",
    "aff-1r-neg": "...",
    "neg-2r": "...",
    "neg-2r-neg": "...",
    "aff-2r": "...",
    "aff-2r-neg": "..."
  }
}
```

### 完全なJSON構造（2CON形式の例）

```json
{
  "meta": {
    "topic": "日本は首相公選制を導入すべきである。是か非か",
    "affTeam": "C大学",
    "negTeam": "D大学",
    "dateTime": "2025/12/21",
    "author": "ジャッジ名"
  },
  "verdict": {
    "affVotes": "3",
    "negVotes": "0",
    "winner": "aff"
  },
  "judgeComments": "講評コメント...",
  "commPoints": {
    "aff": {
      "const1": "5",
      "const2": "5",
      "cx1": "4",
      "cx2": "5",
      "response1": "5",
      "response2": "4",
      "1r": "5",
      "2r": "5",
      "penalty": "0"
    },
    "neg": {
      "const1": "4",
      "const2": "4",
      "cx1": "4",
      "cx2": "4",
      "response1": "4",
      "response2": "4",
      "1r": "4",
      "2r": "4",
      "penalty": "0"
    }
  },
  "columns": {
    "aff-1const": "# メリット1...",
    "neg-1cx": "...",
    "neg-1const-aff": "...",
    "neg-1const-neg": "...",
    "aff-1cx-aff": "...",
    "aff-1cx-neg": "...",
    "aff-2const-aff": "...",
    "aff-2const-neg": "...",
    "neg-2cx-aff": "...",
    "neg-2cx-neg": "...",
    "neg-2const-aff": "...",
    "neg-2const-neg": "...",
    "aff-2cx-aff": "...",
    "aff-2cx-neg": "...",
    "neg-1r-aff": "...",
    "neg-1r-neg": "...",
    "aff-1r-aff": "...",
    "aff-1r-neg": "...",
    "neg-2r-aff": "...",
    "neg-2r-neg": "...",
    "aff-2r-aff": "...",
    "aff-2r-neg": "..."
  }
}
```

---

## JSONキー対応表

### トップレベルキー

| キー | 型 | 説明 | 必須 |
|------|------|------|------|
| `meta` | Object | 試合のメタ情報 | ✅ |
| `verdict` | Object | 判定結果 | ✅ |
| `judgeComments` | String | ジャッジの講評コメント | ✅ |
| `commPoints` | Object | コミュニケーション点 | ✅ |
| `columns` | Object | 各スピーチの内容 | ✅ |

### `meta` オブジェクト

| キー | 型 | 説明 | 日本語名 |
|------|------|------|----------|
| `topic` | String | 論題 | 論題 |
| `affTeam` | String | 肯定側チーム名 | 肯定側 |
| `negTeam` | String | 否定側チーム名 | 否定側 |
| `dateTime` | String | 試合日時（形式: YYYY/MM/DD） | 日時 |
| `author` | String | 記入者名（ジャッジ名など） | 記入者 |

### `verdict` オブジェクト

| キー | 型 | 説明 | 値の例 |
|------|------|------|--------|
| `affVotes` | String | 肯定側の票数 | "2", "3" |
| `negVotes` | String | 否定側の票数 | "1", "0" |
| `winner` | String | 勝者（"aff" または "neg"） | "aff", "neg" |

### `commPoints` オブジェクト

#### 1CON形式

| キー | 型 | 説明 | 日本語名 |
|------|------|------|----------|
| `aff.const` | String | 肯定側立論のコミュ点（1-5） | 立論 |
| `aff.cx` | String | 肯定側質疑のコミュ点（1-5） | 質疑 |
| `aff.response` | String | 肯定側応答のコミュ点（1-5） | 応答 |
| `aff.1r` | String | 肯定側第1反駁のコミュ点（1-5） | 第1反駁 |
| `aff.2r` | String | 肯定側第2反駁のコミュ点（1-5） | 第2反駁 |
| `aff.penalty` | String | 肯定側の減点（0, -1, -2...） | 減点 |
| `neg.const` | String | 否定側立論のコミュ点（1-5） | 立論 |
| `neg.cx` | String | 否定側質疑のコミュ点（1-5） | 質疑 |
| `neg.response` | String | 否定側応答のコミュ点（1-5） | 応答 |
| `neg.1r` | String | 否定側第1反駁のコミュ点（1-5） | 第1反駁 |
| `neg.2r` | String | 否定側第2反駁のコミュ点（1-5） | 第2反駁 |
| `neg.penalty` | String | 否定側の減点（0, -1, -2...） | 減点 |

#### 2CON形式

| キー | 型 | 説明 | 日本語名 |
|------|------|------|----------|
| `aff.const1` | String | 肯定側第1立論のコミュ点（1-5） | 立論1 |
| `aff.const2` | String | 肯定側第2立論のコミュ点（1-5） | 立論2 |
| `aff.cx1` | String | 肯定側第1質疑のコミュ点（1-5） | 質疑1 |
| `aff.cx2` | String | 肯定側第2質疑のコミュ点（1-5） | 質疑2 |
| `aff.response1` | String | 肯定側第1応答のコミュ点（1-5） | 応答1 |
| `aff.response2` | String | 肯定側第2応答のコミュ点（1-5） | 応答2 |
| `aff.1r` | String | 肯定側第1反駁のコミュ点（1-5） | 第1反駁 |
| `aff.2r` | String | 肯定側第2反駁のコミュ点（1-5） | 第2反駁 |
| `aff.penalty` | String | 肯定側の減点（0, -1, -2...） | 減点 |
| `neg.*` | String | 否定側も同様の構造 | - |

### `columns` オブジェクト（スピーチ内容）

#### 1CON形式のカラムID

| カラムID | スピーチ名 | 省略形 | 配置 |
|----------|------------|--------|------|
| `aff-const` | 肯定側立論 | AC | 上段 |
| `neg-cx` | 否定側質疑 | NQ | 上段 |
| `neg-const` | 否定側立論 | NC | 下段 |
| `aff-cx` | 肯定側質疑 | AQ | 下段 |
| `neg-1r` | 否定側第1反駁 | 1NR | 上段 |
| `aff-1r` | 肯定側第1反駁 | 1AR | 上段 |
| `aff-1r-neg` | 肯定側第1反駁（否定側の議論） | 1AR | 下段 |
| `neg-2r` | 否定側第2反駁 | 2NR | 上段 |
| `neg-2r-neg` | 否定側第2反駁（否定側の議論） | 2NR | 下段 |
| `aff-2r` | 肯定側第2反駁 | 2AR | 上段 |
| `aff-2r-neg` | 肯定側第2反駁（否定側の議論） | 2AR | 下段 |

#### 2CON形式のカラムID

| カラムID | スピーチ名 | 省略形 | 配置 |
|----------|------------|--------|------|
| `aff-1const` | 肯定側第1立論 | 1AC | 上段のみ |
| `neg-1cx` | 否定側第1質疑 | 1NQ | 上段のみ |
| `neg-1const-aff` | 否定側第1立論（肯定側の議論） | 1NC | 上段 |
| `neg-1const-neg` | 否定側第1立論（否定側の議論） | 1NC | 下段 |
| `aff-1cx-aff` | 肯定側第1質疑（肯定側の議論） | 1AQ | 上段 |
| `aff-1cx-neg` | 肯定側第1質疑（否定側の議論） | 1AQ | 下段 |
| `aff-2const-aff` | 肯定側第2立論（肯定側の議論） | 2AC | 上段 |
| `aff-2const-neg` | 肯定側第2立論（否定側の議論） | 2AC | 下段 |
| `neg-2cx-aff` | 否定側第2質疑（肯定側の議論） | 2NQ | 上段 |
| `neg-2cx-neg` | 否定側第2質疑（否定側の議論） | 2NQ | 下段 |
| `neg-2const-aff` | 否定側第2立論（肯定側の議論） | 2NC | 上段 |
| `neg-2const-neg` | 否定側第2立論（否定側の議論） | 2NC | 下段 |
| `aff-2cx-aff` | 肯定側第2質疑（肯定側の議論） | 2AQ | 上段 |
| `aff-2cx-neg` | 肯定側第2質疑（否定側の議論） | 2AQ | 下段 |
| `neg-1r-aff` | 否定側第1反駁（肯定側の議論） | 1NR | 上段 |
| `neg-1r-neg` | 否定側第1反駁（否定側の議論） | 1NR | 下段 |
| `aff-1r-aff` | 肯定側第1反駁（肯定側の議論） | 1AR | 上段 |
| `aff-1r-neg` | 肯定側第1反駁（否定側の議論） | 1AR | 下段 |
| `neg-2r-aff` | 否定側第2反駁（肯定側の議論） | 2NR | 上段 |
| `neg-2r-neg` | 否定側第2反駁（否定側の議論） | 2NR | 下段 |
| `aff-2r-aff` | 肯定側第2反駁（肯定側の議論） | 2AR | 上段 |
| `aff-2r-neg` | 肯定側第2反駁（否定側の議論） | 2AR | 下段 |

---

## 移行ガイド

### 他のアプリへデータを移行する場合

将来的に新しいディベートフローアプリが登場した場合、以下の手順でデータを移行できます。

#### ステップ1: JSONファイルを確認

1. 本アプリで「💾 保存」ボタンからJSONファイルをダウンロード
2. テキストエディタ（メモ帳、VS Codeなど）でJSONファイルを開く
3. 上記のキー対応表を参照し、必要なデータを確認

#### ステップ2: データ変換スクリプトの作成

新しいアプリのフォーマットに合わせて、PythonやJavaScriptで変換スクリプトを作成できます。

**Python例:**

```python
import json

# 本アプリのJSONファイルを読み込む
with open('debate-flow-20241221--首相公選制-A高校-B高校.json', 'r', encoding='utf-8') as f:
    data = json.load(f)

# 新しいアプリのフォーマットに変換
new_format = {
    "topic": data["meta"]["topic"],
    "teams": {
        "affirmative": data["meta"]["affTeam"],
        "negative": data["meta"]["negTeam"]
    },
    "speeches": {
        "AC": data["columns"].get("aff-const", ""),
        "NC": data["columns"].get("neg-const", ""),
        # ... 必要に応じて追加
    }
}

# 新しい形式で保存
with open('converted.json', 'w', encoding='utf-8') as f:
    json.dump(new_format, f, ensure_ascii=False, indent=2)
```

#### ステップ3: 手動変換

簡単なケースであれば、JSONファイルを直接編集して新しいフォーマットに変換できます。

---

## バージョン管理

### 現在のバージョン: 1.0.0

将来的にデータフォーマットに互換性のない変更が発生した場合、JSONファイルに `version` フィールドを追加する予定です。

```json
{
  "version": "1.0.0",
  "meta": { ... },
  ...
}
```

---

## よくある質問

### Q: なぜカラムIDが `-aff` / `-neg` で終わるものがあるのか？

A: 2行レイアウト（上段・下段）を採用しているため、同じスピーチでも「肯定側の議論」と「否定側の議論」を分けて記録する必要があります。`-aff` サフィックスは上段（肯定側の議論）、`-neg` サフィックスは下段（否定側の議論）を表します。

### Q: ブロック記法（`#`）や参照記法（`>`）はどのように保存されるか？

A: `columns` オブジェクトの各フィールドにプレーンテキストとして保存されます。マークダウン記法はそのまま文字列として保持されるため、他のアプリでもテキストとして扱えます。

### Q: データを Excel に移行できるか？

A: はい。JSONファイルをPythonやJavaScriptで読み込み、CSVに変換することで Excel で開けます。ただし、構造化されたデータのため、スプレッドシートへの変換時にレイアウトを調整する必要があります。

---

## サポート

データ移行に関する質問や問題がある場合は、GitHubリポジトリの [Issues](https://github.com/mikisayaka19/debate-flowsheet/issues) で報告してください。
