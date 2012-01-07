作業手順
========

## 作業の流れ

1. vimdoc-ja リポジトリをクローンする。
2. 原文ファイルを更新する。
3. 翻訳ファイルを更新する。
4. Web サイトを更新する。
5. 変更を push する。

## ブランチの説明

* `master`: ランタイムファイル。翻訳ファイルやシンタックスファイルなど。`:set runtimepath+=/path/to/vimdoc-ja/master` としてそのまま使える形。
* `devel`: 作業用のファイル。原文ファイルや html 生成スクリプトなど。その他、ランタイムファイル以外のもの。
* `gh-pages`: http://vim-jp.org/vimdoc-ja/ の html。ここにコミットするとサーバー上のファイルが更新される。

## 例

### vimdoc-ja リポジトリをクローンする。

```sh
$ git clone git@github.com:vim-jp/vimdoc-ja.git
$ cd vimdoc-ja
```

あとで html を生成するときに `master` `devel` `gh-pages` ブランチが必要なので作っておきます。

```sh
$ git branch -t devel origin/devel
$ git branch -t gh-pages origin/gh-pages
```

### 原文ファイルを更新する。

Vim のソースは http://code.google.com/p/vim/ から取得できます。ソースの取得には hg を使います。

```sh
$ hg clone https://code.google.com/p/vim/
```

クローン済みのリポジトリを最新に更新するには `hg pull` を実効します。

```sh
$ cd /path/to/vim
$ hg pull --update
```

更新したい原文ファイルを vimdoc-ja の devel ブランチにコピーします。

```sh
$ git checkout devel
$ cp /path/to/vim/runtime/doc/foo.txt en/foo.txt
$ git commit -a -m "..."
```

原文の差分を見つつ翻訳ファイルを更新していきます。

```sh
$ git diff devel~2..devel~1 | gvim -
```

### 翻訳ファイルを更新する。

```sh
$ git checkout master
$ vim doc/foo.jax
$ git commit -a -m "..."
```

### Web サイトを更新する。

翻訳ファイルから html を生成します。

```sh
$ git checkout devel
$ vim -u tools/buildhtml.vim
```

`git clone . html` によってリポジトリがクローンされ、その中で html ファイルが生成されます。

生成された html ファイルを確認して問題なければ取り込みます。

```sh
$ cd html
$ git diff HEAD^ | gvim -
$ git push ..
$ cd ..
```

### 変更を push する。

remote に push して完了です。

```sh
$ git push
```

