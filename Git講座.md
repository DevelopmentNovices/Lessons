# Gitとは
Gitとは、ファイルやディレクトリの状態を更新履歴として記録・追跡する分散型バージョン管理システムである。
Gitを利用すると、ファイルやディレクトリの状態を過去の状態に戻したり、編集箇所の差分を表示したりすることができる。
また他人が編集したファイルを古いファイルで上書きしようとすると警告が出るため、他人の編集内容を上書きしてしまうなどのトラブルを防ぐことができる。
# 環境構築
1. インストーラをダウンロード  
以下のURLからgitのHPに行き、Downloads > windowsと進み、ClickHere to downloadをクリックし最新のGitのインストーラをダウンロードする  
http://git-scm.com/
2. ダウンロードしたGitのインストーラを実行し、Installをクリックしインストールが完了するまで待つ。インストールが完了したらFinishをクリックし終了する。
3. インストールしたら、スタートメニュー > すべてのプログラム > Git > Git Bashを起動する。
確認のため以下のversionコマンドを実行する。Gitのバージョンが表示されればインストール成功。
```
$ git --version
git version 2.43.0.windows.1
```
4. ユーザ名とメールアドレスを登録する
Gitの設定はユーザのホームディレクトリに作成される.gitconfigファイルに記録されている。
直接ファイルを編集するか、configコマンドを実行しユーザ名とメールアドレスを登録する。
```
$ git config --global user.name "<ユーザ名>"
$ git config --global user.email "<メールアドレス>"
```
# Gitの基礎知識
## リポジトリ
リポジトリとは、ファイルやディレクトリの状態を記録する場所である。
変更履歴を管理したいディレクトリをリポジトリの管理下に置くことで、そのディレクトリ内のファイルやディレクトリの変更履歴を記録することができる。
リポジトリは、ローカルリポジトリとリモートリポジトリの二種類に分けられる。
ユーザは作業内容をローカルリポジトリに記録し、リモートリポジトリにアップロードすることで公開する。
リモートリポジトリを通して他人の作業内容を取得することもできる。
## ローカルリポジトリ
ローカルリポジトリとは、ユーザのローカル環境に配置されたリポジトリである。
## リモートリポジトリ
リモートリポジトリとは、複数人のユーザで共有するためにサーバに置かれたリポジトリである。
## ワークツリー
ワークツリーとは、リポジトリの管理下に置かれた作業ディレクトリのことである。
## インデックス
インデックスとは、リポジトリとワークツリーの間に存在する場所である。
コミットする場合、ワークツリーの状態を直接リポジトリ内に記録するのではなく、インデックスに設定された状態を記録する。
そのため、コミットでファイルの状態を記録するには、インデックスにファイルを登録する必要がる。
# Gitの基本操作
## init（イニット）
特定のディレクトリをGitの管理下にするには、そのディレクトリに移動してinitコマンドを実行する。
```
$ git init
```
以下は、Cドライブ直下にsampleディレクトリを作成し、Gitリポジトリに設定する例である。
```
$ mkdir sample
$ cd sample
$ git init
Initialized empty Git repository in C:/sample/.git/
```
## status（スタッツ） & add（アド）
Gitの管理下にあるディレクトリのワークツリーとインデックスの状態を確認するにはstatusコマンドを実行する。
```
$ git status
```
以下は、先ほど作成したsampleディレクトリ内にsample.txtを作成し、状態を確認した例である。
```
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        sample.txt

nothing added to commit but untracked files present (use "git add" to track)
```
sample.txtが履歴の追跡対象になっていないことが確認できる。
一度インデックスに登録すると、追跡対象に登録することができる。
ファイルをインデックスに登録するにはaddコマンドを実行する。
\<file>はインデックスに登録するファイルを指定する。スペース区切りで複数指定することもできる。
```
$ git add <file>..
```
以下は、sample.txtをインデックスに追加し、状態を確認した例である。
```
$ git add sample.txt
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   sample.txt
```
## commit（コミット）
インデックスに設定された状態をリポジトリに記録するにはcommitコマンドを実行する。
```
$ git commit -m "<コメント>"
```
以下は、コミットをし、状態を確認した例である。
```
$ git commit -m "first commit"
[master (root-commit) 5166da7] first commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 sample.txt

$ git status
On branch master
nothing to commit, working tree clean
```
## push（プッシュ）
ローカルリポジトリの変更履歴をリモートリポジトリにアップロードし共有するにはpushという操作を行う。
この操作を行うことで、リモートリポジトリの変更履歴がローカルリポジトリの変更履歴と同じ状態になる。
## clone（クローン）
リモートリポジトリを複製するにはcloneという操作を行う。
この操作を行うことで、リモートリポジトリの内容をユーザのローカル環境にダウンロードしローカルリポジトリとして利用できる。
## pull（プル）
リモートリポジトリからローカルリポジトリを更新するにはpullという操作を行う。
この操作を行うことで、リモートリポジトリから最新の変更履歴をダウンロードして、ユーザのローカルリポジトリを更新する。
# ブランチ
# タグ
# コミット
# プルリクエスト
# 参考
>[サル先生のGit入門](https://backlog.com/ja/git-tutorial/)