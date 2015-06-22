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
   <script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

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

Pythonをさらに強力にするサードパーティ製パッケージ
--------------------------------------------------
この節では標準ライブラリ以外に多数のサードパーティ製パッケージが提供されていることを紹介しています。
Pythonでは `PyPI: Python Package Index <https://pypi.python.org/pypi>`_ というサイトで提供されており、 **pip** コマンドでインストールして使用できます。

ここで「Windowsで書いてある通りにpipをインストールができなかった」という質問がありました。書籍上のコードではLinuxを想定しているので **sudo** でrootユーザーになってpipをインストールしています。
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
第3章の著者の嶋田 健志(`@TakesxiSximada <https://twitter.com/TakesxiSximada>`_)にバトンタッチして、後半の読書会をはじめました。

3-1 開発環境とチーム開発に求められること
----------------------------------------
この節ではこのあとに解説するそれぞれの項目について概要的に触れています。
チーム開発として必要な以下の要素について簡単に解説がありました。

- バージョン管理システム: チームで開発を行うためには、それぞれの担当箇所の開発を平行して行うために、バージョン管理システムが必要です。
- 隔離された実行環境: さまざまなプロジェクトの開発を行う場合に、プロジェクトごとに使用するライブラリのバージョンが異なる場合があります。環境を混在させないために隔離された実行環境が必要です。
- ソフトウェア品質の担保: 作成したソフトウェアはきちんとが仕様どおりに動作するか確認するためにテストが必要です。
- ドキュメント: 仕様書や手順書などをチーム内で共有するために、あまり手間を掛けずにドキュメントを作成する必要があります。
- 統合開発環境: これからPythonで開発を行うのであれば統合開発環境を使用して、テストやデバッグを効率的に行う必要があります。

3-2 GitとGitHub
---------------
この節ではバージョン管理リステムとしてGitの紹介と、ホスティングサービスの
`GitHub <https://github.com/>`_ について解説しました。

最初にGit、GitHubを使っているかどうか参加者に聞いていましたが、使ったことがない人がそこそ人数がいたので、少し丁寧に解説をしました。

バージョン管理については馴染みの話題ということもあり、たくさんの質問が出ました。

- Q: ブランチはどの単位で作成しているか?
- A: 機能単位で作成している。redmine, github issueの単位で。
  今のプロジェクトでは「fix_shimada_チケット番号」というようなブランチ名にしていて、ブランチは人に紐付いている。担当者が変わった場合はブランチを作成し直す。
- Q: 普段はコマンドラインとGUIツールのどちらを使っているのか?
- A: コマンドラインを使っている。GUIツールの sourcetree は手になじまなかった。(筆者はGitを使いこなせていないのでSrouceTreeを使っています)
- Q: コンフリクトをしたときにはコマンドラインだと大変じゃないか?
- A: ガッツで乗り切っている(笑)
- Q: Gitをデザイナーさんにどうやって使ってもらうか。今はメールとかでもらったものを代わりにcommitしている
- A: 答えはない...

.. note::

   筆者から参考資料として、知り合いのデザイナーさんのGit関連の資料を共有しました

   - http://blog.uni-q.net/entry/2014/08/06/194117
   - `C86：新刊「イメージできるGit」の告知 - Uni-Q blog <http://blog.uni-q.net/entry/2014/08/06/194117>`_

GitHubに関する質疑応答は以下のとおりです。

- Q: 仕事でGitHubを使っているか?
- A: 使っている。ただし、この書籍はmercurial(別のバージョン管理ツール)とbitbucket(別のホスティングサービス)を使用して執筆した
- Q: GitHubに企業で開発しているコードを乗せると他の人から見られるのでは?
- A: 無料プランは公開リポジトリしか作れないが、お金を払うとプライベートリポジトリが作成できる。
  仕事ではプライベートリポジトリを使用している。
  個人でプライベートリポジトリが必要であれば、無料で作成できるbitbucketがおすすめ

3-3 virtualenv
--------------
この節ではプロジェクトごとにPythonの環境を独立させるためのvirtualenvについて解説しました。以下のコードはvirtualenvをインストールして利用している手順です。

env環境でのみrequestsが利用可能になっていることが確認できます。

.. code-block:: sh
   :caption: virtualenvのインストールと利用

   $ pip install virtualenv    # pipコマンドでインストール
   $ virtualenv env            # envという名前で環境を作成
   New python executable in env/bin/python
   Installing setuptools, pip...done.
   $ . env/bin/activate        # env環境を有効にする
   (env)$ pip install requests # requestsをインストール
   (env)$ python
   >>> import requests         # requestsをインポートできる
   >>> quit()
   (env)$ deactivate           # env環境を無効にする
   $ python
   >>> import requests         # requestsのインポートに失敗する
   Traceback (most recent call last):
   File "<stdin>", line 1, in <module>
   ImportError: No module named requests

virtualenvを使うことにより、プロジェクトごとに同じパッケージでも異なるバージョンを使用したりといったことが可能になります。
また、vritualenvwrapperのようにvirtualenvをより便利に使うためのツールも提供されているので好みで使ってみてくださいという話がありました。

virtualenv環境をどのように作成してどのフォルダに配置するかというのは、人それぞれなので、正解はないという解説もありました。

質疑応答では「Windowsでファイルの関連付けは変わらないのか?」という質問があり「おそらくファイルのダブルクリックやOS経由でPythonを呼び出すときには、virtualenv環境の外になるため元々のPythonが呼び出されるのではないか」という回答がされました。

他に「本番環境にリリースするときにはどうしているのか」という質問があり、
「opsworksを使用して、デプロイするスクリプトの中でvirtualenv環境を作成している」という回答がありました。

プロジェクトで沢山のサードパーティ製パッケージを使用している場合、本番環境にインストールするのが大変ではないか?という質問がありました。
pipコマンドにはpip freezeという現在インストールしているパッケージの一覧を出力するコマンドがあり、このコマンドを使用することによって、同じ環境が簡単に作成できるという解説がありました。pip freezeを使用した例は以下のようになります。

.. code-block:: python
   :caption: pip freezeの利用例

   (env1)$ pip freeze > requirements.txt    # パッケージ一覧をファイル出力
   (env1)$ cat requirements.txt             # パッケージ一覧を確認
   alabaster==0.7.4
   Babel==1.3
   docutils==0.12
   Jinja2==2.7.3
   MarkupSafe==0.23
   Pygments==2.0.2
   pytz==2015.4
   six==1.9.0
   snowballstemmer==1.2.0
   Sphinx==1.3.1
   sphinx-rtd-theme==0.1.8
   (env1)$ deactivate
   $ virtualenv env2                        # 新規に環境(env2)を作成
   $ . env2/bin/acitvate
   (env2)$ pip freeze                       # パッケージが存在しない
   (env2)$ pip install -r requirements.txt  # ファイルを使用してインストール
   # ここで各パッケージがインストールされる

3-4 テストと品質
----------------
この節ではPythonでのテストについての解説を行いました。
テストは大事ですが手で実行すると大変なので、ユニットテストコードを書きましょうという話です。

最初にPythonには `doctest <http://docs.python.jp/2/library/doctest.html>`_ というコメント(docstring)にテストを書く方法があります。
次のコード例のように書くと、docstringがそのままサンプルコードになり、ユニットテストのコードにもなるため非常に便利です。

.. code-block:: python
   :caption: doctestのサンプル

   # -*- coding: utf-8 -*-
   def get_ok():
   """
   文字列 'OK' を返す
   >>> get_ok()
   'OK'
   """
   
   return 'OK'

doctestは以下のように実行します。上記のコードを ``doctest_sample.py`` というファイルに保存します。
なお、エラーが発生しない場合は何も出力されません。

.. code-block:: sh
   :caption: doctestを実行

   $ python -m doctest doctest_sample.py
   $


doctestで複雑な単体テストコードを書こうとすると、コメントが長くなりすぎてわかりにくくなります。
複雑な単体テストを行いたい場合は `unittest <http://docs.python.jp/2/library/unittest.html>`_ を使用して、ユニットテストコードを書きましょうという説明がありました。

3-5 Sphinx
----------
`Sphinx <htttp://sphinx-users.jp/>`_ はreStructedTextという形式で作成したドキュメントを、HTML、PDF等に変換できるツールです。
さきほど紹介したPythonのドキュメントもSphinxで作成されています。

しまださんは `sphinxcontrib-plantuml <https://pypi.python.org/pypi/sphinxcontrib-plantuml>`_ を使用してURLの図を作成しているそうです。
しかし、複数の図があると1画像ごとにJavaのプロセスが起動するため、時間がかかるそうです。

Sphinxにはこのように拡張機能(directive)でさまざまな機能を拡張できます。
`sphinx-contrib <https://bitbucket.org/birkenfeld/sphinx-contrib/>`_ に拡張機能がまとめてあるので参照してみてください。

「仕事でSphinxはどんなところで使っているか?」という質問がありました。
最初にプロジェクトの要求リストをSphinxで書いて、コードの中にそのリストをコピーして実装を薦めたりしていたそうです。
ただ、途中からなし崩し的にうまくいかなくなり、ドキュメントとコードの同一性を保つのが難しいという話がありました。

また、以前 `Doxygen <http://www.stack.nl/~dimitri/doxygen/>`_ でコードを解析した結果のXMLを元にSphinxドキュメントを生成する
`dqn <https://pypi.python.org/pypi/dqn>`_
というツールを作っていたそうです。

3-6 PyCharm
-----------
この節では `PyCharm <https://www.jetbrains.com/pycharm/>`_ というPython用のIDE(統合開発環境)について解説しました。

PyCharmのデバッグツールはもうちょっとというコメントがありました。
PyCon APAC 2015ではPyCharmを作っているjetBrainsの人が
`Python Debugger Uncovered <https://tw.pycon.org/2015apac/en/program/39>`_
という発表をしていました。

また、 `buildout <http://www.buildout.org/en/latest/>`_ という環境構築ツールがありますが、これとPyCharmを組み合わせるてハマったことがあるそうです。

質疑応答では「実務上はCLIを使っているそうだが、PyCharmはどこで使っているのか」という質問がありました。
回答としては、新しく入ってきた人にはPyCharmの設定とかやデバッグの使い方を伝えている。チームで開発するときにはPyCharmがよさそうとのことでした。

また「なにか実際に開発した例を教えてほしい」という質問があり、
`BattleHack Tokyo <https://2015.battlehack.org/tokyo?locale=ja>`_
というイベントでスマホアプリのサーバー側を
`Tornado Web Server <http://www.tornadoweb.org/en/stable/>`_
で作成したそうです。
Heroku 上でサーバーを動かし、Heroku賞をもらったそうです。すごいですね。
作成したコードは以下に置いてあるそうです。

- https://github.com/TakesxiSximada/bluemix_tornado_example
- https://github.com/TakesxiSximada/batoran

ビアバッシュ(懇親会)
====================
読書会の終了後はビールとピザでビアバッシュという形式の懇親会を行いました。
今回、実は私がネットでピザを注文したつもりが注文が完了しておらず、ギリギリのタイミングで再注文するというトラブルがありました。ピザが間に合ってよかったです。

ひと通りピザを食べ終わったらライトニングトーク(LT)大会になりました。今回は私を含めて3名が発表しました。

LT1 - 業務のためのPython勉強会
------------------------------
阿久津(`@akucchan_world <https://twitter.com/akucchan_world>`_)さんからは自身が主催している
`業務のためのPython勉強会 <http://startpython.connpass.com/event/14076/>`_
について紹介がありました。

この勉強会は阿久津さんが `Pythonスタートブック <http://gihyo.jp/book/2010/978-4-7741-4229-6>`_ の著者の辻さんと知り合って立ち上げたもので、第1回は20名くらいの会場がいっぱいになったそうです。

第1回の勉強会の中で阿久津さんが発表した「私のPython独学奮闘記」をダイジェストで話してもらいました。以下の3種類のアプローチで学習を進めているという話でした。

- Text: 「Pythonスタートブック」等の書籍での学習
- Web: `MIT OpenCourseWare <http://ocw.mit.edu/index.htm>`_ での学習
- Real: 勉強会への参加、企画

.. raw:: html

   <iframe src="//www.slideshare.net/slideshow/embed_code/key/BiuW7thGxQ5tlc" width="425" height="355" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="//www.slideshare.net/TakeshiAkutsu/s01-t2-akutsumypythonhistory" title="S01 t2 akutsu_my_pythonhistory" target="_blank">S01 t2 akutsu_my_pythonhistory</a> </strong> from <strong><a href="//www.slideshare.net/TakeshiAkutsu" target="_blank">Takeshi Akutsu</a></strong> </div>

初心者としてどのように勉強していったかなかなか興味深い発表でした。ぜひ、PyCon JPにもプロポーザルを出してほしいなと個人的に思いました。

`第2回 <http://startpython.connpass.com/event/16104/>`_ は7月2日開催予定ですが、すでにキャンセル待ちで人気の勉強会のようです。第3回は8月開催予定とのことです。

LT2 - slackpy
-------------
著者の一人の池内さん(`@iktakahiro <https://twitter.com/iktakahiro>`_)からは最初に業務で使っているチャットはなにか?という質問がありました。
参加者からはSlack、HipChat、ChatWorkなどのツールの名前があがっていました。

池内さんが作成している `slackpy <https://pypi.python.org/pypi/slackpy/>`_ というパッケージで、Slackに対して簡単にログメッセージを表示できることを紹介していました。

ログレベルを指定するとSlack上で色分けして表示されるため見た目にもわかりやすいです。

発表の後で「Pythonのloggingのhandlerにしてほしい」という提案がありました。
次のバージョンアップに期待です。

LT3 - Pythonエンジニア養成読本オモテウラ
----------------------------------------
最後は筆者のLTです。最初にPython関連イベント2つの告知をしました。どちらも参加者募集中、発表内容を募集中です。

- `PyCon mini Sapporo 2015 <http://sapporo.pycon.jp/2015/>`_
- `PyCon JP 2015 <https://pycon.jp/2015/>`_

LTではどのようにこの本が作られていったのかという話をしました。
Googleスプレッドシートにレビューの指摘を書いてもらい、その対応状況をGoogle Apps ScriptでSlackチャットに投げたりといった工夫について紹介しました。

.. raw:: html

   <iframe src="//www.slideshare.net/slideshow/embed_code/key/aYYteVVOVe7N7O" width="425" height="355" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="//www.slideshare.net/takanory/two-sidesofpythonengineertrainingbookplonesymposiumtokyo" title="Two sides of &quot;Python Engineer Training Book&quot;" target="_blank">Two sides of &quot;Python Engineer Training Book&quot;</a> </strong> from <strong><a href="//www.slideshare.net/takanory" target="_blank">Takanori Suzuki</a></strong> </div>

まとめ
======
2回目の読書会はビアバッシュでのライトニングトークも盛り上がりました。
次回は7月23日(木)に開催します。内容は「第4章 PyData入門」です。
本を読んで試して疑問がある方、もっとここが知りたい!!という所がある方など、ぜひ参加してください。参加申し込みは下記のURLからできます。

- `「Pythonエンジニア養成読本」読書会 03 <http://pymook.connpass.com/event/16291/>`_

では、また来月もお会いしましょう。
