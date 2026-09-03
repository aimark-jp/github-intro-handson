# AGENTS.md

このリポジトリで AI エージェントが作業するときのルールです。
Codex CLI・Cursor など、AGENTS.md を自動で読み込むツールはこれに従ってください。

対象は「`members/` に自分の自己紹介を追加する」作業だけです。
ファイルの書き方（frontmatter・テンプレート・使える記法）は [members/README.md](members/README.md) に
まとまっています。ここでは繰り返さないので、書式に迷ったらそちらを見てください。

このファイルが対象にしていないもの:

- `practice/members/<login>.md` … これは別の、Git 練習専用の仕組みです（[docs/03-branch.md](docs/03-branch.md) 参照）。
  自己紹介サイトとは無関係なので、この作業では触らないでください。
- ワークショップ当日だけの手順 … それは [PROMPT.md](PROMPT.md) の役割です。1回きりの導入用なので、
  ここでは扱いません。

---

## 公開リポジトリであることに注意する

このリポジトリは public です。`members/` に置いた内容は GitHub Pages で誰でも見られる形で
公開されます（https://aimark-jp.github.io/github-intro-handson/ ）。

- 住所・電話番号・個人のメールアドレス・非公開の勤務先情報など、公開してよいか判断が必要な情報を、
  自分の判断で `intro.md` やアイコン画像に書き込まないでください。
- 本人以外の情報（同僚や友人の名前など、公開の同意を確認していないもの）も書き込まないでください。
- 迷ったら書かずに、「これは公開して大丈夫ですか？」と作業を頼んだ人に確認してください。

---

## やること: ブランチを切って PR を出す

1. `gh api user --jq .login` で GitHub のユーザー名（login）を調べる。手で打ち替えない。
2. `git switch -c add-<login>` でブランチを作る（例: `add-yourname`）。**`main` に直接コミットしない。**
   すでに同名のブランチがあれば（以前の練習で作っていた場合など）、新規作成せずそのブランチに
   移動すればよい。
3. `members/<login>/intro.md` を新規作成する（任意で `avatar.png` / `.jpg` / `.jpeg` / `.webp` も
   同じフォルダに追加）。フォルダ名は自分の GitHub ユーザー名と正確に一致させる。書式は
   [members/README.md](members/README.md) のテンプレートに従う。
4. 変更をコミットし、`git push -u origin add-<login>`。
5. `gh pr create` で PR を作る。**PR の URL を報告したら、そこで止まる。マージはしない。**

マージは人間がブラウザで行います。PR を出すところまでが AI の担当、というのがこのリポジトリ全体の
方針です（[docs/04-pr-merge.md](docs/04-pr-merge.md) 参照）。明示的に頼まれない限り、
`gh pr merge` は実行しないでください。

## PR の説明文は日本語で書く

`gh pr create --fill` はコミットメッセージをそのまま PR 本文に使います。コミットメッセージを
日本語で書いていれば、`--fill` のままで問題ありません。

コミットメッセージが日本語になっていない場合や、内容をきちんと書き添えたい場合は、`--fill` に
頼らず `--title` / `--body` を明示的に日本語で渡してください。

```bash
gh pr create --title "add-<login> の自己紹介を追加" --body "$(cat <<'EOF'
members/<login>/intro.md を追加しました。
EOF
)"
```

## 触っていいファイル / 触ってはいけないファイル

触っていい:

- `members/<自分の login>/intro.md`
- `members/<自分の login>/avatar.{png,jpg,jpeg,webp}`（任意）

触らない:

- `members/<他人の login>/` 以下 … 他の人のフォルダ。1人1フォルダの仕組みなので、
  自分のフォルダ以外に触る必要はない。
- `site/**`、`.github/**` … サイトの実装と CI 設定。`.github/CODEOWNERS` によりこの2つの配下は
  `@tokku5552` のレビューが必須。変更が必要になった場合は、まず人間に確認する。
- `docs/**`、`README.md`、`PROMPT.md`、`practice/**` … 講義資料と練習専用の仕組み。この作業の対象外。

## PR のチェックが失敗したら

PR を出すと、`members/**` の内容が自動でチェックされます
（`.github/workflows/pages.yml` の `validate` ジョブ、`node site/build.mjs --check`）。

失敗した場合は PR の **Files changed** タブに、どこが問題かが日本語の注釈で表示されます。
それを読んで修正し、同じブランチに push すれば自動で再チェックされます。
エラーメッセージの意味や直し方は [members/README.md](members/README.md) の
「PR に赤いバツが出たら」を参照してください。
