Vim ドキュメント翻訳者の手引き
=============================

- ヘルプの書き方  
  日本語訳に限らない一般的なVimのヘルプの書き方は `:help help-writing` を参照  
  翻訳については `:help help-translated` も参照

- 半角と全角  
  ASCII文字は半角文字を使う  
  カタカナは全角文字を使う

- 数字  
  漢数字(一、二)ではなく、算用数字(1, 2)を使う  
  ただし、一時的、統一、など、日本語の一部は漢数字

- 文中に英数字がある場合には前後に空白を入れる。  
  例: 文の中に 1 つの English が混ざる。But 句読点の前後は空白なし。  
  他の翻訳プロジェクトでも空白を入れているところ多し  
  ただ、空白を入れないほうが書きやすいし読みやすいと感じる  
  ファイル名やコマンド、コード片などは空白で区切った方が分かりやすいのでは？

  "～"、'～'、\`～\` のように引用符でくくられている部分は、くくられている部分を明確にするため、前後に空白を入れる。  
  ただし、英数字同様に句読点の前後は空白なし。|～| によるリンクも同様。

- 行末の `␣>` (`␣`は半角空白) 及び行頭の `<`  
  これらはサンプルを示すsyntax hightlightをかけるためのキーワードになっている。helpIgnoreグループになっているので、見落とさないように色を変えておいた方がよい。
  ```vim
  :hi Ignore ctermfg=red
  ```
  サンプル直後の本文が `<` で始まる場合は、語順を変えるか `<` を2重にして非表示にされないようにする。

- 1行は78カラム以内  
  [autofmt](https://github.com/vim-jp/autofmt)を入れてgqを使うとそのように整形できる。(kaoriya版には同梱)  
  (あるいは、[JpFormat.vim](https://sites.google.com/site/fudist/Home/jpformat))
  ```vim
  " 整形用の設定例
  :set formatexpr=autofmt#japanese#formatexpr()  " kaoriya版では設定済み
  :let autofmt_allow_over_tw=1                   " 全角文字がぶら下がりで1カラムはみ出すのを許可
  :set formatoptions+=mB     " または mM
  :set smartindent
  ```
  'formatoptions' には "mB" または "mM" を含めること。"mB" の場合は、行連結時にシングルバイト文字とマルチバイト文字の間に空白が入るが、"mM" の場合は空白は入らない。現時点ではシングルバイト文字とマルチバイト文字の間に空白を入れるかどうかは統一されていないため、整形時には周辺の文章に合わせて手動で調整が必要になる場合がある。

  以下のいずれかで、はみ出た部分の色を変えるのもよい。
  ```vim
  :syn match Error /\%>79v.*/
  ```
  ```vim
  :set cc=+1
  ```


- 口調  
  ユーザーマニュアルは「です、ます」調に統一する。  
  現状、リファレンスマニュアルは「だ、である」調が多いが、一部「です、ます」調のファイルもある。少なくとも1つのファイル内では統一しておきたい。
  箇条書き部分やサンプルコードのコメント部分は「だ、である」調にすること。


- 句読点は「、」と「。」を使用する

- 丸括弧は全角の「（」および「）」ではなく半角括弧+空白「 (」および「) 」を使う。

- 訳注  
  注釈には、原文を補足するものと、翻訳者の作業用メモ、の 2 種類がある  
  補足の場合は、`{訳注: 補足}` の形式にする。(構文強調される)

  行単位で書くと小細工できて都合がいい
  ```
  訳注メモ: こんな感じでリリースに含めないようなメモを書く  
  訳注メモ: 作業ログ、疑問、注意点など、他の翻訳者が後で参照できるようにする  
  訳注メモ: リリースに含めないと利用者からのフィードバックを得られないか?  
  訳注メモ: 消さないほうが利用者にとって分かりやすいか?  
  訳注メモ: 名前も入れておくと分かりやすい?
  ```

- ファイル形式  
  文字コードは UTF-8  
  改行文字は UNIX 形式(`\n`)
  ```vim
  :set fileencoding=utf-8 fileformat=unix
  ```

  ファイルによっては cp932 などでは扱えない文字を含んでいるので、`:set encoding=utf-8` もしておいた方がよいと思われる。  


- `_not_` や `ALL` などの強調表現  
  全角のバッククォート (‘) で始まり、シングルクォート (’) で終わりを括る。
  日本語的な表現ではないのでなにもしなくていいのではないか?
  というか非日常的な記号は使いたくない

- 命令形で書かれている文  
  リファレンスマニュアルなので、命令しているというよりは操作の手順を簡潔に述
  べているだけであって、特に命令形だからという意識はしなくて良い。

- 日本語環境だと翻訳されるメッセージ  
  `:language messages ja_JP` などの日本語環境では、一部のメッセージが日本語に翻訳される。そのようなメッセージは**本文中では原文のままにし、その日本語訳を訳注で記載する**こと。基本的に一つのメッセージに対して一つの訳注をつければよいが、くどくなる場合は複数のメッセージに対して一つの訳注をつけてもよい。例：
  
  `1` 訳注 / `1` メッセージ
  ```
  	h F   ヘルプバッファフラグ。表示されるのは "[help]"。
  	      {訳注: 日本語メッセージの場合: "[ヘルプ]"}
  	H F   ヘルプバッファフラグ。表示されるのは ",HLP"。
  	w F   プレビューウィンドウフラグ。表示されるのは "[Preview]"。
  	      {訳注: 日本語メッセージの場合: "[プレビュー]"}
  ```

  `1` 訳注 / `n` メッセージ（`n >= 2`）
  ```
   							*read-messages* 
   ファイルを読み込むときVimはその情報を表示する。いくつかのものについての説明 
   をあげる。他のものは見ればわかる。ロングとショートのどちらを使うかは 
   'shortmess' オプションに依存する。 
    
   	ロング		ショート	意味 ~ 
   	[readonly]	{RO}		ファイルは書き込み制限されている 
   	[fifo/socket]			ストリームを使っている 
   	[fifo]				FIFOストリームを使っている 
   	[socket]			ソケットストリームを使っている 
   	[CR missing]			"dos" ファイルフォーマットで読み込ん 
   					でいてCRのないNLを見つけた 
   	[NL found]			"mac" ファイルフォーマットで読み込ん 
   					でいてNLを見つけた(unixフォーマット 
   					なのだろう) 
   	[long lines split]		少なくとも1つの行が2つに分割された 
   	[NOT converted]			'fileencoding' から 'encoding' の変換 
   					が失敗した 
   	[converted]			'fileencoding' から 'encoding' の変換 
   					を実施した 
   	[crypted]			暗号が解除された 
     	[READ ERRORS]			ファイルを全て読み込めなかった 
  
   {訳注: 以下日本語メッセージの場合: 
   	ロング		ショート	意味 ~ 
   	[読込専用]	[読専]		ファイルは書き込み制限されている 
   	[FIFO/ソケット]			ストリームを使っている 
   	[FIFO]				FIFOストリームを使っている 
   	[ソケット]			ソケットストリームを使っている 
   	[CR無]				"dos" ファイルフォーマットで読み込ん 
   					でいてCRのないNLを見つけた 
  ```

- backtick (`` ` ``)  
  バッククォート

- backslash (`\`)  
  バックスラッシュ  
  マニュアルのどこかで円記号との関連についての注意書きをした上で、あとはバッ
  クスラッシュに統一する。

- カッコの名前  
  square brackets (`[]`)  
  brace (`{}`)  
  parenthesis (`()`)  
  `()` 丸カッコ  
  `[]` 角カッコ  
  `{}` 波カッコ  
  `<>` 折カッコ  
  漢字と記号がわかれば、どれがどれだかハッキリわかる
  メモ:
    - 現状では「括弧」も多い。文字数少ないし「括弧」のほうが良いのでは?

- dot (`.`)  
  ドット

- Introduction  
  はじめに

- {not in Vi}  
  {Vi にはない}

- {not available when compiled without the |+cindent| feature}  
  {only available when compiled with the |+multi_byte| feature}  

  否定形・肯定形にかかわらず、どちらも  
  {Vimが |+xxxx| 機能付きでコンパイルされたときのみ有効}  
  の形式で統一。(`{Vim` で書き始めることで構文ハイライトされる。)  
  あるいは、  
  {|+xxxx| 機能付きでコンパイルされたときのみ有効}  
  でもよい。(`{|+xxxx|` 形式で書き始めても構文ハイライトされる。)  

- autocommand  
  自動コマンド

- external command  
  `|:!|`で使用するような、`ls`や`cat`などいわゆる普通のプログラム  
  Vimのコマンドと特に区別して
  「外部プログラム」

- syntax highlighting  
  構文強調表示  
  シンタックスハイライティング  
  シンタックス強調表示  
  構文ハイライト
  メモ:
    - 現状では構文{強調表示,ハイライト}が多い

- Vim の表記  
  一般名称として、ソフトウェア、エディタとしてのVimを指す時には「Vim」と書く。GUI版は「gVim」。  
  シェルなどで入力されるコマンドとしては「vim」もしくは「gvim」と書く。

- ファイル、オプションその他の表記  
  'compatible' option ... == オプション 'compatible'  
  .vimrc file == ファイル .vimrc  
  というように型というかクラスというか、そういうものを書くときはその名前の前に前置するよう統一する。ただし現状では徹底してない。  
  the spec file buffers  
  specがファイルの名前ではなく一般的なファイルのクラスを定義するようなものの場合はこの限りではない。  
  表記や文脈から 'compatible' や.vimrcでもわかる?省略したほうがすっきりする

- Selection (X11の)  
  セレクション

- default  
  標準設定、標準の、初期設定、デフォルト
  なるべくデフォルトはさけたい

- map → マップ
- abbreviation → 短縮入力
- user defined command, user command → ユーザーコマンド

- forward/backward → 前方/後方 固定とする。
- before/after → 前/後ろ (前方/後方 と訳さない)
- quickfix/location → そのまま quickfix/location とする。 (クイックフィックス/ロケーション と訳さない)

- モードの名称
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

意見
------

どのような利用者を想定するか。それによって表現が変わる。

{not in Vi}
のような表記には翻訳マニュアル独自のシンタックスファイルで対応してはどうか

Ex コマンドやオプションに使われるような単語はそのままカタカナにしたほうが分かりやすいのではないか?  
ただしカタカナばかりでは読みにくい分かりにくい

コマンドラインはVimのコマンドラインとシェルのコマンドラインで紛らわしい  
まぁ分かるか

専門用語は無理せずそのままカタカナにする  
必要なら別のファイルに説明を書いておく?


参考資料
--------

辞書.辞典.翻訳.語学検索：翻訳のためのインターネットリソース
  http://www.kotoba.ne.jp/

Excite エキサイト 翻訳 (機械翻訳)
  http://www.excite.co.jp/world/english/

Linux JF (Japanese FAQ) Project
  http://linuxjf.sourceforge.jp/

JF 文章文体ガイド
  http://linuxjf.sourceforge.jp/JFdocs/jf-styleguide.html

JF で翻訳できるぞ mini HOWTO
  http://linuxjf.sourceforge.jp/JFdocs/JFhonyaku.html

JM Project
  http://linuxjm.sourceforge.jp/

JM Project ガイド
  http://linuxjm.osdn.jp/guide/

翻訳の指針
  http://linuxjm.osdn.jp/guide/translation_guideline.html

Japanese Manual Project for FreeBSD
  http://www.jp.freebsd.org/man-jp/

JPMANマニュアル校正ガイドライン
  http://www.jp.freebsd.org/man-jp/docs/guideline.html

共通な訳語の対訳表
  http://www.jp.freebsd.org/man-jp/docs/wordlist.txt

The FreeBSD Japanese Documentation Project
  http://www.jp.freebsd.org/doc-jp/index.html

対訳表
  http://www.jp.freebsd.org/doc-jp/tt.html

WIDE IPv6 WG による訳語集
  http://www.v6.wide.ad.jp/Documents/glossary.txt

FreeBSD Security Advisory 翻訳メモ
  https://www.allbsd.org/~hrs/FreeBSD/doc-jp/announce-jp/FreeBSD-SA/freebsd-sa.txt

X Japanese Documentation Project
  http://xjman.dsl.gr.jp/

翻訳の手引
  http://xjman.dsl.gr.jp/translation.html

訳語リスト
  http://xjman.dsl.gr.jp/dist/word.txt

Xlib - C Language X Interface
  http://xjman.dsl.gr.jp/X11R6/X11/index.html

用語集
  http://xjman.dsl.gr.jp/X11R6/X11/glossary.html

Pythonドキュメント翻訳プロジェクト
  https://github.com/python-doc-ja/python-doc-ja/wiki

翻訳通信
  http://www.honyaku-tsushin.net/

仁平和夫(にひら かずお)『翻訳のコツ』
  http://www.honyaku-tsushin.net/bn/200209SAp2.pdf

日本語組版処理の要件（日本語版）
  https://www.w3.org/TR/jlreq/

ツール
-----

ExciteTranslate
  https://github.com/mattn/excitetranslate-vim