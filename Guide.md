Vim ドキュメント翻訳者の手引き
=============================

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

- 行末の「 >」及び行頭の「<」  
  これらはサンプルを示すsyntax hightlightをかけるためのキーワードになっている
  。helpIgnoreグループになっているので、見落とさないように色を変えておいた方が
  よい。
  :hi Ignore ctermfg=red
  :syn match Error /\%>79v.*/

- 1行は78カラム以内  
  kaoriya版に付属のformat.vimを入れてgqを使うとそのように整形できる。

- 口調  
  「だ、である」調にする
  個人的には「です、ます」調が好み
  リファレンスマニュアルとユーザーマニュアルで使い分けるのもあり?

- 句読点は「、」と「。」を使用する

- 訳注  
  注釈には、原文を捕捉するものと、翻訳者の作業用メモ、の 2 種類がある  
  行単位で書くと小細工できて都合がいい  
訳注: 原文が分かり難いようだったら  
訳注: このように注釈を入れ捕捉する  
訳注メモ: こんな感じでリリースに含めないようなメモを書く  
訳注メモ: 作業ログ、疑問、注意点など、他の翻訳者が後で参照できるようにする  
訳注メモ: リリースに含めないと利用者からのフィードバックを得られないか?  
訳注メモ: 消さないほうが利用者にとって分かりやすいか?  
訳注メモ: 名前も入れておくと分かりやすい?

- ファイル形式  
  文字コードは UTF-8  
  改行文字は UNIX 形式(\n)  
  :set fileencoding=utf-8 fileformat=unix

- _not_ や ALL などの強調表現  
  全角のバッククォート (‘) で始まり、シングルクォート (’) で終わりを括る。
  日本語的な表現ではないのでなにもしなくていいのではないか?
  というか非日常的な記号は使いたくない

- 命令形で書かれている文  
  リファレンスマニュアルなので、命令しているというよりは操作の手順を簡潔に述
  べているだけであって、特に命令形だからという意識はしなくて良い。

- backtick(`)  
  バッククォート

- backslash(\)  
  バックスラッシュ  
  マニュアルのどこかで円記号との関連についての注意書きをした上で、あとはバッ
  クスラッシュに統一する。

- カッコの名前  
  square brackets([])  
  brace({})  
  parenthesis(())  
  () 丸カッコ  
  [] 角カッコ  
  {} 波カッコ  
  <> 折カッコ  
  漢字と記号がわかれば、どれがどれだかハッキリわかる

- dot(.)  
  ドット

- Introduction  
  はじめに

- {not in Vi}  
  {Vi にはない}

- {not available when compiled without the |+cindent| feature}  
  {}

- external command  
  |:!|で使用するような、"ls"や"cat"などいわゆる普通のプログラム  
  Vimのコマンドと特に区別して
  「外部プログラム」

- syntax highlighting  
  構文強調表示
  シンタックスハイライティング
  シンタックス強調表示
  構文ハイライト

- Vim の表記  
  一般名称として、ソフトウェア、エディタとしてのVimを指す時には「Vim」と書く。
  シェルなどで入力されるコマンドとしては「vim」もしくは「gvim」と書く。

- ファイル、オプションその他の表記  
  'compatible' option ... == オプション'compatible'  
  .vimrc file == ファイル.vimrc  
  というように型というかクラスというか、そういうものを書くときはその名前の前
  に前置するよう統一する。ただし現状では徹底してない。  
  the spec file buffers  
  specがファイルの名前ではなく一般的なファイルのクラスを定義するようなものの
  場合はこの限りではない。
  表記や文脈から'compatible'や.vimrcでもわかる?省略したほうがすっきりする

- Selection (X11の)  
  セレクション

- default  
  標準設定、標準の、初期設定、デフォルト
  なるべくデフォルトはさけたい

- map → マップ
- abbreviation → 短縮入力
- user defined command, user command → ユーザーコマンド

意見
------

どのような利用者を想定するか。それによって表現が変わる。

{not in Vi}
のような表記には翻訳マニュアル独自のシンタックスファイルで対応してはどうか

Ex コマンドやオプションに使われるような単語はそのままカタカナにしたほうが
分かりやすいのではないか?
ただしカタカナばかりでは読みにくい分かりにくい

モードの名前は漢字かカタカナか統一したほうがいいと思う
思い切って Normal モードとか Insert モードとかでもいい気がする

コマンドラインはVimのコマンドラインとシェルのコマンドラインで紛らわしい
まぁ分かるか

専門用語は無理せずそのままカタカナにする
必要なら別のファイルに説明を書いておく?


参考資料
--------

辞書.辞典.翻訳.語学検索：翻訳のためのインターネットリソース
  http://www.kotoba.ne.jp/

IBM 情報処理用語英和対訳集
  http://www-6.ibm.com/jp/manuals/nlsdic/nlsdic.html

Excite エキサイト 翻訳 (機械翻訳)
  http://www.excite.co.jp/world/english/

Linux JF (Japanese FAQ) Project
  http://www.linux.or.jp/JF/

JF 文章文体ガイド
  http://www.linux.or.jp/JF/JFdocs/jf-styleguide.html

JF で翻訳できるぞ mini HOWTO
  http://www.linux.or.jp/JF/JFdocs/JFhonyaku.html

JM Project
  http://www.linux.or.jp/JM/

JM 翻訳作業の手引き
  http://www.linux.or.jp/JM/guidance/index.html

翻訳の指針
  http://www.linux.or.jp/JM/guidance/translation_note.html

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
  http://home.jp.freebsd.org/%7Ehrs/doc-jp/freebsd-sa.txt

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

Mozilla Japan 翻訳部門
  http://www.mozilla-japan.org/jp/td/

参考資料
  http://www.mozilla-japan.org/jp/td/links.html

Pythonドキュメント翻訳プロジェクト
  http://www.python.jp/Zope/pythondoc_jp/index_html

翻訳通信
  http://homepage3.nifty.com/hon-yaku/tsushin/

仁平和夫(にひら かずお)『翻訳のコツ』
  http://homepage3.nifty.com/hon-yaku/tsushin/bn/200209SAp2.pdf


ツール
-----

ExciteTranslate
  https://github.com/mattn/excitetranslate-vim