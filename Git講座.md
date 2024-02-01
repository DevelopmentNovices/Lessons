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
ローカルリポジトリの変更履歴をリモートリポジトリにアップロードし共有するにはpushコマンドを実行する。
```
$ git push
```
この操作を行うことで、リモートリポジトリの変更履歴がローカルリポジトリの変更履歴と同じ状態になる。
## clone（クローン）
リモートリポジトリをローカルリポジトリに複製するにはcloneコマンドを実行する。
```
$ git clone <repo> [<dir>]
```
この操作を行うことで、リモートリポジトリの内容をユーザのローカル環境にダウンロードしローカルリポジトリとして利用できる。  
以下は、このLessonsリポジトリをcloneする例である。
```
$ git clone https://github.com/DevelopmentNovices/Lessons.git
Cloning into 'Lessons'...
remote: Enumerating objects: 7, done.
remote: Counting objects: 100% (7/7), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 7 (delta 0), reused 4 (delta 0), pack-reused 0
Receiving objects: 100% (7/7), done.
```
## pull（プル）
リモートリポジトリからローカルリポジトリを更新するにはpullという操作を行う。
```
$ git pull
```
この操作を行うことで、リモートリポジトリから最新の変更履歴をダウンロードして、ユーザのローカルリポジトリを更新する。
## fetch（フェッチ）
リモートリポジトリから更新情報のみを取得するにはfetchコマンドを実行する。
```
$ git fetch
```
# ブランチ
ブランチとは、開発の本流の履歴から分岐して記録する機能である。
単一の履歴はブランチと呼ばれる。
分岐したブランチは他のブランチの影響を受けないため、同じリポジトリ内で複数の変更を同時に進めることができる。
さらに、分岐したブランチは他のブランチと合流することで一つのブランチにまとめることができる。
## masterブランチ
リポジトリに最初のコミットを行うと、Gitはmasterという名前のブランチを作成する。
そのため、以降のコミットはブランチを切り替えるまでmasterブランチに追加される。
## ブランチの運用
ブランチは自由に作成することができる。
そのため、ブランチを効果的に利用するにはあらかじめ運用ルールを設けることが大切である。
ここでは、統合ブランチとトピックブランチについて説明する。
### 統合ブランチ
統合ブランチとは、リリース版がいつでの作成可能なようにしておくためのブランチである。
トピックブランチの分岐元としても使用する。
そのため、安定した状態を保っておくことが重要である。
### トピックブランチ
トピックブランチとは、機能の追加やバグ修正といったある課題に関する作業を行うために作成するブランチである。
複数の課題に関する作業を同時に行う時は、その数だけトピックブランチを作成する。
トピックブランチは安定した統合ブランチから分岐する形で作成し、作業が完了したら統合ブランチに取り込むという使い方をする。
## HEAD
HEADとは、現在使用しているブランチの先頭を表す名前である。
defaultではmasterの先頭を表す。
HEADが移動することで、使用するブランチが変更される。
## stash
stashとは、ファイルの変更内容を一時的に記録しておく領域である。
stashを使うことで、ワークツリーとインデックス中でまだコミットされていない変更を一時的に退避させることができる。
退避させた変更は後から取り出して、元のブランチや別のブランチに反映させることができる。
まだコミットしていない変更内容や新しく追加したファイルが、インデックスやワークツリーに残ったままで、他のブランチへ移動すると、その変更内容は元のブランチから移動先のブランチに対して移動する。
ただし、移動先のブランチで、同じファイルが既に何らかの変更が行われている場合は移動に失敗する。
このような場合は、変更内容を一度コミットするか、またはstashを使って一時的に変更内容を退避させてから移動しなければならない。
# ブランチの基本操作
## branch（ブランチ）
ブランチを作成するにはbranchコマンドを実行する。
```
$ git branch <branchname>
```
以下は、issue1ブランチを作成する例である。
```
$ git branch issue1
```
引数を指定せずbranchコマンドを実行すると、ブランチの一覧を表示することができる。  
以下は、ブランチの一覧を表示した例である。
```
$ git branch
  issue1
* master
```
ブランチを消去するには、branchコマンドに -d オプションを指定して実行する。
```
$ git branch -d <branchname>
```
以下は、issue1ブランチを消去した例である。
```
$ git branch -d issue1
Deleted branch issue1 (was fa856d6).
```
## checkout（チェックアウト）
別のブランチへ移動するにはcheckoutコマンドを実行する。
```
$ git checkout <branch>
```
以下は、issue1ブランチへ移動する例である。
```
$ git checkout issue1
Switched to branch 'issue1'
```
issue1ブランチに移動した状態でコミットを行うと、issue1ブランチに履歴が記録される。  
以下は、sample2.txtを作成しissue1にコミットした例である。
```
$ git add sample2.txt
$ git commit -m "add sample2.txt file"
[issue1 fa856d6] add sample2.txt file
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 sample2.txt
```
## merge（マージ）
ブランチと他のブランチをまとめて一つのブランチにするにはmergeコマンドを実行する。
```
$ git merge <commit>
```
指定したブランチがHEADの指しているブランチに取り込まれる。  
以下はmasterブランチにissue1を取り込んだ例である。
```
$ git checkout master
$ git merge issue1
Updating 5166da7..fa856d6
Fast-forward
 sample2.txt | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 sample2.txt
```
# 参考
>[サル先生のGit入門](https://backlog.com/ja/git-tutorial/)