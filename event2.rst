=======================================
 「Pythonエンジニア養成読本」読書会 02
=======================================

.. contents:: 目次
   :local:

はじめに
========
`「Pythonエンジニア養成読本」読書会 02 <http://pymook.connpass.com/event/15198/>`_

自己紹介
========
- takesxisximada:
- たじまさん2回め、集合知プログラミング読みたい。はじめてのPython読んでる
- にしだ: 2回め、会社でちょっとしたScriptをPythonで書きだした
- あくつさん: 2回め、メーカーでマーケティング。Pandas使いたい
- かんさん: 1回めネットワークセキュリティ関係、Pythonでスクリプト書きたい
- おおたさん: 1回目、技術系の会社で問い合わせ対応。趣味で統計を勉強し始めてRをかじった。その延長でPythonを
- おのでら: 2回目、ECサイトをシステム開発Javaで、Pythonも勉強したい
- らくのさん?: 1回目、開発でPythonちょっと使うけどまわりにPython使っている人がいない
- よこいさん: 2回目、会社では営業でデータ分析でPyData使いたい。科学技術計算で使っている
- きしかわさん: 2回目、ストレージのサポート。bash, perl。PyCharmを使い始めた
- はやし: 2回目。gihyo.jp。今日も写真を撮りに来た
- ky: 2回目、2章担当。今日は参加者。普段はPython Djangoで仕事している
- にしざき: 去年数学科を卒業して、Pythonいいなーと
- むらおか: 仕事でPython、Webやっている。知り合いが本を書いたので試しに参加した
- やすだ: 1回目、サービス系、スマホアプリ、PythonでWebサービスも作っているので詳しい人の話も聞きたい
- はせがわ: 2回目、仕事ではAndroid、今日はチーム開発の話なのでいろいろ活かしたい
- iktakahiro: 1回目、PyData担当。来月やります。イメトレで来た
- さとうまさき: 会社の人。PHP書いてる。飛び入り参加
- せきね: Webの章を担当。8月にやります

Appendix1 便利な標準ライブラリ、サードパーティ製パッケージ
==========================================================
- 自己紹介。PyCon SG, PyCon APACのこととか
  
Pythonの付属バッテリー、標準ライブラリ
--------------------------------------
- めっちゃあるよー
- pipコマンドをWindowsで→sudoしなければOK
- shutil, re
- argparse
- logging
- shutilはosでできるけど、より楽にしてくれる

Pythonをさらに強力にするサードパーティ製パッケージ
--------------------------------------------------
- oauthlib
- lxml
- stackflowを使う
- PyPIランキング

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

