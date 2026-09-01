# 04　PRを出してマージする

「入れていい？」を申請する

---

## やること

03 で作った枝の内容を、「**これを `main` に入れていいですか**」という形で申請して、取り込みます。

この申請を **プルリクエスト（PR）** と言います。

---

## 打つコマンド

`add-notes` の枝にいることを確認してから始めます。

```bash
git branch
```

### PR を出す

```bash
gh pr create --fill
```

`--fill` は「コミットの名前をそのまま PR の題名にする」という意味です。
自分で題名を考えたい場合は `--fill` を外すと、対話式で聞かれます。

最後に `https://github.com/.../pull/1` のような URL が出ます。**これが申請書のありか**です。

### 画面で差分を見る

```bash
gh pr view --web
```

ブラウザで PR が開きます。**Files changed** のタブを押すと、緑と赤の差分が出ます。

02 でターミナルに出した `git diff` と同じものです。違うのは、**ここには会話が残せる**ことです。
行をクリックするとコメントが書けます。チームで使うときは、ここが相談の場所になります。

**「なぜこう変えたか」が後から誰でも読める。** これが PR を使う一番の理由です。

### 取り込む

```bash
gh pr merge --merge --delete-branch
```

`--merge` は取り込み方の指定、`--delete-branch` は**役目を終えた枝を消す**指定です。
枝は取り込んだら消すのが普通です。履歴は `main` に残るので、消しても記録は失われません。

### 手元にも反映する

**取り込まれたのはクラウド側だけ**です。手元の `main` はまだ古いままなので、持ってきます。

```bash
git switch main
```

```bash
git pull
```

`practice/notes.md` を開くと、枝で書いた内容が `main` にも入っています。

```bash
git log --oneline
```

記録が積み上がっているのが見えます。

---

## こうなれば成功

- `gh pr create --fill` が PR の URL を出した
- ブラウザの **Files changed** に緑と赤の差分が見えた
- `gh pr merge` がエラーなく終わり、ブラウザで PR を開くと **Merged**（紫のラベル）になっている
- `git switch main` → `git pull` のあと、`practice/notes.md` に枝で書いた内容が入っている

---

## つまずいたら

| 症状 | どうするか |
|---|---|
| `must be on a branch named differently than "main"` | `main` にいます。`git switch add-notes` で枝に戻ってから出してください |
| `no commits between main and add-notes` | 枝の上でコミットできていません。03 に戻って `git commit` してください |
| `pull request create failed: ... not found` | 枝をまだ上げていません。`git push -u origin add-notes` を先に打ってください |
| `gh pr merge` で選択肢を聞かれた | `--merge --delete-branch` を付け忘れています。`Ctrl + C` で抜けて打ち直してください |
| マージしたのに手元が変わらない | `git switch main` と `git pull` がまだです。両方打ってください |
| `git pull` で `You have unstaged changes` | 記録していない変更があります。`git add` → `git commit` してから `git pull` してください |

---

[← 03 作業を分ける](03-branch.md)　|　[05 他人の変更を受け取る →](05-pull.md)
