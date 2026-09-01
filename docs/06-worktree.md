# 06　並列で作業する

worktree（デモを見るだけ・手順は持ち帰り）

**当日は打ちません。** 講師の画面を見るだけです。このページは、あとで自分で試すときのために置いてあります。

---

## やること

**作業する場所（フォルダ）を増やして**、2つの作業を同時に進められるようにします。

---

## 何が違うのか

03 でやった `git switch` は、**1つのフォルダの中身が入れ替わる**操作でした。
枝を切り替えると、いま開いているファイルが書き換わります。だから**同時に2つは進められません。**

`git worktree` は、**フォルダをもう1つ増やす**操作です。

| | `git switch` | `git worktree` |
|---|---|---|
| フォルダ | 1つ。中身が入れ替わる | 2つ以上。同時に開ける |
| 履歴（`.git`） | 1つ | 1つのまま共有される |
| 同時作業 | できない | **できる** |

**片方で AI を走らせながら、もう片方で別の作業ができます。**
AI の応答を待っている時間がそのまま空くのが、いちばん効く場面です。

---

## 打つコマンド

### 作業場所を増やす

```bash
git worktree add -b feature/foo ../wt-feature-foo
```

`feature/foo` という枝を作って、`../wt-feature-foo` というフォルダに置く、という意味です。
`../` なので、**いまのフォルダの隣**にできます。

増えたフォルダに入って、そこをエディタで開けば、もう別の作業場です。

```bash
cd ../wt-feature-foo
```

```bash
code .
```

### 一覧を見る

```bash
git worktree list
```

いまいくつ作業場があるかが並びます。

### 片付ける

```bash
git worktree remove ../wt-feature-foo
```

フォルダごと消えます。枝の記録は残るので、消しても作業が失われることはありません。

---

## こうなれば成功

- `git worktree list` に2行以上出る
- 2つのフォルダを別々のエディタで開き、両方で同時に編集できる
- `git worktree remove` のあと `git worktree list` が1行に戻る

---

## つまずいたら

| 症状 | どうするか |
|---|---|
| `fatal: '../wt-feature-foo' already exists` | 同じ名前のフォルダがすでにあります。別の名前にするか、`git worktree remove` で消してください |
| `already checked out` | その枝を別の作業場で開いています。`git worktree list` で場所を確認してください |
| `remove` しても一覧に残る | フォルダを手で消した場合に起きます。`git worktree prune` で掃除できます |
| 元のフォルダに戻れない | `git worktree list` の一番上が元のフォルダです。`cd` でそこに戻ってください |

---

## 持ち帰り: 1タスク1作業場で回す

慣れてきたら、**タスクごとに作業場を作って、終わったら消す**という使い方になります。

```bash
git worktree add -b feature/issue-123 ../wt-issue-123
cd ../wt-issue-123
```

作業してコミットしたら、そのまま PR まで出せます。

```bash
git push -u origin feature/issue-123
gh pr create --fill
```

マージされたら片付けます。

```bash
cd -
git worktree remove ../wt-issue-123
```

**元のフォルダでは作業せず、作業場は使い捨てにする。** これが一番散らからない形です。

---

[← 05 他人の変更を受け取る](05-pull.md)　|　[README に戻る](../README.md)
