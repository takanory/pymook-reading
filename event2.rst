================================================
 第2回 便利なライブラリ、パッケージとチーム開発
================================================

.. contents:: 目次
   :local:

はじめに
========
鈴木たかのりです。

`前回 <http://gihyo.jp/news/report/01/python-training-book-reading-club/0001>`_
に引き続き
`Pythonエンジニア養成読本 <http://gihyo.jp/book/2015/978-4-7741-7320-7>`_
という書籍の `読書会イベント <http://pymook.connpass.com/>`_ についてレポートします。

`第2回の読書会 <http://pymook.connpass.com/event/15198/>`_ は6月18日(木)に `アライドアーキテクツ株式会社 <http://www.aainc.co.jp/>`_ の会議室で開催されました。

当日はだいたい以下のタイムテーブルで進めました。

- 19:00-19:15 参加者の自己紹介
- 19:15-19:45 「Appendix1 便利な標準ライブラリ、サードパーティ製パッケージ」
- 19:45-21:00 「第3章 チーム開発」
- 21:00-22:00 ビアバッシュ(ビールとピザでの参加者懇親会)

今回も前回と同様書籍の読みあわせは行わず、ざっと内容について解説をしたあとに質疑応答を中心に進めました。

自己紹介
========
最初に全体で自己紹介を行いました。全部で23名の方が参加してくださいました。
また、今回は著者6名のうち5名が参加していました。
全体としては1/3が初参加、2/3が2回目の参加という感じでした。

自己紹介の中では2回目参加の方の中で「会社でちょっとしたスクリプトをPythonで書き始めた」「PyCharmを使い始めた」といったように、前回の内容を踏まえて進展があった内容が印象的でした。
今後も、3回、4回と継続していく中で、参加者の方の新しい成果が自己紹介で聞けるといいなと思いました。

Appendix1 便利な標準ライブラリ、サードパーティ製パッケージ
==========================================================
Appendix1は私の担当です。
今回は前回の反省を踏まえて、最初に自己紹介を行いました。
`@takanory <https://twitter.com/takanory>`_ のTwitterの画面を見せつつ、
先週は台湾で開催された `PyCon APAC 2015 <https://tw.pycon.org/2015apac/en/>`_ に参加していたことや、
ちょうどこの日は `PyCon Singapore 2015 <https://pycon.sg/>`_ が開催中で、知り合いのshimizukawaさんが参加している、といった話をしました。

以下はPyCon APAC 2015の集合写真のツイートです。どこかに筆者がいます。

.. raw:: html

   <blockquote class="twitter-tweet" lang="en"><p lang="en" dir="ltr">Remember the exciting moments? Photos here! <a href="http://t.co/sECvyoE7eV">http://t.co/sECvyoE7eV</a> <a href="https://twitter.com/hashtag/pyconapac2015?src=hash">#pyconapac2015</a> <a href="http://t.co/DFsZEqovms">pic.twitter.com/DFsZEqovms</a></p>&mdash; PyConTW (@PyConTW) <a href="https://twitter.com/PyConTW/status/611410021948243968">June 18, 2015</a></blockquote>
   <script async src="http://platform.twitter.com/widgets.js" charset="utf-8"></script>

PyCon APAC、PyCon Singaporeについては `gihyo.jp <http://gihyo.jp/>`_ の以下の連載記事でレポートされています。
こちらもぜひ読んでみてください。

- `台湾で開催された「PyCon APAC 2015」参加レポート <http://gihyo.jp/news/report/01/pycon-apac-2015>`_
- `海外PyCon発表修行レポート2015 <http://gihyo.jp/news/report/01/overseas-pycon-presentation-training-2015>`_
  
Pythonの付属バッテリー、標準ライブラリ
--------------------------------------
この節では、Pythonをインストールすると付属してくる標準ライブラリについて一部を紹介しています。
最近のプログラミング言語では一般的だと思いますが、Pythonでもインストールするとさまざまな便利な標準ライブラリが使えるようになります。
「こんなのあるといいな」と思ったらとりあえず標準ライブラリを探すと、だいたいすでに提供されているので、ぜひライブラリの一覧を見てくださいという話をしました。

Python標準ライブラリについては下記のドキュメントにまとまっています。
日本語化もされており、
`Python ドキュメント日本語訳プロジェクト <https://github.com/python-doc-ja/python-doc-ja>`_
のみなさんには非常に感謝しています。

- `Python 標準ライブラリ — Python 2.7 <http://docs.python.jp/2/library/>`_
- `Python 標準ライブラリ — Python 3.4.3 <http://docs.python.jp/3.4/library/index.html>`_

書籍ではたくさんあるライブラリのうち「これくらいは知っておいたほうがいいかな」という一部のライブラリのさらに一部の機能だけを紹介しています。

例えばOS依存の機能を操作するosモジュールでは以下のディレクトリ操作を行うコードを紹介しました。
実際には `osモジュールのドキュメント <http://docs.python.jp/2.7/library/os.html>`_
を見てみると、たくさんのメソッドが用意されています。

.. code-block:: python
   :caption: osモジュールのサンプルコード

   >>> import os
   >>> os.mkdir('spam')  # ディレクトリを作成
   >>> os.chdir('spam')  # ディレクトリを移動
   >>> os.getcwd()       # 現在のディレクト名を取得
   '/Users/takanori/spam'

ここでは質疑応答で、書籍で紹介している以外によく使うライブラリはなにか?という話が出ました。

書籍の中で紹介しているライブラリは以下の通りです。

- sys - システムパラメータと関数へのアクセス
- os - オペレーティングシステムインタフェース
- time - 時刻データへのアクセスと変換
- datetime - 基本的な日付型および時間型
- math - 数学関数
- random - 擬似乱数の生成
- itertools - 効率的なループ実行のためのイテレータ生成関数
- shutil - 高レベルなファイル操作
- json - JSON エンコーダおよびデコーダ

ここで回答としてあがったのは以下のライブラリでした。

- urllib, urllib2 - URLでのリソースへのアクセス
- urlparse - URLの文字列解析
- logging - ログ出力
- argparse - コマンドラインオプションの解析

別の方から「shutilでできることはosでできるのではないか?」という質問がありました。
答えはそのとおりですが、例えばshutilだと ``copytree(src, dst)`` でディレクトリツリーをまとめてコピーしてくれますが、osモジュールで実装しようとすると、自分でディレクトロとファイルを走査して一つづつコピーするなど大変です。そういう意味でも shutil はユーティリティー的に便利な機能を提供してくれています。

余談として **logging** はバッチファイルなどでも途中経過を出力するときに使うと便利であるという話をしました。
また、コマンドライン引数の処理は **optparse** と **argparse** が標準ライブラリにありますが、個人的にはargparseがお勧めであるという話もしました。

- pipコマンドをWindowsで→sudoしなければOK
- shutil, re
- argparse
- logging
- shutilはosでできるけど、より楽にしてくれる

Pythonをさらに強力にするサードパーティ製パッケージ
--------------------------------------------------
この節では標準ライブラリ以外に多数のサードパーティ製パッケージが提供されていることを紹介しています。
Pythonでは `PyPI: Python Package Index <https://pypi.python.org/pypi>`_ というサイトで提供されており、 **pip** コマンドでインストールして使用できます。

ここで「Windowsで書いてある通りにpipをインストールができなかった」という質問がありました。書籍上のコードではLinuxを想定しいるので **sudo** でrootユーザーになってpipをインストールしています。
「Windowsではsudoはおそらく不要である」という回答をしましたが、無事pipコマンドがインストールできたようです。

ちなみにpipのインストールは ``https://bootstrap.pypa.io/get-pip.py`` をダウンロードして ``python get-pip.py`` を実行して行います。
詳細は
`Installation <https://pip.pypa.io/en/stable/installing.html>`_
ドキュメントを参照してください。

また、ここではよいパッケージを探す指標として、更新の履歴やダウンロード数がPyPIで確認できるので、それを見ると良いという話をしました。
例えばHTTPアクセスを人にわかりやすい形で記述できる
`requests <https://pypi.python.org/pypi/requests/2.7.0>`_
は、今年の5月の2.7.0まで継続的に開発されており、1日に174,718もダウンロードされていてよく使われていることがわかります。

他によりパッケージを探す手段として
`Stack Overflow <http://stackoverflow.com/>`_ で検索して回答を見るという方法が紹介されていました。確かに有用な方法だと思いますので、おすすめです。

まとめとしては、標準ライブラリ、サードパーティ製パッケージたくさん便利なものが用意されているので、ぜひいいものもを見つけて活用してほしいなという話をしました。

第3章 開発環境とチーム開発
==========================

3-1 開発環境とチーム開発に求められること
----------------------------------------

3-2 GitとGitHub
---------------
- git, github 使っていない人そこそこいる
- ブランチはどの単位できってる?

  - 機能単位。redmine, github issueの単位で作る
  - fix shimada チケット番号
  - ブランチは人に紐付いている
  - owner変わったらブランチ名変わる→切り直す

- 普段はcli, sourcetreeは手になじまない
- コンフリクトしたときcliだと大変じゃないですか

  - ガッツで乗り切っている

- gitをデザイナーさんにどうやって使ってもらうか

  - メールとかでもらったものを代わりにcommitしてもらっている
  - 答えはない...

- http://blog.uni-q.net/entry/2014/08/06/194117
- C86：新刊「イメージできるGit」の告知 - Uni-Q blog http://blog.uni-q.net/entry/2014/08/06/194117

- github: 人のリポジトリを直したいとき、forkして修正してPull Reqeustを送って取り込んでもらうことができる
- 仕事で github 使っている

  - 一緒に仕事をしている人が bitbucket を使っていない
  - この本は bitbucket + mercurial で書いた

- github ってネット上にある。企業で開発している人もコードを乗せちゃうと見れちゃう?

  - 無料プランは公開リポジトリしか作れない
  - お金を払うとプライベートリポジトリが作成できる
  - 個人でプライベートリポジトリを作るなら bitbucket がおすすめ

3-3 virtualenv
--------------
- バージョンがそれぞれで持てるよ
- activate, deactivate
- virtualenvwrapper 等の付随するツールがあるので、それを使うと楽かも

  - 2系と3系のvirtualenvの下にさらにvirtualenv作ってる
  - 使い方は人それぞれ

- Windowsでファイルの関連付けは変わらない?

  - ダブルクリック起動だとだめそう

- 本番環境に持って行く時はどうしている?

  - opsworksを使って、deploy script の中で virtualenv の環境を作る
  - pip freeze の話→バージョン固定で書きだされる
  
3-4 テストと品質
----------------
- テスト手でやると大変なので、ユニットテストを書く
- doctestの説明
- doctestは短いものだけ、複雑なものは unittest を書く

3-5 Sphinx
----------
- plantumlを入れるのを使ってた
- 1画像1プロセス

  - Javaなので起動が遅い
  - 手元でbuildしないほうがいいのでは

- いろんなdirectiveがある

  - sphinx contribを見よう

- 仕事ではどんなところで使っているか?

  - 最初にプロジェクトの要求リストとかをSphinxで書いている
  - コードの中にSphinxをコピーして実装している
  - 途中からなし崩し的にうまくいかなくなる
  - ドキュメントとコードの同一性を保つのがつらい
  - ドキュメントはしっかり書きたい

- doxygen で sourcecode -> xml -> sphinx とかやっている

  - dqn ってツールを昔作っていた

3-6 PyCharm
-----------
- デバッグツールはもうちょっと
- .idea: ウィンドウを開いた、開かないとかの情報も入っている
- `PyCon APAC/Taiwan 2015 Python Debugger Uncovered - Dmitry Trofimov <https://tw.pycon.org/2015apac/en/program/39>`_
- buildoutという環境構築ツールが有る

  - PyCharm上で実行するときにハマった

- 実務上はCLIと言っているが、PyCharmはどこで使っている?

  - 新しく入ってきた人にはPyCharmの設定とか、デバッグの使い方とか
  - チームで開発するときにみんなでやるのは PyCharm がよさそう
  - 一人の中で使い分けることはあんまりない?→ないです
  - PyCharm で作った環境は CLI でも使える?

- こんなん作りました的なのないですか

  - battle hack に参加した
  - スマホアプリ作った
  - サーバーはPython, Tornadoで
  - 最初は bluemix だったがあとで heroku にした
  - Heroku賞もらった

ビアバッシュ(懇親会)
====================
- 阿久津さんのLT
  - 業務のためのPython勉強会
  - Pythonスタートブックの辻さんと知り合いでできたよ
  - 20人くらいの場所がいっぱいになった
  - `業務のためのPython勉強会 - connpass <http://startpython.connpass.com/event/14076/>`_
  - `S01 t2 akutsu_my_pythonhistory <http://www.slideshare.net/TakeshiAkutsu/s01-t2-akutsumypythonhistory>`_
  - MIT Open Course Ware: 6.00.1x、6.0..2x、6/10からはじまったばっかりなので
  - $50で修了証のPDFがもらえる
  - 次回は7月2日、3回目は8月開催予定
  - すごい人気がある

- iktakahiroのLT

  - チャットツールはなにを使っているか
  - Slack, HipChat
  - `slackpy 1.1.2 : Python Package Index <https://pypi.python.org/pypi/slackpy/1.1.2>`_
  - loggingのhandlerにするのいいと思う

まとめ
======

`「Pythonエンジニア養成読本」読書会 03 <http://pymook.connpass.com/event/16291/>`_

