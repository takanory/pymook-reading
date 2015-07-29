=========================================
 第3回 PyData入門 - Pythonでのデータ処理
=========================================

.. contents:: 目次
   :local:

はじめに
========
鈴木たかのりです。

`前回 <http://gihyo.jp/news/report/01/python-training-book-reading-club/0002>`_
に引き続き
`Pythonエンジニア養成読本 <http://gihyo.jp/book/2015/978-4-7741-7320-7>`_
という書籍の `読書会イベント <http://pymook.connpass.com/>`_ についてレポートします。

`第3回の読書会 <http://pymook.connpass.com/event/15198/>`_ は7月23日(木)に `アライドアーキテクツ株式会社 <http://www.aainc.co.jp/>`_ の会議室で開催されました。

当日はだいたい以下のタイムテーブルで進めました。

- 19:00-19:15 参加者の自己紹介
- 19:15-21:00 「第4章 PyData入門」
- 21:00-22:00 ビアバッシュ(ビールとピザでの参加者懇親会)

今回も過去2回とと同様に書籍の読みあわせはせず、ページ数の関係で削ったところや、出版後の追加情報を中心に解説を行いました。

自己紹介
========
いつものように参加者全員で自己紹介を行いました。全部で21名の方が参加してくださいました。

自己紹介の中では3回全て参加されている方から「集合知プログラミングのコードがだんだん読めるようになってきた。」といううれしい進捗報告がありました。
他にも「前回チーム開発でgithubが紹介されていたので、アカウントを作ってまずはドットファイル(設定ファイル)をアップしてみた。」という方もいました。
今回が初参加の方もおり、会場を借りているアライドアーキテクツの新人の方や、4月に転職してPythonをはじめた方などが参加していました。

現在までの3回をフル参加している方も数名いて、この読書会に参加することでなにか面白いことや得るものがあるのかなと思い、開催社としては非常にうれしいです。
    
第4章 PyData入門
================
自己紹介のあとは、早速本題のPyData入門の解説に入りました。
最初に著者の池内 孝啓(`@iktakahiro <https://twitter.com/iktakahiro>`_)から改めて自己紹介と今日の読書会でのポイントについて説明がありました。

自己紹介
--------
`ALBERT <http://www.albert2005.co.jp/>`_ という会社で働いており、データ分析をしているそうです。
データの前処理などの用途でPythonを使うようになったそうです。

また、コミュニティ活動としては `PyData.Tokyo <https://pydata.tokyo/>`_ のオーガナイザーをしているそうです。

昨年開催されたPythonのカンファレンス `PyCon JP 2014 <https://pycon.jp/2014/>`_ のチュートリアルで、PyData入門の講師としておこない、そこでいろんな出会いがありPyData.Tokyoをたちあげたそうです。
`PyCon JP 2015 <https://pycon.jp/2015/>`_ は10月に開催予定です。
つい先日トークの募集が締め切られ、機械学習、データ処理系のProposalが結構出ていたそうで、今年も楽しみにしているそうです。

(筆者注: ぜひ、 `トーク一覧 <https://pycon.jp/2015/ja/proposals/vote_list/>`_ を参照して面白そうなトークがあったらFacebook/Twitter等でシェアしてください。シェアされた数が投票数として採用/不採用の参考になります)


最後に、今日の読書会ではPandasを中心に話し、他には紙面の都合で触れられなかった話をしたいとのことでした。
また、出版後にPandasの新バージョン(0.16.2)がリリースされたので、アップデート情報についても触れるとのことです。

4-1 IPythonの使い方
-------------------
この節ではIPythonの基本的な使い方について解説しています。

IPythonはPythonの対話モードをより強力にしたものです。
IPythonでは以下の機能を備えています。

- 補完: Tabを入力してモジュール名やオブジェクト名を補完できます
- Magic Functions: ``%pwd`` と入力して現在のディレクトリ名を取得したり、  ``%env`` で環境変数を取得できます
- OSのコマンドライン環境との統合: ``!`` のあとにコマンドを入力するとOS上で実行してその結果を表示します
- オブジェクトの確認: オブジェクト名の後ろに ``?`` をつけるとオブジェクトの型、長さ等の情報を表示します
- Notebook: 後述するIPython Notebookの機能を提供します

書籍を校正しているときにIpythonのバージョン3.0がリリースされましたが、差分の反映が間に合わないためバージョン2.4を対象としました。
またインストール時に以下のようにしているのは、あとで出てくるIPython Notebookで使うためのモジュールもまとめてインストールするためです。

.. code-block:: sh
   :caption: pip で IPython をインストール

   $ pip install ipython[notebook]==2.4.0

IPythonのNotebook以外の機能を利用した例は以下の様な感じです。

.. code-block:: python
   :caption: IPython の利用例

   In [1]: import r # ←ここで Tab を入力
   random readline resource rfc822 rmagic runpy
   re repr rexec rlcompleter robotparser
   In [2]: %pwd
   Out[2]: u'/home/pydata/pydata'
   In [3]: !ls -l
   total 8
   drwxr-xr-x 25 pydata pydata 850 1月 1 10:00 bin/
   drwxr-xr-x 3 pydata pydata 102 1月 1 10:00 include/
   drwxr-xr-x 3 pydata pydata 102 1月 1 10:00 lib/
   -rw-r--r-- 1 pydata pydata 60 1月 1 10:00 pip-selfcheck
   In [4]: data = [1, 2, 3]

   In [5]: data?
   Type: list
   String form: [1, 2, 3]
   Length: 3
   Docstring:
   list() -> new empty list
   list(iterable) -> new list initialized from iterable's items

ここで「コマンドラインでIPython使っている人はいるのか?」という質問がありました。会場ではコマンドラインで使っている人はあまりおらず、IPythonは以下の2パターンで使用している人が多いようでした。

- IPython Notebookで使用している
- IDE経由でIPythonを使用している

4-2 PyData用パッケージの基本
----------------------------
この節ではPyDataというカテゴリで語られる、Pythonでデータ解析を行うためのパッケージについて紹介しています。

著者の池内さんの会社ではデータ解析には `R言語 <https://ja.wikipedia.org/wiki/R%E8%A8%80%E8%AA%9E>`_ を使っている人が多いそうです。
データの加工、集積にはSQLを使っている人が多く、Pythonのユーザーは最近増えてきているそうです。

R言語を使用している理由としては、論文で出てきたアルゴリズムの実装やライブラリがR言語で公開されるのが早く、R言語そのものの情報も多いのだそうです。

そこでなぜPythonなのかというと、Pythonは汎用のプログラミング言語なので、一つ覚えればなんでもできるところが魅力だと語っていました。
PyData関連のパッケージを使用すればデータ解析もできるし、Webアプリを作ったりも当然できます。
データ解析した結果をWebで表示するデモアプリを作ったり、といったことも一つの言語で完結しているのが魅力だと語っていました。

また、Pythonはプログラミング言語として書きやすいし読みやすいことも魅力であると言っていました。

書籍の中では最近はやっている深層学習(ディープラーニング)について
`Pylearn2 <http://deeplearning.net/software/pylearn2/>`_ を紹介していましたが、
最近リリースされた `Chainer <http://chainer.org/>`_ が話題になっていると紹介されていました。
Chainer は Pylearn2 とは違い Python 的に書けるのがよいそうです。また、日本で開発されており、日本語のドキュメントが豊富なことも魅力です。

読書会では以下のPyData関連パッケージについて紹介しました。

NumPy
~~~~~
Python では大量のデータを for 文で処理すると時間がかかります。
しかし、 `NumPy <http://www.numpy.org/>`_ を上手に使うと、行列計算などを高速に処理ができます。

NumPyの行列データは `PyCharm <https://www.jetbrains.com/pycharm/>`_ (Python用のIDE)で可視化でき、見やすいです。
PyCharmは最近PyData系のサポートが厚くなっているそうです。

余談ですが画像処理の `OpenCV <http://opencv.org/>`_ にはNumPyが必要です。
これは、画像データを高速に処理するために、NumPyの行列データを利用しているためです。

SciPy
~~~~~
マーケティング領域のデータ分析では、対象がどの程度似ているかどうかを距離計算によって測ることがよくあります。
距離計算は、「ユーザーがどの程度似ている」「アンケート結果がどの程度似ている」といったものを表します。
距離の計算方法にはいろいろな種類がありますが、 `ユークリッド距離 <https://ja.wikipedia.org/wiki/%E3%83%A6%E3%83%BC%E3%82%AF%E3%83%AA%E3%83%83%E3%83%89%E8%B7%9D%E9%9B%A2>`_ が有名です。距離計算は `SciPy <http://www.scipy.org/>`_ を使用すると簡単にできるそうです。

SciPyは距離計算以外にも非常に沢山の機能を提供しています。

SymPy
~~~~~
`SymPy <http://www.sympy.org/en/index.html>`_ は Python で記号計算を行うためのパッケージです。
ここは趣味で紹介したそうです。実例はとくに思いつかないので、教えてほしいとのことでした(笑)。

もし中学生のお子さんがいたら、数学の教科書に書いてある式を入力すると SymPy が因数分解や微積分を解いてくれるので試してみてください。

Pandas
~~~~~~
`pandas <http://pandas.pydata.org/>`_ はデータ解析を行うためのパッケージです。
CSV、Excelなどのデータを読み込んで **DataFrame** という行列のデータを生成します。行と列にそれぞれ名前が付いていることが特徴です。
R言語にもデータフレームがあり、pandasを作った人もR言語を意識しているのではないかとのことでした。

R言語をすでに使っている人は、pandas使ってみるとよいかもとのことです。

質疑応答
~~~~~~~~
質疑応答では以下の様な議論がありました。

- Q: pandasの DataFrame をSelializeしてサーバークライアント間(どちらもpython)で通信している。パフォーマンスが出るのはなにか?
- A: 両方Pythonだったらpickleでいいのでは? `to_msgpack() <http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.to_msgpack.html>`_ があるので、パフォーマンスがよさそう
- Q: pandas を Version 0.16 にしたら warning  が出るようになった
- A: 警告表示を抑制するオプションを使うでとりあえずは大丈夫だと思う
- Q: 以前 Python 2 と pandasで書いたスクリプトを Python 3 で使いたい。気をつけるところはあるか?
- A: pandas としては問題ない。日本語周りは気をつけた方がいい。
- Q: Python で for 文を使ってはいけないのか。map とかはなかなか難しい。
- A: 大量のデータを扱う場合は for 文だと遅いのでNumPyをつかった計算ができないか検討しましょう。通常のfor文よりも内包表記のほうが僅かに速いです。またPythonの組み込み関数 `map <http://docs.python.jp/2/library/functions.html#map>`_ 、 `filter <http://docs.python.jp/2/library/functions.html#filter>`_ は勉強しましょう。

余談としてデータ分析の高速化についての PyData.Tokyo でのレポートが紹介されていました。
  
- `どこまで速くできる？ 達人に学ぶPython超高速データ分析～PyData.Tokyo Meetup #4イベントレポート <http://codezine.jp/article/detail/8687>`_

4-3 はじめてのIPython Notebook
------------------------------
IPython NotebookはWebブラウザから対話的にPythonプログラミングなどを行う環境です。
IPython の最新バージョンは 3.2.1 となっており、書籍で紹介していた 2.4 と大きく変わったところは、ロゴと名前が `Jupyter <https://jupyter.org/>`_ になったことです。
Jupyter は Python だけでなく Julia、R言語などさまざまな言語に対応しています。

最近ではIPython Notebookを使用してプレゼンを行う人もおり、この日も追加資料として以下の Notebook を利用して解説が行われました。
なお、下記のリンクをクリックすると IPython Notebook の中身が表示されますが、これは GitHub が Notebook ファイルの表示に対応するようになったためです(`GitHub + Jupyter Notebooks = <3 <https://github.com/blog/1995-github-jupyter-notebooks-3>`_)。

- `pymook_reading_20150723.ipynb <https://github.com/iktakahiro/ipython-notebook-sample/blob/master/pymook/pymook_reading_20150723.ipynb>`_


上記のNotebookを使用して、2つのデータを結合する例を解説しました。
for文をまわしてif文で分岐なども可能ですが、Pandasを利用すると ``merge()`` メソッドでSQLのような感じで2つのデータを結合できます。

また、Pandas 0.16.2で ``pipe()`` メソッドが追加になりました。
データフレームに対して ``.pipe(f)`` で処理を行うフィルターのようなもの関数を指定できます。また ``pipe()`` は複数重ねることも可能なため、サンプルコードでは食料品のデータに対して割引処理と消費税計算を行っています。

IPython Notebookでは棒グラフなどのグラフ描画ができますが、見た目的にはデフォルト形式よりもggplot形式がおすすめとのことです。他にも以下のようなグラフ描画用のライブラリが紹介されていました。ただし、プレゼン資料でなければグラフの見た目について頑張る必要はないとい話もしていました。

- `Seaborn <http://stanford.edu/~mwaskom/software/seaborn/>`_
- `Bokeh <http://bokeh.pydata.org/en/latest/>`_

他の人が作成した Notebook ファイルが閲覧できる `nbviewer <http://nbviewer.ipython.org/>`_ というサイトがあります。このサイトはグラフ描画などの参考になります。

IPython Notebookを使用するには普通に ``pip install ipython[notebook]`` でもよいのですが、 `Wakari.io <https://wakari.io/>`_ というサイトではクラウド上で IPython Notebook が使用できるのでお試しで使うには便利です。
また、 `Anaconda <https://store.continuum.io/cshop/anaconda/>`_ というデータ分析用のパッケージのセットがありますが、この中にも IPython Notebook が含まれています。

`Rodeo <http://blog.yhathq.com/posts/introducing-rodeo.html>`_ という Web ブラウザ上で動作する Python の IDE があります。これは IPython Notebook と似ていますが、よりリッチな操作ができるそうです。
データフレームの値を見て、対話形式で絞り込みなどが行えるそうです。

まとめとして、 IPython Notebook はあまり長いコードを書くのには向いていないので、サンプルのような短めのコードと結果を参照するのに使用することをおすすめするとのことです。
もしかしたら Rodeo は長いコードを書く用途にも向いているかも知れないとのことでした。このあたりは実際に使ってみた人の感想を聞いてみたいところです。

4-4 ［実践編］オープンデータの利用と可視化
------------------------------------------
この節ではオープンデータを利用して IPython Notebook で可視化する例を紹介しています。
ここで裏話として書籍の中で利用するオープンデータを探すのが大変だったという話がありました。
データ取得が面倒だったり、データ形式が利用しにくいものが多いそうです。
その点、書籍で利用した横浜のデータは
`よこはまオープンデータカタログ（試行版） <http://www.city.yokohama.lg.jp/seisaku/seisaku/opendata/catalog.html>`_ でライセンス付きで公開されており、CSVファイルなどを直接ダウンロードできます。

ここで全体を通して以下のような質疑応答がありました。

- Q: 横浜のグラフを、地図データで可視化しようと思ったが挫折した。
  地図データの可視化は `basemap <http://matplotlib.org/basemap/>`_ がおすすめか?
- A: Pythonではないが、 `Tableau <http://www.tableau.com/ja-jp>`_ (BIツール)で地図上にマッピングとかをしているが、日本の地図はそこまで細かくない。
  日本だと県ごと白地図しかない。今だとJAXAの衛星データ(`全球高精度デジタル3D地図 (ALOS World 3D) <http://www.eorc.jaxa.jp/ALOS/aw3d/>`_)とかにマッピングすると面白そう。
- Q: IPython Notebookをサーバーに入れて、みんなが使えるようにできないか?
- A: 自分が以前やったのは、複数のサーバーをポートを分けて実行した。
- Q: Notebook 上でデモするときに、パラメーターをユーザーに入力させることは可能か?
- A: IPython Notebook でシークバーを表示して値を変更するといった使い方が可能
- Q: Windows で Anaconda を使っている。IPython Notebook の終了方法がわからない
- A: 基本的にはコマンドを ``Ctrl-C`` で終了させる
- Q: R言語やJavaScriptなど、言語間での連携はできないか?
- A: 連携する方法はないので、CSVなどのファイル渡しがよい

余談ですが、ALBERTのページに「統計学とデータ分析」について書いているので、これから勉強しようとする人は読むとよいという紹介がありました。

- `統計学とは <http://www.albert2005.co.jp/technology/data/statistics.html>`_
    
ビアバッシュ(懇親会)
====================
読書会の終了後は毎回恒例の懇親会(ビアバッシュ)です。
ビールとピザを片手に会話を楽しみ、その後ライトニングトークを行いました。

一つ目は前回に続いて阿久津(`@akucchan_world <https://twitter.com/akucchan_world>`_)さんから
`業務のためのPython勉強会#3 - connpass <http://startpython.connpass.com/event/17073/>`_ の紹介がありました。
次回は8月10日(月)に開催予定とのことです。

著者の一人である嶋田 健志(`@TakesxiSximada <https://twitter.com/TakesxiSximada>`_)さんからは自身が出した PyCon JP 2015 の Proposal について紹介がありました。
Twitter/Facebook 等でシェアをよろしくお願いしますとのことです。
なお、チュートリアルの方は「Pythonエンジニア養成読本」の内容がベースとなっています。

- `【初心者向けPythonチュートリアル】Webスクレイピングに挑戦してみよう <https://pycon.jp/2015/ja/proposals/vote/59/>`_
- `Python × Bluemix でやったHack-a-thonでの超短期間認識系アプリ開発事例 <https://pycon.jp/2015/ja/proposals/vote/118/>`_

同じく著者の一人の関根 裕紀(`@checkpoint <https://twitter.com/checkpoint>`_)さんからは2015年10月に開催される `PyCon JP 2015 <https://pycon.jp/2015/>`_ のお知らせや、現在 `トーク一覧 <https://pycon.jp/2015/ja/proposals/vote_list/>`_ が参照できるので、ぜひTwitter/Facebookで拡散してほしいという話がありました。

最後に私からも宣伝LTとしてPyCon JPのプロポーザルとPython入門について話すイベントについて告知させてもらいました。

- `投票: PyCon JP を支える技術 2015 <https://pycon.jp/2015/ja/proposals/vote/130/>`_
- `【 ヒカ☆ラボ 】Pythonに興味がある方必見！PyCon JP 2015座長が語る、「Python言語」はじめの一歩！ <http://www.zusaar.com/event/8057003>`_

まとめ
======
3回目の読書会もビアバッシュでのゆるめのライトニングトークが盛り上がったのでよかったです。ぜひ他の参加者のみなさんも発表の練習だと思ってなにかしゃべってもらえればと思います。

次回読書会は8月XX日(XX)に開催します。内容は「第5章 入門Webアプリケーション開発」です。
本を読んで試して疑問がある方、もっとここが知りたい!!という所がある方など、ぜひ参加してください。参加申し込みは下記のURLからできます。

- (ここにURL入れる)

では、次回もよろしくお願いします。
