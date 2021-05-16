# 独習Git

## 第１章 はじめに

特記なし
## 第２章 Git概要
#### 用語
1. リポジトリとは
   ファイルを保存するストレージ
2. コミットとは
   変更を保存する動作
3. ブランチとは
   　　　　　D---F Ver1/Branch
    　　　　／
    A---B---C---E Main/Trunk
---
#### 特徴
1. 分散リポジトリ
   全ての開発者がローカル環境にリポジトリ全体のコピーを保持する。
2. ブランチの即時性
   メインリポジトリのチェックアウト時点のコピーをブランチとして作成する。
   ブランチでの作業はメインリポジトリに反映するまで変更が隔離されるため、自由に試すことが出来る。
3. ステージングエリア
   舞台袖のようなもので、コミット前の変更がため込まれる。またその中で実際にコミットするものの仕分けが出来る。
---
#### コマンド
1. ver調査
~~~
$ git --version
git version 2.31.1.windows.1
~~~
2. クローン
~~~
$ git clone (リポジトリurl)
~~~
3. logを表示
~~~
$ git log --oneline
1020db5 (HEAD -> main, origin/main, origin/HEAD) 'add Git Doc'
1ca17c0 add Front add Task
e9064b9 Update README.md
~~~
## 第３章 Gitに馴染む
1. 初期設定
    1. 名前とe-mailの設定
    ~~~
    $ git config --global user.name "自分の名前"
    $ git config --global user.email "自分のemailアドレス"
    ~~~   
    2. 設定の確認
    ~~~
    $ git config --list
    user.name=自分の名前
    user.email=自分のemailアドレス
    ~~~
2. gitヘルプ表示
   ~~~
   $ git add --help
   ~~~
3. git用語集の表示
   ~~~
   $ git help glossary
   ~~~
4. Configファイルの保存場所
    1. /etc/gitconfig
    2. $HOME/.gitconfig
    3. .git/config
※20章で優先度について解説
## 第４章 リポジトリ
1. 
    1. 
## 第５章 GitGui
1. 
    1. 
## 第６章 ファイルの追跡と更新
1. 
    1. 
## 第７章 変更箇所をコミット
1. 
    1. 
## 第８章 Gitタイムマシン
1. 
    1. 
## 第９章 ブランチ
1. 
    1. 
## 第１０章 ブランチをマージ
1. 
    1. 
## 第１１章 クローン
1. 
    1. 
## 第１２章 リモートと共同作業
1. 
    1. 
## 第１３章 変更をプッシュ
1. 
    1. 
## 第１４章 同期を保つ
1. 
    1. 
## 第１５章 ソフトウェア考古学
1. 
    1. 
## 第１６章 git rebaseの理解
1. 
    1. 
## 第１７章 ブランチの規約
1. 
    1. 
## 第１８章 GitHub
1. 
    1. 
## 第１９章 サードパーティ
1. 
    1. 
## 第２０章 Git応用
1. 
    1. 