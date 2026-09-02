# 05　他人の変更を受け取る

fetch / pull

---

## やること

**もう1つ別のフォルダに同じリポジトリを落として**、そこから変更を上げます。
そのあと、元のフォルダで受け取ります。

---

## 仕掛けの説明

本来これは、**他の人が push した**ときに起きることです。ですが今日は一人なので、そのままでは再現できません。

そこで、**同じリポジトリをもう1か所に `clone`** します。この2つ目のフォルダを「他の人の PC」だと思ってください。

実務では、この2つ目が本当に別の人のパソコンになるだけです。**やっていることは完全に同じ**です。

---

## 打つコマンド

### 「他の人」のフォルダを作る

いまのフォルダの外に出てから、もう一度 `clone` します。

```bash
cd ~/Desktop
```

```bash
gh repo clone 自分のユーザー名/つけた名前 friend-copy
```

最後の `friend-copy` が、落とす先のフォルダ名です。元のフォルダとぶつからないように変えています。

```bash
cd friend-copy
```

いまどこにいるかを確認しておきます。**ここからしばらく、フォルダを行き来します。**

```bash
pwd
```

### 「他の人」として変更を上げる

`friend-copy` のほうの `practice/notes.md` をエディタで開いて、1行書き足します。

```bash
code .
```

書き足して保存したら、02 と同じ手順です。

```bash
git add practice/notes.md
```

```bash
git commit -m "別の場所から書き足した"
```

```bash
git push
```

これで**クラウド側だけ**が1歩進みました。元のフォルダはまだ何も知りません。

### 元のフォルダに戻って受け取る

```bash
cd ~/Desktop/つけた名前
```

```bash
pwd
```

元のフォルダに戻れていることを確認してから進みます。

まず、クラウド側に何があるかを**見に行くだけ**の操作をします。

```bash
git fetch
```

```bash
git status
```

`Your branch is behind 'origin/main' by 1 commit, and can be fast-forwarded.` のように出ます。
**手元が1つ遅れている**、という意味です。

`git fetch` は「クラウド側の状況を見に行く」だけで、**手元のファイルは書き換えません。**

受け取ります。

```bash
git pull
```

`practice/notes.md` を開いてください。**もう1つのフォルダから書き足した行が入っています。**

`git pull` は「見に行って、手元にも反映する」操作です。`fetch` と反映をまとめてやってくれます。
普段は `git pull` だけ使えば足ります。

**作業を始める前に `git pull`。** 他の人と一緒に使うときは、これが習慣になります。

### 片付け

`friend-copy` はもう使いません。フォルダごと消して構いません。
中身はクラウドに上がっているので、消しても失われません。

---

## こうなれば成功

- `friend-copy` から `git push` がエラーなく終わった
- 元のフォルダで `git fetch` のあと `git status` に `behind` と出た
- `git pull` のあと、元のフォルダの `practice/notes.md` に書き足した行が入っている

---

## つまずいたら

| 症状 | どうするか |
|---|---|
| いま自分がどのフォルダにいるか分からない | `pwd` を打つと現在地が出ます。`ls` でも中身から判断できます |
| `gh repo clone` で `already exists` | `friend-copy` がすでにあります。`friend-copy2` など別の名前にしてください |
| 元のフォルダの名前を忘れた | `cd ~/Desktop` してから `ls` を打つと並びます |
| `git status` に `behind` が出ない | `friend-copy` 側の `git push` がまだか、元のフォルダに戻れていません。`pwd` で確認してください |
| `git push` で `rejected` と出た | クラウド側が先に進んでいます。`git pull` してから `git push` し直してください |
| `git pull` で `You have unstaged changes` | 記録していない変更があります。`git add` → `git commit` してから `git pull` してください |
| `git pull` で `CONFLICT` と出た | 2か所で**同じ行**を変えています。今日は扱わないので、`git merge --abort` で元に戻して先へ進んでください |
| `Already up to date` と出て何も起きない | `friend-copy` 側の `git push` ができていません。そちらで `git log --oneline` を打って、コミットがあるか確認してください |

---

[← 04 PRを出してマージする](04-pr-merge.md)　|　[06 並列で作業する →](06-worktree.md)
