# Vim ドキュメント翻訳者の手引き


## はじめに

公式ヘルプの以下の場所にヘルプの書き方が記載されている。参照すること。

- `:h help-writing`

  (翻訳ヘルプに限らない一般的な) ヘルプの書式について。

- `:h help-translated`

  翻訳ヘルプを作成する際の注意事項。


### ファイル形式  

文字コードは UTF-8、改行文字は UNIX 形式 (`\n`) にする。

```vim
set fileencoding=utf-8 fileformat=unix
```

ファイルによっては cp932 などでは扱えない文字を含んでいるので次の設定もしておいたほうがよい。

```vim
set encoding=utf-8
```


## 文体

ユーザーマニュアルでは敬体 (ですます調) を用いる。

リファレンスマニュアルでは敬体と常体 (だである調) のどちらを用いても構わない。現状では両方が混在している。少なくとも、1 つのファイルではどちらかに統一しておきたい。

敬体を用いる場合でも、以下の場所では常体を用いること。

- 見出し

  ```help
  プラグインを使う
  ----------------
  
  まず、プラグイン自身のドキュメントを読んで、動作条件を確認してください。
  ```

- 短い箇条書き

  ```help
  プラグインの追加は以下の手順で行います:
  1. プラグインを入手する
  2. 正しいディレクトリにコピーする
  ```

- サンプルコードのコメント

  ```help
  :smile					*:smile*
      ユーザーを幸せにします。例: >
        " 10000 回幸せにする
        for i in range(10000)
          smile
        endfor
  ```


### 命令形

リファレンスマニュアルなので、命令しているというよりは操作の手順を簡潔に述べているだけであって、特に命令形だからという意識はしなくて良い。


## 半角と全角

ASCII 文字は半角文字を使う。カタカナは全角文字を使う。


## 空白

以下の場所には空白を入れる。

- 英単語やアラビア数字の前後
- クォートで囲まれた語句 (`"xxx"`、`'xxx'`、`` `xxx` ``) の前後
- リンク (`|xxx|`) の前後

ただし句読点や括弧の前後には空白を入れてはならない。例:

```help
正	v:true    数値 1。JSON では "true" として使われる。|json_encode()| を参照。
誤	v:true    数値1。JSONでは"true"として使われる。|json_encode()|を参照。
```

**メモ**

- 現状では徹底されていない。
- 他の翻訳プロジェクトでも空白を入れているところ多し。
- 空白を入れないほうが書きやすいし読みやすいと感じる。
- ファイル名やコマンド、コード片などは空白で区切った方が分かりやすいのでは?
- 「全角文字と半角文字の間には空白を入れる」的なルールでもよさそう。


## アラビア数字と漢数字

基本的にはアラビア数字 (`1`、`2`、`3`、...) を使う。例:

```help
正	第 2 引数は省略可能です。
誤	第二引数は省略可能です。
```

慣用表現の場合は漢数字 (`一`、`二`、`三`、...) を使う。例:

```help
正	これで同じ問題は二度と起きないでしょう。
誤	これで同じ問題は 2 度と起きないでしょう。
```


## 句読点

句読点は `、` と `。` を使う。


## 括弧

丸括弧は `_(` と `)_` を使う (`_` は半角空白)。全角の `（` と `）` を使ってはならない。


## `_not_` や `ALL` などの強調表現  

対応する日本語を曲線型のシングルクォート (`‘` と `’`) で囲む。

**メモ:**

- 日本語的な表現ではないので何もしなくていいのではないか?
- というか非日常的な記号は使いたくない。
- 現状ではほとんど使われていない。


## 訳注  

訳注には次の 2 種類がある。

1. 原文の補足
1. 翻訳者の作業用メモ

1 の用途で使う場合は `{訳注: 補足説明。ほげほげ、ふがふが。}` の形式にせよ。構文強調表示される。

2 の用途で使う場合、行単位で書くと小細工できて都合が良い。

```help
訳注メモ: こんな感じでリリースに含めないようなメモを書く  
訳注メモ: 作業ログ、疑問、注意点など、他の翻訳者が後で参照できるようにする  
訳注メモ: リリースに含めないと利用者からのフィードバックを得られないか?  
訳注メモ: 消さないほうが利用者にとって分かりやすいか?  
訳注メモ: 名前も入れておくと分かりやすい?
```

**メモ:** 現在 2 の用途ではあまり使われていない。


### 翻訳されるメッセージ

日本語環境だと翻訳されるメッセージは、本文中では原文のままにし、その日本語訳を訳注で補足すること。

基本的には 1 つのメッセージに対して 1 つの訳注をつければよい:
  
```help
  h F   ヘルプバッファフラグ。表示されるのは "[help]"。
        {訳注: 日本語メッセージの場合: "[ヘルプ]"}
  H F   ヘルプバッファフラグ。表示されるのは ",HLP"。
  w F   プレビューウィンドウフラグ。表示されるのは "[Preview]"。
        {訳注: 日本語メッセージの場合: "[プレビュー]"}
```

くどくなる場合は複数のメッセージに対して 1 つの訳注をつけてもよい:

```help
	ロング		ショート	意味 ~ 
	[readonly]	{RO}		ファイルは書き込み制限されている 
	[fifo/socket]			ストリームを使っている 
	[fifo]				FIFOストリームを使っている 
	[socket]			ソケットストリームを使っている 

{訳注: 以下日本語メッセージの場合: 
	ロング		ショート	意味 ~ 
	[読込専用]	[読専]		ファイルは書き込み制限されている 
	[FIFO/ソケット]			ストリームを使っている 
	[FIFO]				FIFOストリームを使っている 
	[ソケット]			ソケットストリームを使っている 
}
```


## 推奨設定

ヘルプを書くのに便利な設定がいくつかある。

### Conceal 文字の可視化

行末の `_>` (`_` は半角空白) と行頭の `<` はコードブロックをハイライトするためのキーワードになっている。これらはデフォルトでは conceal されるので、見落とさないためにも次のような設定をするとよい。

```vim
setlocal conceallevel=0
highlight Ignore ctermfg=red
```

コードブロックの直後の本文が `<` で始まってしまう場合は、語順を変えるか `<` を二重にして conceal されないようにすること。


### autofmt プラグイン

1 行は 78 桁以内である。[autofmt](https://github.com/vim-jp/autofmt) を入れて `gq` を使うと上手く整形できる (kaoriya 版には同梱)。  

```vim
" 整形用の設定例
set formatexpr=autofmt#japanese#formatexpr()  " kaoriya 版では設定済み
let autofmt_allow_over_tw = 1  " 全角文字がぶら下がりで 1 桁はみ出すのを許可
set formatoptions+=mB          " または mM
set smartindent
```

`formatoptions` には `mB` または `mM` を含めること。`mB` の場合は、行連結時にシングルバイト文字とマルチバイト文字の間に空白が入るが、`mM` の場合は空白は入らない。現時点ではシングルバイト文字とマルチバイト文字の間に空白を入れるかどうかは統一されていないため、整形時には周辺の文章に合わせて手動で調整が必要になる場合がある。

autofmt の代わりに [JpFormat.vim](https://sites.google.com/site/fudist/Home/jpformat) を使ってもよい。

次のいずれかで、はみ出た部分の色を変えるのも役に立つだろう。

```vim
syntax match Error /\%>79v.*/
```

```vim
set colorcolumn=+1
```

## 対訳表

|英語|日本語|メモ|
|:---|:-----|:---|
|abbreviation|短縮入力||
|autocommand|自動コマンド||    
|map|マップ||
|quickfix/location|quickfix/location|誤: クイックフィックス/ロケーション|
|syntax highlighting|構文強調表示、構文ハイライト、シンタックス強調表示、シンタックスハイライティング|現在は「構文強調表示」「構文ハイライト」が多い|
|user defined command、user command|ユーザーコマンド|前者は「ユーザー定義コマンド」がいいのでは?|
|(X11の) Selection|セレクション||
|external command|外部プログラム| `:!` で使用するような `ls` や `cat` などの普通のプログラム。Vim コマンドと区別するためこう訳す|
|Introduction|はじめに||
|default|標準設定、標準の、初期設定、デフォルト|なるべく「デフォルト」はさけたい (**nested memo:** why?)|
|forward/backward|前方/後方||
|before/after|前/後ろ|誤: 前方/後方|
|{not in Vi}|{Vi にはない}||


### カッコ

|記号|英語|日本語|メモ|
|:---|:---|:-----|:---|
|`[]`|square brackets|角カッコ||
|`{}`|brace|波カッコ||
|`()`|parenthesis|丸カッコ||
|`<>`|?|折カッコ||

漢字と記号がわかれば、どれがどれだかハッキリわかる。

**メモ:** 
  - 現状では「括弧」も多い。
  - 文字数少ないし「括弧」のほうが良いのでは?


### 記号

|記号|英語|日本語|メモ|
|:---|:---|:-----|:---|
|`` ` ``|backtick|バッククォート||
|`\`|backslash|バックスラッシュ|どこかに円記号との関連についての注意書きをした上でバックスラッシュに統一|
|`.`|dot|ドット||


### モード

```
Normal mode                     ノーマルモード
Visual mode                     ビジュアルモード
        characterwise ～        文字ビジュアルモード    （あるいは、文字単位～）
        linewise ～             行ビジュアルモード      （あるいは、行単位～）
        blockwise ～            矩形ビジュアルモード
Select mode                     選択モード
        characterwise ～        文字選択モード          （あるいは、文字単位～）
        linewise ～             行選択モード            （あるいは、行単位～）
        blockwise ～            矩形選択モード
Operator-pending mode           オペレータ待機モード
Insert mode                     挿入モード
    Replace mode                置換モード
    Virtual Replace mode        仮想置換モード
Command-line mode               コマンドラインモード
Ex mode                         Exモード
Terminal-Job mode               端末ジョブモード
```


### Vim

ソフトウェア、エディタとしての Vim を指すときには "Vim" と書く。GUI 版は "gVim"。  シェルなどで入力されるコマンドとしては "vim" もしくは "gvim" と書く。


### ファイル、オプションなど  

「ファイル」や「オプション」などは、その名前の前に書く。例:

```help
英語                   日本語 ~
.vimrc file            ファイル .vimrc
'compatible' option    オプション 'compatible'
```

> the spec file buffers  
> specがファイルの名前ではなく一般的なファイルのクラスを定義するようなものの場合はこの限りではない。  
> **メモ:** どういう意味だろう? 具体例がほしい。

**メモ:**

- 現状では徹底されていない。
- 表記や文脈から `'compatible'` や `.vimrc` でもわかるのでは? 省略したほうがすっきりする。
- 原文の順序のままでもいいのでは?


### その他

```help
{not available when compiled without the |+xxx| feature}
```

```help
{only available when compiled with the |+xxx| feature}
```

どちらも次のいずれかにする。

```help
{Vimが |+xxx| 機能付きでコンパイルされたときのみ有効}
```

```help
{|+xxx| 機能付きでコンパイルされたときのみ有効}
```

`{Vim` か `{|+xxx|` で書き始めることで構文強調表示される。


## 意見

- どのような利用者を想定するか。それによって表現が変わる。

- {not in Vi} のような表記には翻訳マニュアル独自のシンタックスファイルで対応してはどうか?

- Ex コマンドやオプションに使われるような単語はそのままカタカナにしたほうが分かりやすいのではないか?  ただカタカナばかりでは読みにくい分かりにくい。

- 「コマンドライン」は Vim のコマンドラインとシェルのコマンドラインで紛らわしい。
  * まぁ分かるか。

- 専門用語は無理せずそのままカタカナにする。
  * 必要なら別のファイルに説明を書いておく?


## 参考資料

- 辞書.辞典.翻訳.語学検索：翻訳のためのインターネットリソース
  http://www.kotoba.ne.jp/

- Excite エキサイト 翻訳 (機械翻訳)
  http://www.excite.co.jp/world/english/

- Linux JF (Japanese FAQ) Project
  http://linuxjf.sourceforge.jp/

- JF 文章文体ガイド
  http://linuxjf.sourceforge.jp/JFdocs/jf-styleguide.html

- JF で翻訳できるぞ mini HOWTO
  http://linuxjf.sourceforge.jp/JFdocs/JFhonyaku.html

- JM Project
  http://linuxjm.sourceforge.jp/

- JM Project ガイド
  http://linuxjm.osdn.jp/guide/

- 翻訳の指針
  http://linuxjm.osdn.jp/guide/translation_guideline.html

- Japanese Manual Project for FreeBSD
  http://www.jp.freebsd.org/man-jp/

- JPMANマニュアル校正ガイドライン
  http://www.jp.freebsd.org/man-jp/docs/guideline.html

- 共通な訳語の対訳表
  http://www.jp.freebsd.org/man-jp/docs/wordlist.txt

- The FreeBSD Japanese Documentation Project
  http://www.jp.freebsd.org/doc-jp/index.html

- 対訳表
  http://www.jp.freebsd.org/doc-jp/tt.html

- WIDE IPv6 WG による訳語集
  http://www.v6.wide.ad.jp/Documents/glossary.txt

- FreeBSD Security Advisory 翻訳メモ
  https://www.allbsd.org/~hrs/FreeBSD/doc-jp/announce-jp/FreeBSD-SA/freebsd-sa.txt

- X Japanese Documentation Project
  http://xjman.dsl.gr.jp/

- 翻訳の手引
  http://xjman.dsl.gr.jp/translation.html

- 訳語リスト
  http://xjman.dsl.gr.jp/dist/word.txt

- Xlib - C Language X Interface
  http://xjman.dsl.gr.jp/X11R6/X11/index.html

- 用語集
  http://xjman.dsl.gr.jp/X11R6/X11/glossary.html

- Pythonドキュメント翻訳プロジェクト
  https://github.com/python-doc-ja/python-doc-ja/wiki

- 翻訳通信
  http://www.honyaku-tsushin.net/

- 仁平和夫(にひら かずお)『翻訳のコツ』
  http://www.honyaku-tsushin.net/bn/200209SAp2.pdf

- 日本語組版処理の要件（日本語版）
  https://www.w3.org/TR/jlreq/


## ツール

- ExciteTranslate
  https://github.com/mattn/excitetranslate-vim
