# 02　変更を記録する

履歴と差分を読む（add / commit / push）

今日の本体です。**ここが通れば、残りは全部この形の繰り返し**になります。急がず進めてください。

---

## やること

`practice/profile.md` を自分のことに書き換えて、その変更を GitHub に記録します。

---

## 打つコマンド

### ファイルを書き換える

01 で `clone` したフォルダを、普段使っているエディタで開きます。

```bash
code .
```

`code` が使えない場合は、Finder（Mac）やエクスプローラー（Windows）からフォルダを開いて、
`practice/profile.md` をダブルクリックしてください。

`practice/profile.md` を開いて、**中身を好きに書き換えます。** 何を書いても構いません。
全部消しても大丈夫です。あとで戻せます。書き換えたら保存してください。

### 何が変わったかを見る

ここからはターミナルです。フォルダの中にいることを確認してから打ちます。

```bash
git status
```

```bash
git diff
```

`git status` は**変わったファイルの一覧**、`git diff` は**中身がどう変わったか**を出します。

`git diff` の見方はこれだけ覚えてください。

| 行の先頭 | 色 | 意味 |
|---|---|---|
| `+` | 緑 | 増えた行 |
| `-` | 赤 | 消えた行 |

長い場合は最後に `(END)` と出て止まります。`q` を押すと戻ります。

### 記録する

```bash
git add practice/profile.md
```

```bash
git commit -m "プロフィールを自分のことに書き換えた"
```

`git add` は「これを記録します」と選ぶ操作、`git commit` は「選んだものに名前をつけて記録する」操作です。
`-m` のあとが記録の名前になります。日本語で構いません。

### クラウドに上げる

```bash
git push
```

ここまでが1周です。**編集 → status → diff → add → commit → push。** これを繰り返すだけです。

### GitHub の画面で見る

ブラウザで自分のリポジトリを開きます。

```bash
gh repo view --web
```

`practice/profile.md` をクリックすると、いま書き換えた内容になっているはずです。
上の **Commits** から、さっきつけた名前のコミットを開くと、**緑と赤の差分**がそのまま出ます。

ターミナルで見た `git diff` と同じものです。**画面でもコマンドでも、読んでいるものは同じ**です。

### もう一度やる（時間があれば）

同じことをもう1回やります。2回やると履歴に2件並ぶので、「**積み上がっている**」のが目で見えます。

```bash
git add practice/profile.md
git commit -m "好きなものを書き足した"
git push
```

`git log --oneline` を打つと、記録が新しい順に並びます。

---

## こうなれば成功

- `git status` に `modified: practice/profile.md` が出た
- `git diff` に緑の `+` と赤の `-` が出た
- `git commit` のあとに `1 file changed, ...` のような行が出た
- `git push` が `To https://github.com/...` で終わり、エラーが出ていない
- GitHub の画面で、自分が書いた内容とコミットが見えている

---

## つまずいたら

| 症状 | どうするか |
|---|---|
| `fatal: not a git repository` | フォルダの外にいます。`cd` で 01 で clone したフォルダに入ってください |
| `git status` に何も出ない（`nothing to commit`） | ファイルを保存できていません。エディタで保存し直してください |
| `git diff` から抜けられない | `q` を押してください |
| `nothing added to commit` | `git add` を飛ばしています。`git add practice/profile.md` から打ち直してください |
| `Please tell me who you are` と出て commit できない | `git config --global user.name "名前"` と `git config --global user.email "メールアドレス"` を打ってから、もう一度 commit してください |
| commit のとき名前とメールの警告が出た | そのまま進んで大丈夫です。記録自体はできています |
| `git push` で `rejected` と出た | クラウド側が先に進んでいます。`git pull` を打ってから、もう一度 `git push` してください |
| `git push` で認証を聞かれた | `gh auth login` が終わっていません。[00-setup.md](00-setup.md) に戻ってください |
| 書き換えすぎて分からなくなった | `git restore practice/profile.md` を打つと、**最後に記録した状態に戻ります**。まだ commit していない変更は消えます |

---

[← 01 手元とクラウド](01-local-remote.md)　|　[03 作業を分ける →](03-branch.md)
