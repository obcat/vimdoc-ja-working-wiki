翻訳成果を利用したい人へ
========================

ダウンロード
------------

  * スナップショット [[zip|https://github.com/vim-jp/vimdoc-ja/zipball/master]] [[tar|https://github.com/vim-jp/vimdoc-ja/tarball/master]] (ファイル名はgitのハッシュ値が含まれるので不定です: vim-jp-vimdoc-ja-xxxxxxx.zip)
  * リポジトリのデータを直接使う (後述)

インストール方法
----------------

- ダウンロードしたファイルを展開します。

> 各OSで利用できる解凍ソフトを利用してください。例えば Unix 系 OS なら以下のようになります。

    tar zxvf ./vim-jp-vimdoc-ja-xxxxxxx.tar.gz

- 展開されたファイルを 'runtimepath' が通った場所へ配置します。

> Windowsなら、~/vimfiles/ 以下に展開されたディレクトリの中身をコピーします。
>> ~/ はホームディレクトリで、Windows XP なら `C:\Documents and Settings\{ユーザ名}`、Vista や 7 なら `C:\Users\{ユーザ名}` になります。
>Unix 系の OS なら、~/.vim/ 以下にコピーします。
>もしくは、展開した場所を 'runtimepath' に追加する方法もあります。

    :set runtimepath+=/path/to/vim-jp-vimdoc-ja-xxxxxxx

- 日本語 help の優先順位をあげます。vimrc に以下を追記します (OSの言語設定が日本語になっているなら不要)。

    :set helplang=ja,en

    :help コマンドを実効して日本語ヘルプが表示されればインストールは成功です。

- 英語ヘルプを読みたい場合は以下のようにします。

    :help @en


リポジトリのデータを直接使う場合
--------------------------------

[[pathogen.vim|https://github.com/tpope/vim-pathogen]]、[[rtputil.vim|https://github.com/thinca/vim-rtputil]]、[[Vundle|https://github.com/gmarik/vundle]] などを使っている場合は、リポジトリのデータを直接利用することができます。
この場合、リポジトリ最新のデータに簡単に追従できる利点があります。

以下のようにして、各々の bundle ディレクトリにリポジトリの runtime ディレクトリをチェックアウトしてください。

    git clone https://github.com/vim-jp/vimdoc-ja.git ~/.vim/bundle/vimdoc-ja

bundle ディレクトリの位置を変えている場合は適時読みかえてください。更新は `git pull` で可能です。

HTMLでみたい人へ
----------------

  * [[http://vim-jp.org/vimdoc-ja/]]
