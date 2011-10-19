## 作業の流れ

1. vimdoc-ja リポジトリをクローンする。
2. devel ブランチの en ディレクトリの原文ファイルを更新する。 (.jaxのみ更新する場合は不要)。
3. master ブランチの doc ディレクトリの .jax ファイルを更新する。
4. gh-pages を更新する。
5. 変更を push する。

## ブランチの説明

* `master`: ランタイムファイル。翻訳ファイルやシンタックスファイルなど。`:set runtimepath+=/path/to/vimdoc-ja/master` としてそのまま使える形。
* `devel`: 作業用のファイル。原文ファイルや html 生成スクリプトなど。その他、ランタイムファイル以外のもの。
* `gh-pages`: http://vim-jp.org/vimdoc-ja/ の html。ここのコミットするとサーバー上のファイルが更新される。

## 具体例

vimdoc-ja リポジトリをクローンする。

```sh
$ git clone git@github.com:vim-jp/vimdoc-ja.git
$ cd vimdoc-ja
```

あとで html を生成するときに `master` `devel` `gh-pages` ブランチが必要なので作っておきます。

```sh
$ git branch -t devel origin/devel
$ git branch -t gh-pages origin/gh-pages
```

原文ファイルを更新する。

```sh
$ git checkout devel
$ cp /path/to/vim/runtime/doc/foo.txt en/foo.txt
$ git commit -a -m "..."
```

原文の差分を見つつ作業します。

```sh
$ git diff devel~2..devel~1 | gvim -
```

翻訳ファイルを更新する。

```sh
$ git checkout master
$ vim doc/foo.jax
$ git commit -a -m "..."
```

gh-pages 用の html を生成する。

```sh
$ git checkout devel
$ vim -u tools/buildhtml.vim
```

生成された html を確認して問題なければ pull します。

```sh
$ cd html
$ git diff HEAD^ | gvim -
$ cd ..
$ git checkout gh-pages
$ git pull html gh-pages
```

最後、remote に push して完了。

```sh
$ git push
```
