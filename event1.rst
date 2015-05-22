======================================
 「Pythonエンジニア養成読本」読書会01
======================================

.. contents:: 目次
   :local:

はじめに
========

読書会の進め方
==============

自己紹介
========
- nisida: 大学でC言語、SDNでPython使うことが多いので
- たじま: 集合知プログラミングをやりたい。勉強している
- はせがわ: 仕事Android開発
- にしかわ?: ストレージのサポート、splitとかの延長で使えないかな。プログラミング言語は素人
- ほり: WebエンジニアでPHP。Pythonのソースを見てこれだと思った
- あべさん: Ficanceの研究所。RとかC++とかExcel.VBAとか。会社でPythonを使っていきたい
- おのでら: ECサイトをJavaで開発している。4月の勉強会でPythonをさわってみた
- いしい?: AWS、SeleniumのSDKをさわるのにPythonを使っていた。ちゃんと覚えようと思って
- よこい: 昔、科学技術計算のIFがPythonだった。今は営業。Excelで集計している。PyData
- あくつ: メーカーでマーケティングをやっている。Data ScientistになりたいのでPythonを勉強しはじめた。Webとリアルな場に出ることが必要だと思った。来週はつじしんごさんと勉強会をやる
- はやし: gihyo.jp Pythonぜんぜんわからないけど写真を撮っている
- hirokiky: 今日は2章担当。普段はPython Djangoを書いている。教育とかもしている
- sekine: Webの章を担当。今日は会場担当。普段はWebアプリケーションをJava, PHP, Python。毎月Pythonもくもく会をやっている

第1章 よくわかるPythonの世界
============================
- brew で両方はいるよ
- 2to3
- six

kyの自己紹介
============
- PyCharm自慢
- 使いやすいよ
- Community Edition  

第2章 これだけは知っておきたいPython言語はじめの一歩
====================================================
- チュートリアルやればいいけど、でも長いよ
- やさしくはないけど、いいドキュメントです
- はじめてのPythonはいい本だけど分厚い。808ページ
- Pythonスタートブックは導入にはいい本→クラスは書けない
- 集合知プログラミング→Pythonの書き方がきれいではない

- Pythonチュートリアルから削って作った感じ
- ./configure --prefix でインストール先を分けられるよ
- 3章に出てくるvirtualenvを使って、仮想的なpython環境を作る→詳しくは次回
- FizzBuzzのコードを書くところまでは結構こまかく説明
- Project Eulerをおすすめ https://projecteuler.net/
  - とくと人のコードが見れるよ
- rangeは101で100なのか。rangeのソースがみたい→PyCharmでとんだら見れなかったw
- range(start, end, step)を書けるよ

- 文字列とか型についてざっと説明
- スライス
- encode, decodeでなぜこうなるの?→書籍の都合で「日」の部分だけをdecodeしている
  - unicode文字をそのまま表示してくれないので print 文を使っている
  - python 3だと日本語が表示される
  - PEPがあって、いしもとさんが書いた(あとでリンクしよう)
- 型推論とかは?
  - annotationはPython 2にはない
  - Python 3.5だとできるようになる?
  - docstringに

- collection
  - リスト内包表記だときれいにかけるよ
- tupleはimmutableだよ
- 辞書は順番がないよ  
- Setは順番は持っていない。同じ値が入らない
- リスト内包表記って→実行が速い
  - 複雑になるなら書かない方がいい
- データが多い時どうする?
  - 集合を使うと容量は少なく、inも速い
  - もっと多いならredisとかミドルウェアを使う  
- importでよみだせるよ
  - 標準ライブラリがたくさんあるよ→便利なものを知っておくと便利
- import でメソッド内で読むのはどう?
  - おすすめしない。なにに依存しているのか見難くなる
- pyoファイルがうざい→モジュール分割したほうがいいので気にしない
  - パフォーマンスもあるので、しょうがない
  - 別の場所においたりできるといいな→たしかに
- getでdefaultを指定するのがおすすめ
    
ビアバッシュ
============
- http://connpass.com/category/Python/
- http://pyconjp.blogspot.jp/2015/04/python-event-201505.html
- http://connpass.com/event/14076/
- http://www.amazon.co.jp/s/ref=nb_sb_noss?__mk_ja_JP=%E3%82%AB%E3%82%BF%E3%82%AB%E3%83%8A&url=search-alias%3Daps&field-keywords=%E3%82%A8%E3%83%B3%E3%82%B8%E3%83%8B%E3%82%A2%E9%A4%8A%E6%88%90%E8%AA%AD%E6%9C%AC

まとめ
======

