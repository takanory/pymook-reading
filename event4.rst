===================================
 第4回 入門Webアプリケーション開発
===================================

.. contents:: 目次
   :local:

はじめに
========
鈴木たかのりです。

`前回 <http://gihyo.jp/news/report/01/python-training-book-reading-club/0003>`_
に引き続き
`Pythonエンジニア養成読本 <http://gihyo.jp/book/2015/978-4-7741-7320-7>`_
という書籍の `読書会イベント <http://pymook.connpass.com/>`_ についてレポートします。

`第4回の読書会 <http://pymook.connpass.com/event/18062/>`_ は8月27日(木)に `アライドアーキテクツ株式会社 <http://www.aainc.co.jp/>`_ の会議室で開催されました。

当日はだいたい以下のタイムテーブルで進めました。

- 19:00-19:15 参加者の自己紹介
- 19:15-21:00 「第5章 入門Webアプリケーション開発」
- 21:00-22:00 ビアバッシュ(ビールとピザでの参加者懇親会)

今回も過去3回と同様に書籍の読みあわせはせず、ページ数の関係で削ったところや、出版後の追加情報を中心に解説を行いました。

自己紹介
========
いつものように最初に参加者全員で自己紹介を行いました。今回は17名の方が参加しました。

自己紹介の中では「4回参加」「3回参加」など結構いつもみる顔の方ができたのがいいですね。
逆に初参加の方も2名いて、そのうち1名は一週間前に筆者が発表したPython入門を聞いて、その直後に読書会に参加してくれたそうです。ありがたいです。

- 参考: `【 ヒカ☆ラボ 】Pythonに興味がある方必見！PyCon JP 2015座長が語る、「Python言語」はじめの一歩！  <https://atnd.org/events/68337>`_

また、今回は「第5章 入門Webアプリケーション開発」が題材ですが、普段Web開発を行っていない方がほとんどで、Web開発を行っている方はPHPやJavaなどを使っているとのことでした。

第5章 入門Webアプリケーション開発
=================================
自己紹介の後に5章の著者の関根 裕紀(`@checkpoint <https://twitter.com/checkpoint>`_)から自己紹介がありました。

業務ではPythonはメインではあまり使っておらず、趣味や業務の一部で使用しているとのこと。
また、最近は新卒メンバー、若手メンバーの教育支援も行っているそうです。

Pythonとの関わりは `PyCon JP <http://pycon.jp/>`_ のスタッフ、Pythonエンジニア養成読本の執筆の他に、スピーカーとしてPyCon JPなどのイベントでPython関連の発表を行っているとのこと。

また、 `Pythonもくもく会 <http://mokupy.connpass.com/>`_ というハッカソンイベントを毎月開催しているそうです。

5-1 Webアプリケーションフレームワーク入門
-----------------------------------------
この節ではPythonのWebフレームワークについて解説しています。

Webアプリケーションを作成する場合は通常は自分で一から作成はせずに、Webフレームワークというものを使って作成します。
フレームワークとは枠組みのことで、Webフレームワークを使うことによって、その枠組にそってWebアプリケーションを作ることができます。

この節では代表的なPythonのWebフレームワークについて紹介しています。

- `Django <https://www.djangoproject.com/>`_
  
  Djangoは全部入りのフレームワークです。10年位の開発の歴史があり、現在も活発です。
  保守的で後方互換性を重要視しています。また、大規模な事例が多いとのことです。

  Ruby on Railsと全部入りという意味では近いかも知れないですが、設計思想は違うそうです。
  
- `Pyramid <http://docs.pylonsproject.org/projects/pyramid/>`_

  Pyramid はマイクロフレームワークで好みのサードパーティー製のモジュールを組み合わせて使用します。

- `Tornado <http://www.tornadoweb.org/>`_

  TornadoはFacebookが開発しているフレームワークで開発が活発です。
  非同期で大量のデータをさばくときによく使われています。

- `Flask <http://flask.pocoo.org/>`_

  Flaskはこの書籍で紹介しているBottleと似ていて、軽量で簡単に使用できるフレームワークです。
  Djangoなどは設定ファイルなど使いはじめるために覚えることが膨大ですが、FlaskやBottleは数行書くだけでとりあえず動作させることができます。

ここで参加者に対して「PythonのどんなWebフレームワークを使っているか」という質問がありました。回答としてはFlaskを使っている人やDjango、Pyramid、Tornadoを用途によって使い分けているという人がいました。
DjangoにはDjango Adminというデータを管理するための画面が自動生成できる機能があります。この機能を使いたいためにDjangoを選択することもあるそうです。

スピーカーがWebアプリケーションを構築する際におすすめするのはDjangoとのことです。
理由としてはドキュメントがちゃんとしていることと、検索すると色々と情報がひっかかるからとのことです。
Webアプリケーションのプロトタイプを作成する場合はBottleがおすすめだそうです。

Bottle
~~~~~~
ここで、この書籍で使用しているWebフレームワーク `Bottle <http://bottlepy.org/>`_ についての説明になりました。
BottleはWebフレームワークとして以下の4つの機能を提供しています。また、これらの機能はだいたいのWebフレームワークで提供されています。

- ルーティング: 指定されたURLと処理するコードを対応付ける仕組み
- テンプレートエンジン: HTMLを返却するときにテンプレートに変数などを入れる仕組み
- HTTPユーティリティ: HTTPリクエストやレスポンスを扱うためのクラスや関数
- サーバー: 開発用のWebサーバー

また、Bottleの特徴として1つのファイルでフレームワークが実装されているため、フレームワークをどのように作るのかという勉強にも向いているとのことです。
Bottleのソースコードリーディングをそのうち実施予定とのことです。

ここで、ルーティングで使用しているデコレータについて「デコレータとはどういうものなのか?」という質問がありました。

Bottleでは以下のように ``route`` デコレータを使用して「 ``/hello`` にアクセスきたら ``hello()`` メソッドを実行する」という指定を行います(これをルーティングといいます)。

.. code-block:: python
   :caption: ルーティングの指定

   @route('/hello')
   def hello():
       # テンプレートの描画
       return template('Hello {{string}}', string='World')

デコレータはある関数をラップする関数です。デコレータを指定することによってある関数に機能を追加したりできます。

なお、デコレータはシンタックスシュガー(`糖衣構文 <https://ja.wikipedia.org/wiki/%E7%B3%96%E8%A1%A3%E6%A7%8B%E6%96%87>`_)であり、以下の2つのコードはどちらも同じ動作をします。
Webフレームワークだと他に「このURLはログイン必須」というデコレータでログインチェックを行ったりできるものがあります。

.. code-block:: python
   :caption: デコレータの例

   def spam(...):
       ...
   spam = ham(spam)

   @ham
   def spam(...):
       ...

Bottleにはテンプレートエンジンも付属しています。
プログラムからHTMLを返すときには、文字列を連結する必要がありますが、テンプレートエンジンを使用することにより、HTMLテンプレートの中に値を埋め込むことができます。
例えば以下のテンプレートは ``basket`` の内容を一つずつ取り出し、リストで出力しています。

.. code-block:: python
   :caption: Bottleのテンプレート

   <ul>
     % for item in basket:
       <li>{{item}}</li>
     % end
   </ul>

PythonのWebフレームワークのテンプレートエンジンは他には
`Jinja2 <http://jinja.pocoo.org/docs/dev/>`_ 、 `Mako <http://www.makotemplates.org/>`_ 、 `Djangoテンプレート <https://docs.djangoproject.com/en/1.8/topics/templates/>`_ などがあります。
Bottleのテンプレートは最低限の機能に対応しています。

Bottleのテンプレートエンジンには継承機能があります。継承はヘッダー、フッターの共通化などに利用できます。

ここで「テンプレートの ``rebase()`` について使い方がわかりにくかった」という質問がありました。
``include()`` はテンプレートの中に他のテンプレートを読み込む機能で、 ``rebase()`` は逆にベースとなる親テンプレートの指定した個所に、子の内容が展開されるというところが違うという説明がありました。

他に質問で「Webサーバーはどうするのか?」という質問がありました。
PHPも最近はテスト用のWebサーバーを内蔵しているが、Bottle付属のWebサーバーもテスト用のもので、実際にWebサービスとして公開する場合には使用しません。
PythonのWebフレームワークは `WSGI: Web Server Gateway interface <https://www.python.org/dev/peps/pep-0333/>`_ に則っているので、WSGIに対応したアプリケーションサーバーを使用します。
よく使われるのは `uWSGI <https://uwsgi-docs.readthedocs.org/>`_ や `Gunicorn <http://gunicorn.org/>`_ です。
Tornadoは付属しているアプリケーションサーバーを使用します。

.. 他に「Webサービスを作るためにBottleは初心者にとっつきやすいと思ったが、HTMLを覚えないといけないのが大変。tplファイルもほとんどHTMLファイルだがこれはどうにもならないのか」という質問がありました。
   この質問に対して、以下の様な回答があがっていました。

   - HTMLとCSSは必要。他にJavascriptも多少は必要となってくる
   - Webを知らない人を対象にしてしまうと、そもそもWebはどうなっているか、HTMLとかの説明も必要になってしまう。HTMLはどうしても必要。
   - A: CSSとJSはBootstrapとかを使って楽をする。HTMLは勉強する必要はあり。

5-2 データベース開発入門
------------------------
この節ではWebアプリケーションとは切っても切れないデータベースについて解説しています。

Python では `PEP 249 <https://www.python.org/dev/peps/pep-0249/>`_ でデータベースとのAPI仕様が定義されています。そのため、さまざまなデータベース(MySQL、PostreSQL、Oracleなど)と接続するためのアダプターが存在します。

アダプターでデータベースに接続して直接SQLを実行することも可能ですが、データベースに特化したO/Rマッパーを使用するのが一般的です。

ここでは `SQLAlchemy <http://www.sqlalchemy.org/>`_ を使用しています。
他には `SQLObject <http://sqlobject.org/>`_ やDjango付属のO/Rマッパーなどがあります。

ここで「書籍ではバージョンは0.9.9だが最新は1.0.8となっているが現状はどんな感じか」という質問がありました。
回答としては、出版時に1.0系がリリースされ現在はは1.0.8が最新。0.9系はこれからはメンテナンスモードのためこれからは1.0系を使うべきという回答がありました。
また、検証はしていないが、ここで出てくる例は 1.0 系でもそのまま使用できると思うとのことです。

.. - SQLAlchemyではデータベースにアクセスするときにSessionを使う

SQLAlchemyはO/Rマッパーなので、Pythonのオブジェクトを扱っている様にデータベース上の値を取得したり、変更ができます。

.. warning:: サンプルコードを入れる

かなり高機能なので、いろいろ使って見ながら覚えてほしいとのことです。また、私見だがSQLが好きな人にSQLAlchemyは好かれているという印象があるそうです。面白いですね。

WebフレームワークのPyramidを使う場合はSQLAlchemyを使用することが多いそうです。
また、データベースのマイグレーション(テーブルに列を追加したりすること)には `Alembic <http://alembic.readthedocs.org//>`_ を使用するのが一般的です。

SQLAlchemyはWebアプリケーションだけじゃなく単独でも使用できます。
バッチ処理などでも使用できるので、ぜひ使ってみてください。

5-3 ［サンプル］書籍管理アプリの作成
------------------------------------
この節ではここまで説明したBottle(Webフレームワーク)とSQLAlchemy(O/Rマッパー)を組み合わせて、簡単なWebアプリケーションを作成しています。
サンプルのWebアプリケーションでは書籍の登録、編集、削除と一覧表示ができるというCRUD(Create/Read/Update/Delete)ができる一般的なものです。

Pythonコードは160行程度でクラスは2つと非常にシンプルな作りです。テンプレートを含めても400行程度しかありません。
コード全体はgithubの下記のURLで公開しているので、必要な人はダウンロードして試すことが可能です。

- https://github.com/checkpoint/pymook_web_application

このコードを動作させるには、下記のコマンドでパッケージをインストールします。
`bottle-sqlalchemy <https://pypi.python.org/pypi/bottle-sqlalchemy/>`_ は名前のとおり Bottle で SQLAlchemy を使用するためのパッケージです。
`WTForms <https://wtforms.readthedocs.org/>`_ は **フォーム** という入力フォームを表示したり、入力された値をチェックする機能を提供するパッケージです。
WebフレームワークとしてDjangoを使用する場合は、これらの機能はすべて標準で付属しているので追加でパッケージを導入する必要はありません。

.. code-block:: sh
   :caption: パッケージのインストール

   $ pip install bottle==0.12.8
   $ pip install sqlalchemy==0.9.9
   $ pip install bottle-sqlalchemy==0.4.2
   $ pip install WTForms==2.0.2

.. - templateの中でfor文を使える

Webアプリケーションではこのように、サンプルとしてCRUDのアプリケーションを作成することはよくあります。
処理の流れとしてはどのようなWebフレームワークを使用しても同様で、例えば新規にデータを登録する場合は以下の様な流れになります。

1. モデルを作成する(どういうデータを管理するのかを定義する)
2. 入力フォームに入力された値を取り出す
3. モデルのインスタンスに、入力された値を設定する
4. 保存したら一覧画面に遷移する

しかし、Webアプリケーションを本格的に作成する場合は、他にも考えることが増えます。例えば以下の様な観点が必要となります。

- セッション管理(カート機能などの実現に必要)
- セキュリティ対策(XSS、CSRFなど)
  
.. - いろんな道具を組み合わせて使えるのがBottleのいい面

Bottleではセッション管理に `Beaker <https://pypi.python.org/pypi/bottle-beaker/>`_ を使うのが一般的です。
Bottleではこのように、いろんな道具を組み合わせて使えるところがいいところです。

.. - Beakerで言うセッションはWebアプリケーションでログインしてカートに入れるとかそういうセッション。SQLAlchemyでいうセッションとは別。
   - JavaだとHibernateとかがDBのセッションとかの情報を使うよね
     
.. Bottleのドキュメントにレシピとかでどれと組み合わせるべきかとか書いてあるよ

まとめとして、BottleはWebアプリケーションのプロトタイプを作成するときには、さくっと作れるので便利であるとい話がありました。
例として `Plone Symposium Tokyo 2015 <http://plone.jp/plone-symposium-tokyo-2015>`_ で解析結果を可視化するためのWebアプリケーションを、Bottleベースで半日くらいで作成したそうです。
このアプリケーションは `Airbnb <https://www.airbnb.jp/>`_ から東京と京都の物件の情報を取得し、価格帯をグラフ表示するというものです。
発表の様子は下記レポートからも参照できます。

- `第1回　Plone Symposium Tokyo 2015－Day 1：トークセッション編 <http://gihyo.jp/news/report/01/plone-symposium-2015/0001?page=4>`_

単純に参照するだけであればBottleは向いており、Webアプリケーション作成のとっかかりとしておすすめとのことです。
また、冒頭にも書きましたが、1ファイルで作成されているためフレームワークを作る方法についても勉強になるそうです。

質疑応答
--------
最後に全体を通して質疑応答をしました。

- Q: フォームでの `XSS <https://ja.wikipedia.org/wiki/%E3%82%AF%E3%83%AD%E3%82%B9%E3%82%B5%E3%82%A4%E3%83%88%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%97%E3%83%86%E3%82%A3%E3%83%B3%E3%82%B0>`_ 対策はどうするのか?
- A: Bottleはセキュリティ対策は自前で作成するか、サードパーティーのパッケージを使用する必要がある。Djangoは XSS, CSRF 等々ひととおりのセキュリティ対策の機能を持っている。
  しかし、シンプルなWebアプリケーションを作成するときにDjangoを使うのは面倒な場合もある
- Q: フォームライブラリはどれ使えばよいのか?
- A: DBはSQLAlchemyで決まりでよいが、フォームにどれ(ここではWTForms)を使用するかか決めるのは苦労した。ライブラリを探すときにはgithubを見たり、googleやslackoverflowを検索して参考にして決めてる。また、勉強会などに参加して詳しい人に聞くこともおすすめ。
- Q: Bottleでサーバーを起動するときの ``app.py`` というファイルのファイル名は決まっているのか?
- A: ファイル名はどんなものでもよい。コンソールから起動するので以下のように記述する必要がある。

  .. code-block:: python
     :caption: コンソールから起動するスクリプト

     if __name__ == `__main__:
         # ここに動作を書きます
         
- Q: プロトタイプ作成時は ``app.py`` などから実行でよいが、実環境ではどのように実行するのか。
- A: Bottleをプロダクションで使ったことがない。おそらく gunicorn などのWebアプリケーションサーバーを使用する。

ビアバッシュ(懇親会)
====================
読書会の終了後はビールとピザによるビアバッシュ(懇親会)です。
Pythonに関連したりしなかったりといった会話のあとに、ライトニングトーク大会を行いました。

トップバッターは
`‏@shigeshibu44 <https://twitter.com/shigeshibu44>`_ による「WebエンジニアとWebディレクターを兼任してわかった3つのこと」です。

.. raw:: html

   <iframe src="//www.slideshare.net/slideshow/embed_code/key/iRwP3GoLlC9Uu3" width="425" height="355" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="//www.slideshare.net/satoshimoriya5249/webweb3-title" 51451643="WebエンジニアとWebディレクターを兼任してわかった3つのこと" target="_blank">WebエンジニアとWebディレクターを兼任してわかった3つのこと</a> </strong> from <strong><a href="//www.slideshare.net/satoshimoriya5249" target="_blank">Satoshi Moriya</a></strong> </div>

「あるある」的な話で心が多少痛くなる発表でしたが、次回どうなったかの進捗に期待したいと思います。

二番目は、加藤 尊さんの「コンピュータ将棋について～機械学習を用いた局面学習への道～」です。

.. raw:: html

   <iframe src="//www.slideshare.net/slideshow/embed_code/key/bN35TrqUaMWVRq" width="425" height="355" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="//www.slideshare.net/TakashiKato2/ss-52335846" title="コンピュータ将棋について～機械学習を用いた局面学習への道～" target="_blank">コンピュータ将棋について～機械学習を用いた局面学習への道～</a> </strong> from <strong><a href="//www.slideshare.net/TakashiKato2" target="_blank">Takashi Kato</a></strong> </div>

この発表を会社(広告代理店)でしたところ「ポカーン」とされたそうです。まぁ、そうですよね。
内容としてはコンピュータ将棋ってどうやって考えているのかの入り口がわかって非常に興味深かったです。全文検索でよく使われる `n-gram <https://ja.wikipedia.org/wiki/%E5%85%A8%E6%96%87%E6%A4%9C%E7%B4%A2#N-Gram>`_ がここで出てくるのは、面白いアプローチだなと思いました。
 
ライトニングトーク3つ目は `@TakesxiSximada <https://twitter.com/TakesxiSximada>`_ による告知です。
一つはこの記事公開時にはすでに終了していますが、 `SoftLayer Bluemix Summit 2015 <http://softlayer.connpass.com/event/17037/>`_ です。このイベント「NASAをHack!Bluemix+Pythonを駆使した宇宙人探し奮闘記」というタイトルで発表を行ったようです。

もう一つは
`PyCon JP 2015のチュートリアル <https://pycon.jp/2015/ja/schedule/tutorials/list/>`_
で「 `【初心者向けPythonチュートリアル】Webスクレイピングに挑戦してみよう <https://pycon.jp/2015/ja/schedule/presentation/37/>`_ 」という講座を行うことが紹介されました。このチュートリアルは前半はPythonエンジニア養成読本の内容をベースに進めて、後半はWebスクレイピング(Webサイトの内容を解析してデータを抽出する)という実用的なものです。

チュートリアルは現在チケット発売中です(別途PyCon JPの参加チケットも必要です)。
下記のURLからチケット購入可能ですので、興味のある方はぜひ参加ください。

- `PyCon JP 2015 チュートリアル <http://pyconjp.connpass.com/event/18811/>`_
 
まとめ
======
4回目の読書会も質疑応答も活発で、ビアバッシュでも面白いライトニングトークがあり楽しい時間でした。

最終回となる次回読書会は9月17日(木)に開催します。内容は「第6章 環境構築の自動化」で `Ansible <http://www.ansible.com/>`_ について取り上げます。
本を読んで試して疑問がある方、もっとここが知りたい!!という所がある方など、ぜひ参加してください。参加申し込みは下記のURLからできます。

- `「Pythonエンジニア養成読本」読書会 05 <http://pymook.connpass.com/event/19107/>`_

ちなみに、最終回は著者6名全員が集合する予定です。サインをまとめてゲットするチャンスです!!では、次回もよろしくお願いします。

