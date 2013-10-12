# 作業手順

## 作業の流れ

1.  作業用ブランチを取り出す (vimdoc-ja リポジトリをクローンする)
2.  原文ファイルを更新する
3.  翻訳ファイルを更新する
4.  Web サイトを更新する
5.  変更を push する

## ブランチの説明

*   `devel`: 作業用のブランチ。
    原文、翻訳文、HTML 生成スクリプトなどのファイルが格納されている。
    通常はこのブランチのみで作業する
*   `master`: 配布用のブランチ。 
    **devel ブランチを更新すると自動で更新されるので通常は作業しない。**
    翻訳ファイルやシンタックスファイルなど。
    `:set runtimepath+=/path/to/vimdoc-ja/master` として使える形を維持する
*   `gh-pages`: HTML公開用のブランチ。 
    **devel ブランチを更新すると自動で更新されるので通常は作業しない。**
    http://vim-jp.org/vimdoc-ja/ の HTMLが格納される

## 作業用ブランチを取り出す

```sh
$ git clone -b devel git@github.com:vim-jp/vimdoc-ja.git
```

vimdoc-ja ディレクトリに作業用ブランチが取得できます。

## 原文ファイルを更新する

最新の原文ファイルを取得し、develブランチを更新します。
Vim のソースは http://code.google.com/p/vim/ から取得できます。
ソースの取得には hg を使います。

```sh
$ hg clone https://code.google.com/p/vim/
```

クローン済みのリポジトリを最新に更新するには `hg pull` を実行します。

```sh
$ cd /path/to/vim
$ hg pull --update
```

更新したい原文ファイルを vimdoc-ja にコピーします。

```sh
$ cd /path/to/vimdoc-ja
$ cp /path/to/vim/runtime/doc/foo.txt en/foo.txt
$ git commit -a -m "..."
```

原文の差分を見つつ翻訳ファイルを更新していきます。

```sh
$ git diff devel~2..devel~1 | gvim -
```

## 翻訳ファイルを更新する

```sh
$ cd /path/to/vimdoc-ja
$ vim doc/foo.jax
$ git commit -a -m "..."
```

## 変更を push する

リモートの devel ブランチへ push して完了です。

```sh
$ git push
```

しばらく(最大20分程度)すると master と gh-pages ブランチが自動的に更新され、
あなたの翻訳が公開されます。
