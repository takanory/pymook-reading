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

ここで「コマンドラインでIPython使っている人はいるのか?」という質問がありました。解除ではコマンドラインで使っている人はあまりおらず、IPythonは以下の2パターンで使用している人が多いようでした。

- IPython Notebookで使用している
- IDE経由でIPythonを使用している

4-2 PyData用パッケージの基本
----------------------------
この節ではPyDataというカテゴリで語られる、Pythonでデータ解析を行うためのパッケージについて紹介しています。

著者の池内さんの会社ではデータ解析には `R言語 <https://ja.wikipedia.org/wiki/R%E8%A8%80%E8%AA%9E>`_ を使っている人が多いそうです。
他には `SAS <http://www.sas.com/>`_ などの分析ツールを使う場合もあるそうです。
学術領域では `MATLAB <https://jp.mathworks.com/programs/nrd/matlab-trial-request.html?ref=ggl&s_eid=ppc_8182277122&q=matlab>`_ を使っていたり、データの加工、集積にはSQLを使っていることもあるそうです。
その次にPythonを使っているという感じだそうです。

.. warning::

   その次とはどういう意味か確認する

R言語を使用している理由としては、論文で出てきたアルゴリズムの実装やライブラリがR言語で公開されるのが早く、R言語そのものの情報も多いのだそうです。

そこでなぜPythonなのかというと、Pythonは汎用のプログラミング言語なので、一つ覚えればなんでもできるところが魅力だと語っていました。
PyData関連のパッケージを使用すればデータ解析もできるし、Webアプリを作ったりも当然できます。
データ解析した結果をWebで表示するデモアプリを作ったり、といったことも一つの言語で完結しているのが魅力だと語っていました。

また、Pythonはプログラミング言語として書きやすいし読みやすいことも魅力であると言っていました。

Pandas 0.16.2 で新しい機能が出たので補足する。

書籍の中では最近はやっている深層学習(ディープラーニング)について
`Pylearn2 <http://deeplearning.net/software/pylearn2/>`_ を紹介していましたが、
最近リリースされた `Chainer <http://chainer.org/>`_ が話題になっていると紹介されていました。
Chainer は Pylearn2 とは違い Python 的に書けるのがよいそうです。また、日本で開発されており、日本語のドキュメントが豊富なことも魅力です。

読書会では以下のPyData関連パッケージについて紹介しました。

NumPy
~~~~~
Python では大量のデータを for 文で処理すると時間がかかります。
しかし、 `NumPy <http://www.numpy.org/>`_ を上手に使うと、行列計算などを高速に処理ができます。

行列のデータを PyCharm (Python用のIDE)できれいに表示されます。
PyCharmは最近PyData系のサポートが厚くなっているそうです。

余談ですが画像処理の `OpenCV <http://opencv.org/>`_ にはNumPyが必要です。
これば、画像データを高速に処理するために、NumPyの行列データを利用しているためです。

SciPy
~~~~~
マーケティングのときには「距離(似ているかどうか)」が大事であり、ここでいう距離とは「ユーザーが似ている」「アンケート結果が似ている」といったものを表します。
この距離計さんは `SciPy <http://www.scipy.org/>`_ を使用すると簡単にできるそうです。
距離の計算にはいろいろあるな種類がありますが、 `ユークリッド距離 <https://ja.wikipedia.org/wiki/%E3%83%A6%E3%83%BC%E3%82%AF%E3%83%AA%E3%83%83%E3%83%89%E8%B7%9D%E9%9B%A2>`_ が有名です。

SciPyは非常に沢山の機能を提供しており、個人的にはツールとしてSciPyを使うことはあまりなさそうとのことです。

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
- Q: Python で for 文を使ってはいけないのかちゃいけない。map とかはなかなか難しい。
- A: for 文だと遅いのでわかりやすい場合は内包表記の方が速い。大量のデータを使う場合は NumPy を使いましょう。また map、filter は勉強しましょう。

余談としてデータ分析の高速化についての PyData.Tokyo でのレポートが紹介されていました。
  
- `どこまで速くできる？ 達人に学ぶPython超高速データ分析～PyData.Tokyo Meetup #4イベントレポート (1/3)：CodeZine（コードジン） <http://codezine.jp/article/detail/8687>`_

4-3 はじめてのIPython Notebook
------------------------------
3で変わったところ。

- ロゴが変わった。jupyterになった。

Notebookでプレゼンする人もけっこういる。

グラフがうれしい。

joinをfor文でまわしてif文とかだとつらいよね。SQLっぽく処理できるよ。
inner joinもできる。

0.16.2でpipeが追加になった。.pipe(メソッド)って書くとその処理がされる。
列が追加されたりもできるらしい。面白い。

グラフはggplot形式がよさげ。でもプレゼンじゃなければグラフ頑張らなくてもいいのでは。

`Seaborn: statistical data visualization — seaborn 0.6.0 documentation <http://stanford.edu/~mwaskom/software/seaborn/>`_
`Welcome to Bokeh — Bokeh 0.9.1 documentation <http://bokeh.pydata.org/en/latest/>`_

簡単なのはmatplotlibでよい。

githubでIPython Notebookのソース(.ipynb)があると、そのまま見れるようになった。

`nbviewer <http://nbviewer.ipython.org/>`_ が参考になる。

`Wakari - Web-based Python Data Analysis <https://wakari.io/>`_
はクラウド上でIPython Notebookが使える。
Anacondaというデータ分析用のパッケージのセットがあるが、それも最初から入っている。
`Anaconda Scientific Python Distribution <https://store.continuum.io/cshop/anaconda/>`_

`ŷhat | Rodeo: A data science IDE for Python <http://blog.yhathq.com/posts/introducing-rodeo.html>`_
というツールが有る。IPython Noteboookっぽいやつで、よりリッチ。
データフレームの値を見て、絞り込みとかも対話形式でできる。

IPython Notebookはあまり長いコードを書くのには向いていない。Rodeoは向いてるかも。

4-4 ［実践編］オープンデータの利用と可視化
------------------------------------------
オープンデータだけど見つからないとかデータ取得が面倒なものが多い。
横浜のデータはちゃんとしてる。

URL指定でもデータがとれますよ。

PyData.Tokyoのチュートリアルで、kaggleのチュートリアルでタイタニックの乗客リストから生存者を予測するということをやった。

(あとでURL)

describeで平均値、中央値とかざっと全体を見ることができる。

実際にその例で IPython Notebook で見せながら説明。

- Q: 横浜のグラフをいじろうと思って、地図データで可視化しようと思ったが挫折した。basemapっていうのがおすすめでしょうか?
- A: Pythonではないが、tablour(BIツール)でマッピングとかするが、日本はそこまで細かくないかも
  日本だと県ごととかの白地図しかない。JAXAの衛星データとかにマッピングするとか。
- Q: IPython Notebookをサーバーに入れて、みんなが使えるようにできるのか?
- A: ソリューションはあると思うが、おすすめできない。前にやったのはポートを分けたりした
- Q: デモするときにパラメーターを入れさせるとかはできるの?
- A: IPython Notebookでシークバーを用意するとかもできるよ
- Q: Windows で Anacondaを使っている。終わり方がわからない
- A: 基本的にはシェル側でCtrl-Cで止める
- Q: R、JS。言語間での連携はできない?
- A: できないので、ファイル渡しとか

ALBERTのページに統計についてとか書いているので、これから勉強しようとする人は、これを読むとよいかも。(あとでURL)
    
ビアバッシュ(懇親会)
====================
- 業務のためののLT
- 自分のProposalのLT(takesxi)
- PyCOnとかのLT(checkpoint)
- ついでにPythonのヒカラボイベントの紹介    

まとめ
======

