翻訳成果を利用したい人へ
========================

ダウンロード
------------

  * [[暫定リリース版|http://vimdoc-ja.googlecode.com/files/vimdoc_ja-20110212-r335.zip]](ZIP, 2011/02/12, r335)
  * [[スナップショット|http://www1.kaoriya.net/vimdoc_j/vimdoc_ja-snapshot.tar.bz2]](tar.bz2, 毎日7時頃自動更新)
  * リポジトリのデータを直接使う (後述)

インストール方法
----------------

- ダウンロードしたヘルプファイルを展開します。

> 各OSで利用できる解凍ソフトを利用してください。例えば Unix 系 OS なら以下のようになります。

    tar jxvf ./vimdoc_ja-snapshot.tar.bz2

- 展開するとruntimeディレクトリされるので、これを 'runtimepath' が通った場所へ配置します。

> Windowsなら、~/vimfiles/ 以下に runtime の中身をコピーします。
>> ~/ はホームディレクトリで、Windows XP なら `C:\Documents and Settings\{ユーザ名}`、Vista や 7 なら `C:\Users\{ユーザ名}` になります。
>Unix 系の OS なら、~/.vim/ 以下に runtime の中身をコピーします。
>もしくは、展開した場所を 'runtimepath' に追加する方法もあります。

    :set runtimepath+=/path/to/runtime

- tags を生成します。Vimを起動し、以下のようなコマンドを実行します。

    :helptags ~/.vim/doc

> `~/.vim/doc` は、runtime を配置した場所の中の doc ディレクトリを指定します。

- 日本語 help の優先順位をあげます。vimrc に以下を追記します。

    :set helplang=ja,en

- 英語ヘルプを読みたい場合は以下のようにします。

    :help @en


リポジトリのデータを直接使う場合
--------------------------------

[[https://github.com/tpope/vim-pathogen pathogen.vim]]、[[https://github.com/thinca/vim-rtputil rtputil.vim]]、[[https://github.com/gmarik/vundle Vundle]] などを使っている場合は、リポジトリのデータを直接利用することができます。
この場合、リポジトリ最新のデータに簡単に追従できる利点があります。

以下のようにして、各々の bundle ディレクトリにリポジトリの runtime ディレクトリをチェックアウトしてください。

    svn checkout http://vimdoc-ja.googlecode.com/svn/trunk/runtime ~/.vim/bundle/vimdoc-ja

bundle ディレクトリの位置を変えている場合は適時読みかえてください。更新は `svn update` で可能です。

HTMLでみたい人へ
----------------

  * [[http://sites.google.com/site/vimdocja/]]
