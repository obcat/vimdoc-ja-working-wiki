翻訳成果を利用したい人へ
========================

ダウンロード
------------

  * スナップショット [[zip|https://github.com/vim-jp/vimdoc-ja/archive/master.zip]] | [[tar|https://github.com/vim-jp/vimdoc-ja/archive/master.tar.gz]]
  * リポジトリのデータを直接使う (後述)

インストール方法
----------------

- ダウンロードしたファイルを展開します。

> 各OSで利用できる解凍ソフトを利用してください。例えば Unix 系 OS なら以下のようになります。

    tar zxvf ./vimdoc-ja.tar.gz

- 展開されたファイルを 'runtimepath' が通った場所へ配置します。

> Windowsなら、~/vimfiles/ 以下に展開されたディレクトリの中身をコピーします。
> ~/ はホームディレクトリで、Windows XP なら `C:\Documents and Settings\{ユーザ名}`、Vista や 7 なら `C:\Users\{ユーザ名}` になります。
>Unix 系の OS なら、~/.vim/ 以下にコピーします。
>もしくは、展開した場所を 'runtimepath' に追加する方法もあります。

    :set runtimepath+=/path/to/vimdoc-ja

- `:helptags` コマンドを使ってタグファイルを生成します。

>

    :helptags /path/to/vimdoc-ja/doc

:help コマンドを実行して日本語ヘルプが表示されればインストールは成功です。

- :help コマンドで英語のヘルプが表示される場合は日本語の優先順位をあげてください。vimrc に以下を追記します。

    :set helplang=ja,en

- 英語ヘルプを読みたい場合は以下のようにします。

    :help @en


リポジトリのデータを直接使う場合
--------------------------------

[[pathogen.vim|https://github.com/tpope/vim-pathogen]]、[[rtputil.vim|https://github.com/thinca/vim-rtputil]]、[[Vundle|https://github.com/gmarik/vundle]] などを使っている場合は、リポジトリのデータを直接利用できます。
この場合、リポジトリ最新のデータに簡単に追従できる利点があります。

以下のようにして、各々の bundle ディレクトリにリポジトリの runtime ディレクトリをチェックアウトしてください。

    git clone https://github.com/vim-jp/vimdoc-ja.git ~/.vim/bundle/vimdoc-ja

bundle ディレクトリの位置を変えている場合は適宜読みかえてください。更新は `git pull` で可能です。

リポジトリのデータをすべて取得するのはディスク容量が気になるという方は `--depth 1` を指定してください。履歴がダウンロードされなくなります。

    git clone --depth 1 https://github.com/vim-jp/vimdoc-ja.git ~/.vim/bundle/vimdoc-ja

また Git 1.7.10 以降を使用している場合は、`--single-branch` オプションを使うことで html 版を含むブランチがダウンロードされなくなります。

    git clone --depth 1 --single-branch https://github.com/vim-jp/vimdoc-ja.git ~/.vim/bundle/vimdoc-ja

Subversion でも取得できます。

    svn checkout https://github.com/vim-jp/vimdoc-ja/trunk ~/.vim/bundle/vimdoc-ja

プラグインなどを使わずに手動でリポジトリを使う場合はリポジトリをチェックアウトまたは更新した後に :helptags コマンドを使ってタグファイルを更新してください。

    :helptags /path/to/vimdoc-ja/doc


HTMLでみたい人へ
----------------

  * [[http://vim-jp.org/vimdoc-ja/]]
