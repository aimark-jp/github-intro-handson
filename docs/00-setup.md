# 00　事前の準備

git / gh / アカウント / 動作確認

**当日は扱いません。** 勉強会が始まる前に済ませておいてください。
事前案内で届いた内容と同じものです。手元に残しておきたい方はこちらを見てください。

かかる時間は15分ほどです。

---

## やること

GitHub のアカウントを作り、`git` と `gh` を入れて、ログインします。最後に**名前とメールを設定**します。

---

## 打つコマンド

### GitHub のアカウントを作る

https://github.com/signup

入力するのは1画面だけです。

| 欄 | 入れるもの |
|---|---|
| Email | メールアドレス |
| Password | パスワード（15文字以上、または 8文字以上＋数字＋小文字） |
| Username | 好きな ID（半角英数字とハイフン。他の人からも見えます） |
| Your Country/Region | Japan のままで大丈夫です |

最後にメールに届く認証コードを入力すれば完了です。

すでにアカウントを持っている方は、そのままで構いません。

### ソフトを2つ入れる（Mac）

**ターミナル**を開きます（`Command + スペース` を押して「ターミナル」と入力して Enter）。

```bash
xcode-select --install
```

案内のウィンドウが出たら、そのまま進めてください。数分かかります。
`already installed` のようなメッセージが出た方は、もう入っているのでそのままで大丈夫です。

続けて、下のファイルをダウンロードして開きます。

https://github.com/cli/cli/releases/download/v2.98.0/gh_2.98.0_macOS_universal.pkg

インストーラーが立ち上がるので「続ける」で進めます。
「開発元を確認できません」と出たら、ファイルを右クリックして「開く」で進められます。

### ソフトを2つ入れる（Windows）

下のファイルをダウンロードして実行します。

https://github.com/git-for-windows/git/releases/download/v2.55.0.windows.5/Git-2.55.0.5-64-bit.exe

設定を聞かれますが、すべて初期状態のまま「Next」で大丈夫です。
終わると、スタートメニューに **Git Bash** というアプリが増えます。

続けて、下のファイルもダウンロードして実行します。

https://github.com/cli/cli/releases/download/v2.98.0/gh_2.98.0_windows_amd64.msi

**当日は「Git Bash」を使います。** 「コマンドプロンプト」や「PowerShell」ではありません。

### GitHub にログインする

Mac は**ターミナル**、Windows は **Git Bash** に打ちます。

```bash
gh auth login
```

いくつか質問されるので、矢印キーと Enter で選んでいきます。

| 質問 | 選ぶもの |
|---|---|
| ログイン先 | GitHub.com |
| 通信方法 | HTTPS |
| 認証のしかた | Login with a web browser |

最後にブラウザが開くので、画面に出たコードを貼り付ければ完了です。
**パスワードを直接入力する必要はありません。**

### 動作確認

```bash
git --version
```

```bash
gh auth status
```

こんなふうに出れば準備完了です。

```
git version 2.50.1
✓ Logged in to github.com account ...
```

**バージョンの数字は違っていて構いません。** `git version` から始まる行と、`✓ Logged in` の行が
出ていれば大丈夫です。

### 名前とメールを設定する

**ここまでやってください。** `gh auth login` は GitHub との**通信**を通すだけで、
**記録に残す名前とメールは別に設定が要ります。**

設定していないと、こうなります。

- **Mac** … 記録はできますが、`名前@MacBook-Air.local` のような身に覚えのないメールで残り、
  **GitHub 上で自分のコミットとして表示されません**（アイコンもリンクも付きません）
- **Windows** … そもそも記録できずに止まることがあります

まずメールアドレスを調べます。**自分のメールアドレスをそのまま使わないでください。**
GitHub が、公開しても大丈夫な代わりのアドレスを配っています。

https://github.com/settings/emails

このページの **Keep my email addresses private** のところに、こんな形のアドレスが出ています。

```
12345678+ユーザー名@users.noreply.github.com
```

**これをコピーしてください。** 数字の部分は人によって違います。

そのうえで、2つ打ちます。

```bash
git config --global user.name "自分の名前"
```

```bash
git config --global user.email "12345678+ユーザー名@users.noreply.github.com"
```

名前のほうは、日本語でもニックネームでも構いません。**他の人から見えます。**

**自分の本当のメールアドレスを設定すると、** 勉強会で使う共有リポジトリの記録に
そのまま残って参加者全員から見えますし、GitHub 側の設定によっては
`GH007: Your push would publish a private email address.` と出て弾かれます。
上の noreply のアドレスを使えば、どちらも起きません。

設定できたか確認します。

```bash
git config --global --list
```

`user.name` と `user.email` の行が出ていれば大丈夫です。

---

## こうなれば成功

- `git --version` が `git version ...` を返す
- `gh auth status` に `✓ Logged in to github.com account 自分のユーザー名` が出る
- `git config --global --list` に `user.name` と `user.email` の行が出る

---

## つまずいたら

| 症状 | どうするか |
|---|---|
| `git: command not found`（Mac） | `xcode-select --install` がまだか、途中で終わっています。もう一度打ってください |
| `git: command not found`（Windows） | 「コマンドプロンプト」を開いている可能性があります。**Git Bash** を開き直してください |
| `gh: command not found` | `gh` のインストーラーが終わっていません。ターミナルを一度閉じて開き直すと直ることもあります |
| `gh auth login` の途中で分からなくなった | `Ctrl + C` で抜けて、もう一度 `gh auth login` から打ち直せます |
| ブラウザが開かない | 画面に URL が出ているので、それを手でブラウザに貼り付けてください |
| `gh auth status` に `not logged in` と出る | `gh auth login` が完了していません。もう一度やり直してください |
| `git config` を打っても何も表示されない | それで正常です。設定するコマンドは何も返しません。`git config --global --list` で確認してください |
| noreply のアドレスが見つからない | https://github.com/settings/emails の **Keep my email addresses private** にチェックを入れると出てきます |
| 準備が間に合わなかった | **当日そのまま参加してください。** 画面は全部お見せしますし、録画も残ります |

---

[README に戻る](../README.md)　|　[01 手元とクラウド →](01-local-remote.md)
