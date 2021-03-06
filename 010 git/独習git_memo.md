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
1. リポジトリの作成
   ~~~
   $ git init
    Initialized empty Git repository in (パス)
   ~~~
   - サーバが起動されない
   - リポジトリはローカルである
  ローカルフォルダの中にgitリポジトリ（作業ディレクトリ）を追加している
2. リポジトリの状態を確認
   ~~~
   $ git status
    On branch master
    No commits yet
   ~~~ 
3. ファイルをリポジトリに追加する
   ~~~
   $ git add filefixup.bat
   $ git status
    Changes to be committed:
    new file:   filefixup.bat
   ~~~
   新しいファイルが存在すること。  
   コミットが出来ること。
4. ファイルをコミットする
   ~~~
   $ git commit -m "This is the first commit message"
    [master (root-commit) d36c164] This is the first commit message
    1 file changed, 1 insertion(+)
    create mode 100644 filefixup.bat
   ~~~
   コミットをすることでファイルのヒストリーが記録されるようになる。
5. リポジトリを調べる
   ~~~
   $ git log
    commit d36c1645225c32f5dabde0ad58dfee8a9a4f18fa (HEAD -> master)
    This is the first commit message
   ~~~
   --statスイッチを付加することで構成ファイルが参照できる
   ~~~
   $ git log --stat
    commit d36c1645225c32f5dabde0ad58dfee8a9a4f18fa (HEAD -> master)
    This is the first commit message
   ~~~
   ~~~
    filefixup.bat | 1 +
    1 file changed, 1 insertion(+)
   ~~~
## 第５章 GitGui
1. GUIでgitを使用する
    1. 概要
   Git GUIは公式でありWin、Mac、Linux全てで使用できる。
    2. 起動
   ~~~
    $ git gui
   ~~~
    3. GUIでのログを出力
   Repository -> visualize master's History   
    4. コミット前の同ファイルへのステージング
   ステージングファイルの内容は上書きされて、1つ目の変更は消えてしまう。
## 第６章 ファイルの追跡と更新
1. コマンドライン
    1. ファイルに一行追加
    ~~~
    $ echo "追記内容" >> math.sh
    ~~~
    2. ファイル内容確認
    ~~~
    $ cat math.sh
    ~~~
2. リポジトリの変更内容を確認する
    ~~~
    $ git diff
    --- a/math.sh
    +++ b/math.sh
    @@ -1 +1,2 @@
     # Comment
    +a=1
    ~~~
    比較ファイル、先頭(+)が追加された行を表す
3. コミット前のステージングエリアでの変更
    ~~~
    $ git status
    On branch master
    Changes to be committed:
        modified:   math.sh
    Changes not staged for commit:
        modified:   math.sh
    ~~~
    既に一度addでステージングエリアに変更を反映している。そのファイルに対して、さらに修正。コミットする内容は幾度も修正可能。
    ~~~
    $ git diff
    --- a/math.sh
    +++ b/math.sh
     # Comment
     a=1
    -echo $a
     b=2
    ~~~
    これは作業ディレクトリとステージングエリアの差分が比較されている。
    ~~~
    $ git diff --staged
    --- a/math.sh
    +++ b/math.sh
    @@ -1,2 +1,4 @@
     # Comment
     a=1
    +echo $a
    +b=2
    ~~~
    --stagedスイッチをつけることでステージングエリアとリポジトリの差分を表示する。
4. 動作をした場合の結果を事前に確認する
    dry-run（予行演習）※短縮形 -n
    ~~~
    git add --dry-run .
    add 'a'
    add 'b'
    add 'c'
    add 'd'
    ~~~

## 第７章 変更箇所をコミット
1. ステージングエリアの活用
    1. ファイルを追加　git add
    2. ファイルを削除　git rm
    3. ファイル名の変更　git mv
    4. 変更の取消　git reset
    5. 特定ファイルのみコミットしない（テストファイル等）
2. ファイルの削除
    ~~~
    $ rm a
    $ git status
    deleted:    a
    ~~~
    これではファイル削除の変更がステージングエリアに残らない。
    ~~~
    $ git rm a
    $ git status
    Changes to be committed:
        deleted:    a
    ~~~
    これであればファイル削除がステージングエリアに残る。
    ~~~
    $ git commit -m "removed a and b"
     delete mode 100644 a
     delete mode 100644 b
    ~~~
3. ファイル名の変更
    ~~~
    $ mv c renamed_file
    $ git status
    Changes not staged for commit:
        deleted:    c
    Untracked files:
        renamed_file
    ~~~
    ファイル削除、新規ファイル追加の２処理として認識されてしまう。
    ~~~
    $ git rm c
    $ git add renamed_file
    $ git status
        Changes to be committed:
        renamed:    c -> renamed_file
    ~~~
    ~~~
    $ git mv d another_rename
    $ git status
        renamed:    c -> another_rename
        renamed:    d -> renamed_file
    ~~~
    ファイル操作をリネームとして記録することが出来る。
4. ファイルをコミットするべきタイミング
   リポジトリにコミットを行ったタイミングは、「取り戻すことが出来る成果」となる。
   1. ファイルを追加 or 削除
   2. ファイル名を変更
   3. ファイルを適切な状態まで変更したとき
   4. しばらくタスクから離れるとき
   5. 修正に不安なコードを適用するとき
5. コミット行をハンドピックする
   コミットはしたくないが、作業ディレクトリには残しておきたいようなコードなどに有効（デバッグ文等）
   1. GitGuiでなんとかする
    変更行を選択して右クリック「stage line for commit」でステージングエリアに配置したい行のみを選択→コミット
   2. Cuiでなんとかする
   ~~~
    $ git add -p
     -- ファイルの変更 --
    (1/1) Stage this hunk [y,n,q,a,d,e,?]? e
     -- 指定のエディタでコミットしたくない行の削除 --
   ~~~
6. ステージングエリアから変更を削除する
    ~~~
    $ git reset math.sh
    ~~~
7. ファイルを最後にコミットしたバージョンに戻す
   ワークエリアを直近のコミットの状態にする
    ~~~
    $ git checkout math.sh
    ~~~
## 第８章 Gitタイムマシン
1. SHA1 ID
    コミット毎にSHA1 IDハッシュキーが設定されている。
2. 特定ファイルのログのみ参照
    ~~~
    $ git log --oneline math.sh
    ~~~
3. 最適なコミットメッセージを記載する
    ヘルプページには、50文字未満の1行で変更を要約し（ログに表示されるタイトル）、その次に1行空けてさらに詳細な記述を入れることが良いとされている。
    git log --oneline でタイトルをみれて、git logで詳細な変更がみれる。
4. 直近のコミットメッセージを修正する
    ~~~
    $ git commit --amend
    ~~~
5. 現在のリポジトリの状態を判断する
    コミットが前後コミットの状態をポインタで持っており、そのポインタで繋がれた履歴がブランチ。
    開発履歴全体を「master」ブランチと呼ぶ。
    「master」は同時に最後のコミットに向かうポインタも表す。「現在位置」=「master」
    現在のブランチ位置は「HEAD」と呼ぶ。
    ~~~
    $ git rev-parse HEAD
    　97bd2341b220b6d517ba20e1d1b5bb5337a9147a
    $ git rev-parse master
    　97bd2341b220b6d517ba20e1d1b5bb5337a9147a
    ~~~
    rev-parseは指定ブランチのハッシュキーを取得
6. 過去のリポジトリを現在参照リポジトリに変更
    ~~~
    $ git log --oneline
      <HASH KEY> Adding printf.
    $ git checkout <HASH KEY>
    ~~~
    ~~~
    $ git log --oneline
        3d14365 (HEAD) adding four empty files.
        b19e2f0 adding b variable.
    ~~~
    masterブランチが表示されていないのは、履歴から過去に戻っているから。
    ~~~
    $ git checkout master
    ~~~
    最新のコミットブランチに戻る（現在に戻る）
7. 過去のコミットにタグをつける
   ハッシュキーではなく、任意で付けたタグ名で参照（チェックアウト）出来るようになる。
    ~~~
    $ git tag <tag_name> -m "コメント" <HASH KEY>
    $ git tag
    four_file_galore
    ~~~
    git tag で設定したタグの確認ができる
## 第９章 ブランチ
1. ブランチを分けて作成する
    ~~~
    $ git branch dev
    $ git branch
        dev
      * master
    ~~~
    *がついているブランチが現在利用しているブランチ。これはブランチを作成時点でのリポジトリのコピーがdevとして作成されたことを表す。
    ~~~
    $ git checkout dev
    Switched to branch 'dev'
    $ git branch
      * dev
        master
    ~~~
    ブランチを切替した。
    ~~~
    $ git branch -d dev 
    Deleted branch dev (was 9aae6da).
    ~~~
    ブランチを削除した。
2. ブランチを作るときの考え方
   マスターブランチは「使えるコード」としておく。
   クリーンビルド、デプロイ可能な状態。
   ブランチはマスターから分けて、動作を確認したうえで、マスターブランチに反映する開発の進め方が好ましい。
3. Gitコマンドを別名として保存する
    ~~~
    $ git config --global alias.lol "log --graph --decorate --pretty=oneline --all --abbrev-commit"
    ~~~
　　多くのスイッチをつけたコマンドを別名で実行出来る設定

    $ git lol

4. ブランチ毎の最新コミットを表示する
    ~~~
    $ git branch -v
        master      97bd234 Adding printf.
      * new_feature f741e04 starting a second new file
    ~~~

5. ある時点のリポジトリでブランチを切替
    ~~~
    $ git branch fixing_readme <SHA1 HASHKEY>
    $ git checkout fixing_readme 
    Switched to branch 'fixing_readme'
    ~~~
6. 現在の変更をスタッシュする
ブランチの切替を途中で行ったら、現在までの仕事が失われてしまうため、git stashで一時退避する。
    ~~~
    $ git stash
    Saved working directory and index state WIP on new_feature: f741e04 starting a second new file
    ~~~

作業中の状態でハッシュが作成され、masterをチェックアウトすることができる。
~~~
    $ git stash list
    stash@{0}: WIP on new_feature: f741e04 starting a second new file
~~~
スタッシュとした作業のリストを表示する。
~~~
    $ git stash pop
~~~
作業中のリポジトリの状態を取り戻す。
ステージングエリアの状態を。
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