# 作業手順


## 作業の流れ

1.  本リポジトリをクローンする
2.  master から作業ブランチを作成する
3.  原文ファイルを更新する (vim/vim からコピーする)
4.  翻訳ファイルを翻訳・更新する
5.  作業ブランチを push して Pull Request (PR)を作成する
    *   原文ファイルの更新と翻訳ファイルの更新が1つのPRに入るようにする
    *   表記の統一をした場合はdict.ymlの更新も一緒に行う


##  本リポジトリをクローンする

### vimdoc-ja-working へのコミット権がある場合

以下の手順で、本リポジトリをクローンできます。

    $ cd /path/to
    $ git clone git@github.com:vim-jp/vimdoc-ja-working.git


### vimdoc-ja-working へのコミット権がない場合

github での通常の作法と同様に、フォーク＆クローンした後、下記の要領で作業を行い、
フォーク先のレポジトリへコミット&プッシュした後、PRを作成してください。


## master から作業ブランチを作成する

以下の手順で master から作業ブランチを作成できます。

    $ cd /path/to/vimdoc-ja-working
    $ git checkout master
    $ git pull
    $ git checkout -b my-translation

`my-translation` は、適切なブランチ名を付けて、置き換えてください。


## 原文ファイルを更新する

最新の原文ファイルを取得し、作業ブランチを更新します。
Vim のソースは https://github.com/vim/vim から取得できます。
ソースの取得には git を使います。

    $ cd /path/to
    $ git clone https://github.com/vim/vim.git

クローン済みのリポジトリを最新に更新するには `git pull` を実行します。

    $ cd /path/to/vim
    $ git pull

更新したい原文ファイル (以下の例では foo.txt としてます) を vimdoc-ja-working にコピーします。

    $ cd /path/to/vimdoc-ja-working
    $ cp /path/to/vim/runtime/doc/foo.txt en/foo.txt

原文の差分を見つつ翻訳ファイルを更新していきます。

    $ git diff -- en

原文の変更を予めコミットしてから翻訳作業をしても良いです。

    $ git commit -a -m "update original doc..."
    $ git diff HEAD^2...HEAD^1 -- en
    $ git diff master...HEAD -- en


## 翻訳ファイルを翻訳・更新する

特に説明することはありません。
以下の手順を参考にしてください。
翻訳のお作法については [手引き](https://github.com/vim-jp/vimdoc-ja-working/wiki/Guide) を参照してください。
特に、ヘルプ特有の構文を知らない方は `:help help-writing` を一読することをお勧めします。

    $ cd /path/to/vimdoc-ja-working
    $ vim doc/foo.jax
    $ git commit -a -m "..."

翻訳をこまめにコミットしても良いです。


## 作業ブランチを push して Pull Request (PR)を作成する

作業ブランチを push して PR を作成したら、作業完了です。
レビューを受け、修正しつつマージを待ちましょう。

    $ git push -u origin my-translation

master へマージされると、通常は5分くらいで vimdoc-ja の Web と配布用ファイルへ反映されます。