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

今回もいままでと同様書籍の読みあわせは行わず、ざっと内容について解説をしたあとに質疑応答を中心に進めました。

自己紹介
========
最初に全体で自己紹介を行いました。全部でXX名の方が参加してくださいました。

フル参加の方も。集合知プログラミング読めるようになってきた。
前回githubがとりあげられたのでアカウント作ってdot fileアップしたしてみた。
ながしまさん、Python素人

- 小池さん、アライドアーキテクツの人。4月から働き始めた
- むたさん、アライドアーキテクツの新人。Python一ヶ月
- たにさん、4月から転職してPythonはじめた。
- おおたさん、2回目、メーカーで技術サポート、趣味でPython
- よこいさん、3回目、PC持ってきていない、今回本も忘れたw
- にしざきさん、データサイエンティストやりたい
    
第4章 PyData入門
================

自己紹介
--------
ALBERTで働いている。データ分析をしている。
データの前処理からPythonを使うようになった。今日はPyData入門の話をするよ。

PyData.Tokyoのオーガナイザーをやっているよ。

去年のPyCon JP 2014というPythonのイベント、チュートリアルでPyData入門を講師としておこなった。そこでいろんな出会いがありPyData.Tokyoをたちあげた。
PyCon JP 2015は10月に開催予定。機械学習、データ処理系のProposalが結構出ていた。

今日はPandasを中心に話していく予定。あとは紙面の都合で触れられなかった話をしたい。
また、出版後のPandasのアップデート情報についても触れていこうと思う。

4-1 IPythonの使い方
-------------------
ちょうど3.0が校正の時にリリースされた。
そのため、2.4を対象とした。
``ipython[notebook]`` とするとあとででてくるIPython Notebookで使うものもインストールされるよ。

- コマンドラインでIPython使っている人っている?→いない

  - Notebookでさわっている
  - IDEで触っている人
  - 対話モードで使う人はあまりいなかった

4-2 PyData用パッケージの基本
----------------------------
いけうちさんの会社ではデータ解析には「R」を使っている人が多い。
SASとかの分析ツールを使う場合もある。
学術領域だとmatlab。
データの加工、集積にはSQLを使っていることがある。
その次にPythonを使っている感じ。

Rを使う理由としては、論文で出てきたアルゴリズムの実装やライブラリがRで公開されるのが早いため。情報も多い。

Python→Pythonだと一つ覚えればなんでもできる。
データ解析もできるし、Webアプリを作ったりとか。
データ解析した結果をWebで表示するデモアプリを作ったりとかもできるのでうれしい。

Pythonは書きやすいし読みやすいよ。

Pandas 0.16.2 で新しい機能が出たので補足する。

深層学習は最近buzzっている人工知能の中はこのあたり。
Pylearn2を書籍で紹介したが、最近はchainerが話題になっている。
Python的に書けてよさそう。

`Chainer: A flexible framework of neural networks <http://chainer.org/>`_

NumPy
~~~~~
Pythonはfor文を書いたら負け。データがデカイ場合。
C、Java、Goに比べると遅い。NumPyを使うと速くなる。
行列計算じゃなくても速いものがある。

行列をPyCharmできれいに見れるのもうれしい。PyCharmは最近PyData系のサポートが厚くなっている。

画像処理(OpenCV)を使うときにNumPyが必要。画像を行列で扱っている。

SciPy
~~~~~
マーケティングのときには「距離(似ているかどうか)」が大事。
ユーザーが似ている、アンケート結果が似ている。
距離の計算もいろいろあるが、ユークリッド距離が一番有名。

ツールとしてSciPyを使うことはあまりなさそう。機能は多すぎるらしい。

SymPy
~~~~~
趣味で紹介した。実例はとくに思いつかないので、教えてほしい。

子どもがいたら、中学の数学の勉強に使えるかもしれない。

Pandas
~~~~~~
Dataframeという行列のデータがある。行列に名前がある。
Rにもデータフレームがある。Pandasを作った人もRを意識してるんじゃないかなと思っている。

Rを使っている人はPandas使ってみるといいかもね。

生ログはテキストでS3とかよくあると思う。

- Q: PandasのデータのSelializeでパフォーマンスが出るのはなに?
- A: リアルタイムでやりとりしてる。両方Pythonだったらpickleでいいのでは?to_msgpackがあるので、よさそう
- Q: Version 1.6にしたらwarningが出るようになった
- A: だまらせるオプションでだまらせるでいいんじゃないですかね
- Q: Pandasで書いたスクリプトをPython2→3で使いたい。print とか気をつければ大丈夫?
- A: 問題ない。日本語周りは気をつけた方がいい。
- Q: Pythonでfor文使っちゃいけない。mapとか。
- A: forだと遅いけど、内包表記の方が速い。NumPy使うとか。map、filterは勉強しよう。

      `どこまで速くできる？ 達人に学ぶPython超高速データ分析～PyData.Tokyo Meetup #4イベントレポート (1/3)：CodeZine（コードジン） <http://codezine.jp/article/detail/8687>`_

クロス集計もよく使っている。
      
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

