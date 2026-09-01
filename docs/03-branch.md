# 03　作業を分ける

ブランチ（switch -c）

---

## やること

**枝**を作って、その上で作業します。枝の上で何をしても `main` は無傷のまま残ります。

---

## 打つコマンド

### 枝を作る

```bash
git switch -c add-notes
```

`-c` は「作る（create）」です。`add-notes` は枝の名前で、好きな名前で構いません。

いまどの枝にいるかを確認します。

```bash
git branch
```

`* add-notes` のように、いまいる枝に `*` がつきます。

### 枝の上で編集して記録する

`practice/notes.md` をエディタで開いて、好きに書き足してください。保存したら、02 と同じ手順です。

```bash
git status
```

```bash
git add practice/notes.md
```

```bash
git commit -m "メモを書いた"
```

### 枝をクラウドに上げる

```bash
git push -u origin add-notes
```

`-u origin add-notes` は**この枝を初めて上げるときだけ**必要です。
2回目からは `git push` だけで通ります。

### main に戻ってみる

ここが今日いちばん面白いところです。

```bash
git switch main
```

そのまま `practice/notes.md` をエディタで開いてください。

**さっき書いた内容が消えています。**

驚かなくて大丈夫です。消えたのではなく、**さっきの内容は `add-notes` という枝の上にある**だけです。
`main` はそれを知らないので、書く前の状態のままになっています。

枝に戻ると、また出てきます。

```bash
git switch add-notes
```

`practice/notes.md` を開くと、書いた内容が戻っています。

**枝を分けておけば、`main` を壊さずに何でも試せます。** AI に大きく書き換えさせるときほど効きます。

---

## こうなれば成功

- `git branch` に `add-notes` と `main` が並び、`*` が `add-notes` についている
- `git push -u origin add-notes` が エラーなく終わった
- `git switch main` すると `practice/notes.md` の書き足しが消え、`git switch add-notes` で戻ってくる

**最後は `add-notes` にいる状態**にしておいてください。次の 04 でそのまま使います。

---

## つまずいたら

| 症状 | どうするか |
|---|---|
| `git switch` で `Your local changes would be overwritten` | 保存したまま記録していない変更があります。`git add` → `git commit` で記録してから切り替えてください |
| `fatal: a branch named 'add-notes' already exists` | すでに作ってあります。`git switch add-notes`（`-c` なし）で移動してください |
| `git push` で `has no upstream branch` と出た | `-u origin 枝の名前` を付け忘れています。`git push -u origin add-notes` と打ち直してください |
| いまどこにいるか分からない | `git branch` を打つと、`*` がついているところが現在地です |
| `main` に戻ったら中身が消えて焦った | それが正しい動きです。`git switch add-notes` で戻ってきます |

---

[← 02 変更を記録する](02-commit.md)　|　[04 PRを出してマージする →](04-pr-merge.md)
