# Node Small Tool

Node.jsでローカル実行する、小さなバッチ処理ツール集です。
CSV集計やテキスト処理などを通して、バッチ処理の構成を学習しています。

## 主な処理

| ツール | 内容 |
| --- | --- |
| CsvGroupByTool | CSVのグループ化・合計値の集計 |
| ParserOrMapper | `key=value` 形式のテキスト読み取り（変換処理は実装途中） |
| getJsonFromHttp | HTTP経由でのJSON取得 |

## ディレクトリ構成

```text
node_small_tool/
├── node-project/
│   ├── bin/
│   │   ├── index.js          # バッチのエントリーポイント
│   │   └── shell/            # 実行用シェルスクリプト
│   ├── config/
│   │   ├── config.example.json # 設定の雛形（Git管理対象）
│   │   └── config.json         # ローカル設定（Git管理対象外）
│   ├── data/                 # 入出力データ・サンプル
│   ├── lib/
│   │   ├── base/             # 共通処理・ログ出力
│   │   └── *.js              # 各ツールの処理
│   ├── logs/                 # 実行時に生成されるログ
│   ├── package.json
│   └── package-lock.json
└── readme.md
```

## 開発環境

- Node.js（組み込みの `fetch` を使用できるバージョン）
- npm
- Bash（シェルスクリプトを使用する場合）

## セットアップ

```sh
cd node-project
npm ci
cp config/config.example.json config/config.json
```

`config/config.json` のパスを実行環境や入力データに合わせて変更してください。
雛形の `rootPath` は `.` です。以下のコマンドはすべて `node-project/` 内で実行します。

## 設定項目

| キー | 用途 | 雛形の値 |
| --- | --- | --- |
| `rootPath` | 入出力パスの基準ディレクトリ | `.` |
| `csvGroupByToolFilePath` | CSV集計の入力ファイル | `data/csvGroupByTool/input.csv` |
| `csvGroupByToolOutputPath` | CSV集計の出力ファイル | `data/csvGroupByTool/output.csv` |
| `txtMapParserFilePath` | テキスト読み取りの入力ファイル | `data/txtMapParser/input.txt` |

入力・出力ファイルのパスは `rootPath` と結合されます。
実際の設定は `config.json` に記載し、共有する設定項目は `config.example.json` に反映します。

## 実行例

```sh
# CSVのグループ化・集計（出力先ファイルは上書きされます）
node bin/index.js csvGroupByTool

# key=value 形式のテキスト読み取り
node bin/index.js txtMapParser

# サンプルAPIからJSON取得（インターネット接続が必要です）
node bin/index.js getJsonFromHttp
```

処理経過はコンソールと `logs/app.log` に出力されます。
CSVの集計対象列は `lib/001_CsvGroupByTool.js` 内で定義しています。

## 開発状況

- テキスト変換処理は実装途中です。
- 自動テストは未整備です。
