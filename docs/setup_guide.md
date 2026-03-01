# このサイトの仕組みと構築手順

このページでは、この学習サイトをどのように作ったかを初心者向けに丁寧に解説します。
「次回また同じことをやりたい」「仕組みを理解したい」という場合の参考にしてください。

---

## 全体像：何を使って何を作ったか

```
あなたのPC（ローカル）          インターネット上
┌─────────────────┐            ┌──────────────────┐
│  Markdownファイル │  git push  │     GitHub       │
│  （勉強ノート）   │ ─────────> │  （ファイル保管） │
│                 │            │        ↓         │
│  MkDocs         │            │  GitHub Actions  │
│  （サイト変換）   │            │  （自動ビルド）   │
└─────────────────┘            │        ↓         │
                               │  GitHub Pages    │
                               │  （サイト公開）   │
                               └──────────────────┘
                                        ↓
                               スマホのブラウザでアクセス
```

**流れをひとことで言うと：**
Markdownで書いたノートを → MkDocsがサイトに変換 → GitHubが世界に公開

---

## 使ったツール・サービスの説明

### Markdown（マークダウン）とは

普通のテキストファイル（.md）に、簡単な記号でデザインを付ける書き方です。

```markdown
# 見出し1
## 見出し2

**太字**、*斜体*

- リスト1
- リスト2

| 列1 | 列2 |
|-----|-----|
| A   | B   |
```

HTMLやWordのように複雑な操作なしに、シンプルな記号だけで整ったドキュメントが書けます。
このサイトのノートや問題は全てMarkdownで書かれています。

---

### MkDocs（エムケードックス）とは

Markdownファイルを、スマホでも見やすいウェブサイトに変換するツールです。

- **Python製**（Pythonがあれば動く）
- `mkdocs serve` でローカルプレビュー
- `mkdocs build` でHTMLファイルを生成
- **Material テーマ**を使うことで、モバイル対応・検索・ダークモード・数式表示などが無料で使える

このサイトが使っている主な機能：

| 機能 | 使用箇所 |
|---|---|
| 数式レンダリング（MathJax） | $\bar{X}$、$\sigma^2$ などの数式表示 |
| 折りたたみブロック（Details） | 過去問の「解答・解説を見る」 |
| コールアウト（Admonition） | `!!! tip`、`!!! warning` などのボックス |
| 日本語検索 | 右上の検索バー |
| ダークモード | 右上のトグルボタン |

---

### Git（ギット）とは

**ファイルの変更履歴を管理するツール**です。

「いつ・何を・どう変えたか」を記録しておくことで：
- 間違えても前のバージョンに戻せる
- 変更をGitHubに送れる（push）

#### 使ったコマンドの説明

```bash
git init
```
このフォルダをGitで管理し始める宣言。`.git` という隠しフォルダが作られる。

```bash
git add .
```
「次のコミットに含めるファイル」を選ぶ。`.`（ドット）は「全部」の意味。

```bash
git commit -m "Initial setup"
```
変更を「確定」して記録する。`-m` の後ろのテキストは変更内容のメモ（コミットメッセージ）。

```bash
git branch -M main
```
メインのブランチ（作業ライン）の名前を `main` にする。

```bash
git remote add origin https://github.com/gmgmgm417/tokei-kentei.git
```
「このフォルダの送り先はGitHubのこのリポジトリ」と登録する。
`origin` は送り先のニックネーム（慣習的に `origin` を使う）。

```bash
git push -u origin main
```
ローカルの変更をGitHubに送る。`-u origin main` は「今後も同じ場所に送る」という設定。
次回からは `git push` だけでOK。

---

### GitHub（ギットハブ）とは

Gitで管理したファイルをインターネット上に保存・共有できるサービスです。

- **リポジトリ**: ファイルをまとめて保管する場所（フォルダのようなもの）
- **GitHub Pages**: リポジトリの内容をウェブサイトとして公開できる機能（**無料**）
- **GitHub Actions**: コードをpushしたときに自動で処理を実行できる機能（**無料**）

---

### GitHub Actions（ぎっとはぶアクション）とは

「GitHubにpushされたら、自動でMkDocsをビルドしてサイトを更新する」という処理を自動化しています。

設定ファイル: [.github/workflows/deploy.yml](.github/workflows/deploy.yml)

```yaml
# mainブランチにpushされたら起動
on:
  push:
    branches:
      - main

jobs:
  deploy:
    steps:
      - Pythonをセットアップ
      - pip install でMkDocsをインストール
      - mkdocs gh-deploy でサイトをビルド＆公開
```

これにより、あなたが `git push` するだけで約2分後にサイトが自動更新されます。

---

## 構築した手順（時系列）

### 1. プロジェクトフォルダの準備

`C:\Users\gaku\Desktop\pj\統計検定\` フォルダを作成し、以下のファイル群を作成しました：

```
統計検定/
├── mkdocs.yml          ← サイト全体の設定
├── requirements.txt    ← 必要なPythonパッケージ一覧
├── .github/
│   └── workflows/
│       └── deploy.yml  ← 自動デプロイの設定
└── docs/
    ├── index.md        ← トップページ
    ├── 01_probability/ ← 確率論のノート
    ├── 02_statistical_inference/
    ├── ...（全7分野）
    ├── formulas/       ← 公式チートシート
    └── exam_info/      ← 試験情報・学習計画
```

### 2. MkDocsのインストール

```bash
pip install mkdocs mkdocs-material mkdocs-minify-plugin
```

### 3. ローカル確認

```bash
mkdocs serve
```

ブラウザで `http://127.0.0.1:8000` を開いて表示を確認。

### 4. GitHubにリポジトリを作成

GitHub（ https://github.com ）にログインして `tokei-kentei` という名前のPublicリポジトリを作成。

### 5. ローカルのファイルをGitHubに送る

```bash
git init
git add .
git commit -m "Initial setup"
git branch -M main
git remote add origin https://github.com/gmgmgm417/tokei-kentei.git
git push -u origin main
```

### 6. GitHub Pagesの有効化

GitHubのリポジトリ設定画面でGitHub Pagesを有効化。
GitHub Actionsが自動ビルドし、`gh-pages` ブランチにサイトが公開された。

### 7. スマホのホーム画面に追加

`https://gmgmgm417.github.io/tokei-kentei/` をSafari/Chromeで開き、ホーム画面に追加してアプリ化。

---

## 問題を追加するときの手順

サイトを運用していくうえで最も頻繁に行う作業です。

### 手順

**1. ファイルを編集する**（Claude Codeに依頼するか、自分でVSCodeで編集）

例: 確率論の過去問を追加する場合
→ `docs/01_probability/past_questions.md` に問題を追記

**2. 変更をGitHubに送る**

```bash
cd "c:\Users\gaku\Desktop\pj\統計検定"
git add .
git commit -m "確率論: 過去問2問追加"
git push
```

**3. 約2分待つ**

GitHub Actionsが自動でサイトを更新します。
進捗は `https://github.com/gmgmgm417/tokei-kentei/actions` で確認できます。

### コミットメッセージの書き方

`git commit -m "..."` の中身は自由ですが、後から見てわかるように書くのがおすすめです。

```bash
git commit -m "統計的推測: 最尤推定の問題3問追加"
git commit -m "ベイズ統計: 共役事前分布の概念を補足"
git commit -m "公式チートシート: t分布の欄を修正"
```

---

## よくある質問

**Q: `git push` のたびにパスワードが必要？**

最初の認証後は、Windowsの資格情報マネージャーにトークンが保存されるので、通常は不要になります。

**Q: 間違ったファイルを編集してしまった場合は？**

```bash
git status        # 変更されたファイルの一覧を確認
git diff          # 何が変わったかを確認
git restore ファイル名  # 変更を元に戻す（commitする前）
```

**Q: サイトが更新されない場合は？**

`https://github.com/gmgmgm417/tokei-kentei/actions` を開いて、ワークフローが成功（緑）か確認する。失敗（赤）の場合はエラーメッセージを確認。

**Q: 他のPCやスマホからも編集したい場合は？**

```bash
git clone https://github.com/gmgmgm417/tokei-kentei.git
```

でフォルダごとダウンロードできます。

---

## まとめ

| ツール | 役割 | 費用 |
|---|---|---|
| Markdown | ノートを書く | 無料 |
| MkDocs + Material | サイトに変換 | 無料 |
| Git | 変更履歴の管理 | 無料 |
| GitHub | ファイルの保管・公開 | 無料 |
| GitHub Actions | 自動デプロイ | 無料 |
| GitHub Pages | ウェブホスティング | 無料 |

このシステムの最大の利点は、**Markdownでノートを書いてpushするだけ**でスマホから見られる学習サイトが維持できることです。技術的な部分は一度設定してしまえば、あとは内容を増やすことに集中できます。
