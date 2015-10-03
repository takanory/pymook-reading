================================================
 第5回 環境構築の自動化、活躍の場が広がるPython
================================================

.. contents:: 目次
   :local:

はじめに
========
鈴木たかのりです。

`前回 <http://gihyo.jp/news/report/01/python-training-book-reading-club/0004>`_
に引き続き
`Pythonエンジニア養成読本 <http://gihyo.jp/book/2015/978-4-7741-7320-7>`_
という書籍の `読書会イベント <http://pymook.connpass.com/>`_ についてレポートします。

今回が最終回となる `第5回の読書会 <http://pymook.connpass.com/event/19107/>`_ は9月17日(木)に `アライドアーキテクツ株式会社 <http://www.aainc.co.jp/>`_ の会議室で開催されました。

当日はだいたい以下のタイムテーブルで進めました。

- 19:00-19:15 参加者の自己紹介
- 19:15-20:50 「第6章 環境構築の自動化」
- 20:50-21:00 「Appendix 2 活躍の場が広がるPython」
- 21:00-22:00 ビアバッシュ(ビールとピザでの参加者懇親会)

今回も今までと同様に書籍の読みあわせはせず、補足情報や質疑応答を中心に解説を行いました。

自己紹介
========
最初に参加者の自己紹介です。
この読書会の3日前に開催された `Ansible Meetup in Tokyo 2015.09 <http://ansible-users.connpass.com/event/18015/>`_ に参加して、今日は違う話が聞けるかなと思って参加した方や、会社ではChefを使っているがAnsibleに切り替えたいと思っている方、業務などで普段Ansibleを使用している方などさまざまな人がいました。

第6章 環境構築の自動化
======================
一通り自己紹介を終えると、6章の著者の若山 史郎(`@r_rudi <https://twitter.com/r_rudi>`)から自己紹介がありました。

.. figure:: /_static/event5/P9171508.JPG
   :width: 400px
   :alt: 若山 史郎氏

   若山 史郎氏

6章のAnsibleでの環境構築の章の執筆担当で、普段の業務ではGoでプログラミングをしていてPythonは書いていないそうです。以前は仕事でもPython書いていたとのこと。
会社ではWebアプリの開発から運用までをカバーしているため、Ansibleも業務で使用しているとのこと。

この書籍の執筆では、入門Ansibleという書籍を出しており、それで声がかかったそうです(まぁ、筆者が声をかけたようなものですが)。

- `入門Ansible <http://www.amazon.co.jp/dp/B00MALTGDY/>`_

.. figure:: /_static/event5/P9171352.JPG
   :width: 400px
   :alt: 自己紹介の様子

   自己紹介の様子

この章で使用する `Ansible <http://www.ansible.com/>`_ はPythonで書かれていますが、普通に使用する分にはPythonでのプログラミングは行いません。
とはいえ、拡張を作成するときにはPythonが必要となります。

と、ここで読書会の本題に入ろうとしたのですが、若山さんは書籍のPDFを用意しておらず、本を読みながら進めようと思っていたとのこと。
それでは参加者がどこを話しているかわかりにくいので、急遽書籍のPDFデータを著者間で受け渡し、それを画面に表示するというグダグダな感じでスタートしました。

6-1 環境構築をなぜ自動化すべきか
--------------------------------
この節ではAnsibleの前に、なぜ環境構築を自動化するのか、そのメリットについて解説しています。

環境構築の対象となるサーバー台数が1台、2台と少なければ手作業でも問題ありませんが、台数が増えていくと手作業ではミスが発生する可能性が高いため自動は必須です。
自動化を行うのであれば、それは Ansible ではなく
`Chef <https://www.chef.io/chef/>`_ や
`Puppet <https://puppetlabs.com/>`_ でも問題ありません。

次の書籍にも載っている図はAnsibleを想定しています。Ansibleは対象サーバー(環境を構築する対象となるサーバー)にsshで接続して環境構築を行います。これは、対象サーバーにエージェントと呼ばれるプログラムをインストールする必要があるChefとは異なります。

.. figure:: /_static/event5/automation.png
   :width: 400
   :alt: 環境構築の自動化

   環境構築の自動化

また、環境構築の手順を Git などのリポジトリでバージョン管理することにより、うまく動作しない場合に元に戻したり、差分などの確認が行えるのが便利とのことです。

最近、SIerなどからも「Ansible使いたい」という話がよく聞かれるそうです。理由としてはChefなどはエージェントをインストールする必要があるため、そこがお客さんにいやがられるそうです。そのため、エージェントが不要なAnsibleが向いているとのことです。

ここでは以下の様な質疑応答がありました。

- Q: Ansible以外にもエージェントが不要sshだけで動作する環境構築ツールはあるか?
- A: 最近はChefや `SaltStack <http://saltstack.com/>`_ もエージェント不要で動作するようになってきている。これらは途中から思想を変えてきたが、最初から設計がssh前提のAnsibleの方が筋がいいのではないかと考えている。
- Q: Windowsの環境構築で使用可能か?
- A: WindowsとはWinRM(Windows Remote Management)経由で接続しPowerShellでの環境構築が可能。しかし、まだ洗練はされていない。
- Q: Chefのようにエージェントをインストールする利点はなにか?
- A: sshが通らない環境ではエージェントが必要となる場合がある。Ansibleにも **ansible-pull** というコマンドが付属しており、cronで最新の手順を取得して自分自身の環境に適用するといった使い方ができる。この使い方はエージェントっぽくもある。

6-2 Ansibleの導入
-----------------
この節では環境構築を自動化するために、Ansibleをインストールして利用を開始するところまでを解説しています。

書籍の中ではAnsibleのインストールは以下のように **pip** コマンドを使用した手順を紹介しています。
他にも、各種Linuxのパッケージ管理(apt, yum等)でもAnsibleはインストール可能で、依存ライブラリも合わせてインストールされるため、pipコマンドよりもこちらの方がわかりやすいかもしれないとのことです。

.. code-block:: sh
   :caption: pipでのAnsibleインストール
                
   # pythonのヘッダが必要なため、python-devをインストール
   $ sudo apt-get install python-dev
   # Ansibleをインストール
   $ sudo pip install ansible

書籍のコラムで『Ansible 2系ではPython 3系に対応予定です。』と書いてあります。ですが、もうすぐリリースされるAnsible 2は残念ながらPython 3対応していないそうです。
Python 3対応の準備は継続して進められており、Pull Requestを受け入れているそうです。われこそはと思わん方はぜひ協力してみてください。

Ansibleで環境構築を行うためには、サーバーへのアクセス情報をまとめた **Inventoryファイル** と環境構築手順をまとめた **Playbookファイル** の2種類のファイルが必要です。

Inventoryファイルは以下のようにホスト名が並んでおり ``[web]`` と ``[db]`` という2種類のグループがあるということを表しています。
このように記述することにより、webグループ全体に同じ手順で環境構築を行うといったことが可能になります。

.. code-block:: ini
   :caption: Inventoryファイルの例

   mail.example.com

   [web]
   webn01.example.com
   web02.example.com
   web03.example.com

   [db]
   db01.example.com

Playbookファイルには以下のように `YAML <http://ja.wikipedia.org/wiki/YAML>`_ 形式で環境構築手順を記述します。
このPlaybookの例ではwebグループの全サーバに対して ``appuser`` ユーザの作成、 ``/var/log/app`` ディレクトリの作成とnginx、mysql-clientのインストールを行います。

.. code-block:: yaml
   :caption: Playbookの例
                
   - hosts: web # 対象サーバを指定。今回はwebグループ
     sudo: yes # sudoを行う
     vars: # 変数指定
       logdir: /var/log/app
     tasks: # 実行するtaskの指定を開始
       - name: 実行用ユーザの作成 # taskの名前
         user: name=appuser
       - name: ログディレクトリの作成
         file: path="{{ logdir }}" state=directory
       - name: 依存ライブラリのインストール
         apt: name="{{ item }}" state=installed
         with_items:
           - nginx
           - mysql-client

Playbookについては以下の様な説明がありました。

- **tasks** の中に環境構築のタスクを入れる
- YAMLの中にJinja2のテンプレート(``{{ }}`` 形式)で変数が入れられる
- Playbookは基本的にタスクを積み重ねることによって環境を構築する
- 各タスクには名前(**name**)を日本語で書けるので、日本語で書くのがおすすめ
- なお、執筆時点ではまだ確定ではなかったが、今では sudo、suという設定は become に統一された

.. figure:: /_static/event5/P9171592.JPG
   :width: 400px
   :alt: Playbookについて解説中

   Playbookについて解説中

上記2つのファイルを用意したら ``ansible-playbook`` コマンドで環境構築を行います。
書籍では実行例が白黒となっていますが、実際には ``changed`` (環境構築が実行されたタスク)の部分は黄色で、 ``ok`` (環境構築がすでに行われているタスク)の部分は緑色で表示されるそうです。
Ansibleでは同じPlaybookを何度同じサーバーに対して実行しても、環境が同じ状態になります。
2回ユーザーを作成したりインストールしたりはしません。
このような特徴を **べき等性** と呼び、環境構築では非常に重要な概念となります。

Ansibleを使用して実際に環境構築を行う場合は、少しずつPlaybookにタスクなどを継ぎ足しながら実行するそうです。
べき等性があるため、何度繰り返しても一度実行したタスクが無駄に実行されることはありません。

ここでは以下の様な質疑応答がありました。

- Q: Playbookにハイフン(``-``)が入っていたり、入っていない項目があるがこれは何か?
- A: これはYAMLのフォーマットのため。ハイフンがリスト(list)を表し、コロン(``:``)で区切っているものが辞書(dict)を表している
- Q: nameに日本語を書いているが文字コードはなにか?
- A: 文字コードは **utf-8** しか使えない。以前はnameに日本語は使えなかったが Pull Request を送ってutf-8が通るようになった。Ansible はほとんどの個所はutf-8が通るようになっている。

6-3 少し高度な使い方
--------------------
この節ではPlaybookで複雑な動作を記述するための機能について解説しています。

with_items
~~~~~~~~~~
**with_items** はシンプルなループ処理を行います。
以下のPlaybookは複数のディレクトリを作成します。

.. code-block:: yaml
   :caption: with_itemsの例

   tasks:
   - name: /opt/foo以下にbin, conf, logディレクトリ作成
     file: path=/opt/foo/{{ item }} state=directory
     with_items:
       - bin
       - conf
       - log
         
条件分岐などを含んだ複雑なループをPlaybook上で実現したい場合は、PluginをPythonで書く必要があるそうです。

Pluginの書き方は「入門Ansible」に書いてあるよ!!という宣伝がここで入りました。

when
~~~~
**when** は条件分岐を行います。
以下のPlaybookはサーバーの役割によってインストールするアプリケーションを切り替えています。

.. code-block:: yaml
   :caption: whenの例

   tasks:
     - name: 役割がwebだったらnginxを入れる
       apt: name=nginx state=present
       when: server == "web"
     - name: 役割がdbだったらmysql-clientを入れる
       apt: name=mysql-client state=present
       when: server == "db"

Ansibleを実行すると、対象のサーバーに入ってさまざまな情報を収集します。
OSのディストリビューションとバージョン、カーネルのバージョン、IPアドレスなど多岐にわたります。
この情報をそのまま条件分岐に利用できるため、「CentOS 6ならこれを実行する」といった書き方も可能とのことです。

roles
~~~~~
**roles** は大事な機能で、うまく使いこなせるとAnsibleが上手に使えるとのことです。しかし書籍ではページの都合もありあまり触れていません。
書籍では `Ansible Galaxy <https://galaxy.ansible.com/>`_ というroleの共有サービスから取得したroleを使用しています。

以下のコードはroleを使用してサーバーにredisの環境を構築する例です。

.. code-block:: sh
   :caption: ansible-galaxyでRedisのroleをインストール

   $ mkdir -p roles # rolesというディレクトリを作成する
   $ ansible-galaxy install DavidWittman.redis -p roles

.. code-block:: yaml
   :caption: roleの使用例

   - hosts: web
     sudo: yes
     vars:
       - redis_bind: 127.0.0.1
     roles:
       - DavidWittman.redis

運用の現場でも Ansible Galaxy で適切な role を探して使用しているそうです。
対応している platform で絞られるため、だいたい使えるものは決まってくるそうです。
また、よい role があったが Linux のディストリビューションが異なる場合は、githubでforkして修正して使用したりしているそうです。

.. figure:: /_static/event5/P9171793.JPG
   :width: 400px
   :alt: roleについて図を使って解説

   roleについて図を使って解説

ここで書籍に載っていない機能についての紹介がありました

- register

  **register** は、実行した結果を変数に保存します。実行結果によって次の処理を分岐させたりできます。

- local_action

  **local_action** はAnsibleを実行している管理サーバー側でタスクを実行する機能です。
  Amazon EC2のインスタンスを立ち上げたりなど、管理サーバー側で行うべきタスクに使用します。

  Ansibleではさまざまなクラウドの操作ができます。
  `Cloud Modules <http://docs.ansible.com/ansible/list_of_cloud_modules.html>`_ のページを見ると、Amazon以外にCloudstack、Google、Rackspaceなどのモジュールがあることがわかります。

  AWSの環境構築をChefで行うには `CloudFormation <https://aws.amazon.com/jp/cloudformation/>`_ と `OpsWorks <https://aws.amazon.com/jp/opsworks/>`_ を使用するのがAWS側の提案ですが、同様のことがAnsibleだけで実現できるとのことです。
  
ここでは以下の様な質疑応答がありました。

- Q: AWS使う時の管理サーバーはローカルでか、それともAWS上か?
- A: どちらもありえる。関係者がログインできるAnsible実行ホストをAWS上に用意するというパターンもある
- Q: roleの切り方や変数の置き方に悩まないか?
- A: あまり悩まない。roleの切り方をミスると悩むと思う。roleはアプリとかミドルウェアごとに作り、roleの中だけで完結するようにする。role dependency(依存関係)は使っておらず、使わない方がよい。
  AロールはBロールに依存しているという風に書け、勝手に実行されるのは便利だが、なにが実行されているか見えなくなるのであまりおすすめしない。Ansibleはタスクの実行順序を指定できる(上から順番に実行される)ので、自分で明示して実行する方が良い
- Q: 開発環境、ステージング環境など環境ごとの切り替えはどのようにしているか?
- A: 変数で切り替えるのがよい。条件付き実行を使用してproductionなら本番環境用の変数を読み込むという指定をする。modeでproduction/stagingを切り替えている
- Q: クラウド用のコマンドを抽象化したようなものはないか?
- A: 今のところはない。それぞれのクラウドサービスが提供する機能が違うため。共通化すると設定できることが少なくなりそう。
  余談だが、Ansibleではインストールはyum, aptとディストリビューションごとに分かれている。 **package** に統一してはどうか?という話も出ているが、現状は統一されていない。インストールするパッケージ名もapache2, httpd2のように異なるため分かれている方が無難だと考えている。

6-4 よく使うモジュール
----------------------
この節では200以上もあるAnsibleのモジュールのうち、よく使われるものを紹介しています。書籍では以下のモジュールを紹介しています。

- script: スクリプトを実行する
- shell: 任意のコマンドを実行する
- file: ファイルの作成、所有者の変更などのファイル操作を行う
- template: `Jinja2 <http://jinja.pocoo.org/>`_ テンプレートを使用して変数を埋め込んだファイルを生成する
- unarchive: 圧縮ファイルを展開する
- apt: aptコマンドを使用する
- user: ユーザを追加、削除する

この中で一番知ってほしいのは **script** モジュールで、scriptモジュールがあれば今使っているスクリプトをそのままAnsibleで使えるようになります。
**creates** 引数を指定すると、一度だけ実行されるスクリプトになります。
こうすることにより、簡易的にべき等性のあるスクリプトとなります。

.. code-block:: yaml
   :caption: scriptモジュール
                
   tasks:
     - name: command.shを実行する
       script: command.sh
     - name: files/other.shを実行する。/tmp/done.txtがあれば実行しない
       script: files/other.sh creates=/tmp/done.txt

Ansible 1.9では260、Ansible 2.0では400くらいのモジュールがあるそうです。
何か実行したい内容があれば `docs.ansible.com <http://docs.ansible.com/>`_ を検索してモジュールを探してみてください。

通常の shell script と比べて以下の様な利点があるため、Ansibleは **better shell script** だと考えているとのことです。

- 複数サーバーに並列して実行できる
- 書き方が統一できる
- べき等性がある

.. figure:: /_static/event5/P9171916.JPG
   :width: 400px
   :alt: 質疑応答の様子

   質疑応答の様子

この節と全体を通して、以下の様な質疑応答がありました。

- Q: すべての構成をAnsibleでやるとかいう考えはあるか?
- A: とくにはない。目的に合致するもっといい方法があればそちらを使うべき。
- Q: `Docker <https://www.docker.com/>`_ と `Kubernetes <http://kubernetes.io/>`_ などのコンテナ技術と、Ansibleのような環境構築の自動化はそのように使い分けたらよいのか?
  `Capistrano <http://capistranorb.com/>`_ とかともまた違うのか?Ansibleの使いどころを知りたい。
- A: 自動化ツールとして以下の2系統があり、Ansibleは両方できることが売りになっている。 **SIMPLE. AGENTLESS. POWERFUL.** がAnsibleの特徴。

  - Configration Management Tool(構成管理ツール): Chef, Puppetなど
  - Orchestration Tool(リモート実行ツール): Capistrano, Fabricなど

- Q: Ansible.com はどうやって稼いでいるのか?
- A: Ansible.com 社の人がメインで Ansible を開発をして公開している。
  Ansible社は `Ansible Tower <http://www.ansible.com/tower>`_ というツールを販売している。
  Ansilbe Tower はWeb画面からAnsibleを実行したり、Webhookで実行したりといった様々な機能を提供している。
  他にはAnsibleのトレーニングやコンサルティングを実施している。
  しかし、Ansible Towerを使ったことはない。
- Q: 「Orchestration Tool(リモート実行ツール)としても使える」とあったが、複数サーバー間で連携して動作させることは可能か?AサーバーのDBがインストールされたら、BサーバーのXXXをインストールするといったようなことを想定している。
- A: 分散実行ではなく、シリアルで順番に実行すればよいと思う。
- Q: Playbookのファイルをリポジトリで管理するのが望ましいとあったが、リポジトリはどこに置くべきか?
- A: Git を使うのであれば github でもよいし、社内のgitサーバーでもよい。
- Q: sshの秘密鍵の管理はどうすれば安全になるか?秘密鍵そのものをリポジトリにコミットしたくない。
- A: ファイルについては分けておいたほうがよい。
  パスワード、Tokenとかの秘密情報をPlaybookに書きたい場合がある。
  その場合は `Ansible Vault <http://docs.ansible.com/ansible/playbooks_vault.html>`_ という機能で暗号化した情報をPlaybookに書き込み、実行時に Vault 用のパスワードを入力して復号化して実行ということができる。
- A: HashiCorpの `Vault <https://vaultproject.io/>`_ も秘密情報を持てるので、Ansibleと連携するとよいかも知れない。

Appendix2 ますます活躍の場が広がるPython
========================================
少し時間が余ったので、最後のAppendix2の紹介をこの節の著者でもある筆者(鈴木 たかのり)から行いました。

.. figure:: /_static/event5/P9172027.JPG
   :width: 400px
   :alt: Appendix2 について紹介

   Appendix2 について紹介

このAppendix2では半分ネタとして、ちょっと変わった環境でもPythonが動作しているということを紹介しています。
書籍では主に以下のような少し変わった環境で動作するPythonについて紹介しました。

- `Pepper <http://www.softbank.jp/robot/special/pepper/>`_: ロボットの動作をPythonでプログラミングできる
- `Micro Python <https://micropython.org/>`_: マイコン上で直接Pythonが実行できる
- CG: `Blender <http://blender.jp>`_ 等のCGツールのスクリプトとして利用できる

Pythonは設計思想として「シンプルで読みやすいコードを書けること」があります。この思想により、さまざまなツールのスクリプト言語として採用されているのではないかと考えられます。

余談ですが、書籍にはPepper、Micro Pythonの写真やBlenderの画面が掲載されています。
これらの画像を自分で用意するのは大変ですが、これらを使用している知り合いにお願いして画像を提供してもらい非常に助かりました。
その節は、ありがとうございました。

ビアバッシュ(懇親会)
====================
読書会の後は毎回恒例のビールとピザによるビアバッシュ(懇親会)です。
最終回なのでビールの単価を少し上げてみました。

.. figure:: /_static/event5/P9172087.JPG
   :width: 400px
   :alt: ビアバッシュ

   ビアバッシュ

いつものように会話を楽しんだ後にライトニングトーク(LT)大会を行いました。

LT1 - cowsay
------------
1番目は今日のメインスピーカーでもある若山 史郎(`@r_rudi <https://twitter.com/r_rudi>`_)さんによる **cowsay** の話です。

Linuxなどにはメッセージを牛にしゃべらせる `cowsay <https://ja.wikipedia.org/wiki/Cowsay>`_ というジョークプログラムがあります。

.. code-block:: sh
   :caption: cowsayの実行例

   $ cowsay Python engineer training book
    _______________________________ 
   < Python engineer training book >
    ------------------------------- 
           \   ^__^
            \  (oo)\_______
               (__)\       )\/\
                   ||----w |
                   ||     ||

Ansibleはこのcowsayが大好きで、cowsayがインストールされているとデフォルトでAnsible実行時のメッセージをcowsayを使って出力します。
ウザいことこの上ありません。

この表示をオフにするためには環境変数で ``ANSIBLE_NOCOWS=1`` と設定するとよいそうです。
AnsibleのFAQにも `How do I disable cowsay? <http://docs.ansible.com/ansible/faq.html#how-do-i-disable-cowsay>`_ と書いてありました。

.. figure:: /_static/event5/P9172113.JPG
   :width: 400px
   :alt: Ansibleの実行結果がcowsayで表示されている様子

   Ansibleの実行結果がcowsayで表示されている様子

LT2 - ゴルフ
------------
2番目のLTは第2章の執筆を担当した嶋田 健志(`@TakesxiSximada <https://twitter.com/TakesxiSximada>`_)さんによる「ゴルフ」です。

.. figure:: /_static/event5/P9172149.JPG
   :width: 400px
   :alt: 嶋田さんによるLT

   嶋田さんによるLT

が、プレゼンテーションの前半でPCがフリーズしてしまい発表が聞けませんでした。
以下に資料へのリンクを貼っておきますが、Pythonでの `コードゴルフ <https://ja.wikipedia.org/wiki/%E3%82%B3%E3%83%BC%E3%83%89%E3%82%B4%E3%83%AB%E3%83%95>`_ (できるだけ短いコードでお題を解くコンテスト)の話です。

.. raw:: html

   <iframe src="//www.slideshare.net/slideshow/embed_code/key/amU5VhkcFeb48H" width="425" height="355" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="//www.slideshare.net/TakesxiSximada/ss-52895911" title="ゴルフ" target="_blank">ゴルフ</a> </strong> from <strong><a href="//www.slideshare.net/TakesxiSximada" target="_blank">Takesxi Sximada</a></strong> </div>

LT3 - 業務のためのPython勉強会
------------------------------
LTラストは阿久津(`@akucchan_world <https://twitter.com/akucchan_world>`_)さんによる勉強会の紹介です。
阿久津さんは今回は参加できないと思っていたそうですが、なんとか時間ができたそうで最後の方に駆けつけてきてくれました。第1回から全てに参加してくれて、非常にありがたいです。

発表の内容は阿久津さんが主催している
`業務のためのPython勉強会#5 <http://startpython.connpass.com/event/20092/>`_
の紹介でした。次回は10月14日(水)に開催予定だそうです。

.. figure:: /_static/event5/P9172164.JPG
   :width: 400px
   :alt: 阿久津さんによるLT

   阿久津さんによるLT

筆者もこの勉強会に参加したいと思っていたのですが、読書会やPyCon JPの準備などいろいろ忙しくて参加できていませんでした。次回は参加しようかなと考えています。

おわりに
========
今回で「Pytonnエンジニア養成読本」の読書会と読書会レポートは終了です。
5月からはじめて全5回に渡った読書会を、なんとか完走することができました。

この日は、執筆者も全員揃うことができたので、記念撮影をしました。
左から担当した章の順番に並んでいます。

- 鈴木 たかのり: 第1章 よくわかるPythonの世界(`第1回読書会 <http://gihyo.jp/news/report/01/python-training-book-reading-club/0001>`_)
- 清原 弘貴: 第2章 これだけは知っておきたいPython言語はじめの一歩(`第1回読書会 <http://gihyo.jp/news/report/01/python-training-book-reading-club/0001>`_)
- 嶋田 健志: 第3章 開発環境とチーム開発(`第2回読書会 <http://gihyo.jp/news/report/01/python-training-book-reading-club/0002>`_)
- 池内 孝啓: 第4章 PyData入門(`第3回読書会 <http://gihyo.jp/news/report/01/python-training-book-reading-club/0003>`_)
- 関根 裕紀: 第5章 入門Webアプリケーション開発(`第4回読書会 <http://gihyo.jp/news/report/01/python-training-book-reading-club/0004>`_)
- 若山 史郎: 第6章 環境構築の自動化(第5回読書会)

「Pythonエンジニア養成読本」が出版できて、読書会を開催できたのはみんなのおかげです。
私の思いつきではじめた読書会に快く協力してくれて、本当にありがとうございました。
それぞれのスタンスで面白い解説や追加情報が聞けて、有意義な読書会になったと思います。

.. figure:: /_static/event5/P9172204.JPG
   :width: 400px
   :alt: 執筆者が勢揃い

   執筆者が勢揃い

そして、この `読書会をはじめるとき <http://gihyo.jp/news/report/01/python-training-book-reading-club/0001>`_ に動機として『単純にこの本を読んだ人はどんな人たちで、どんな感想を持っているのか知りたい』ということを書きました。
全5回を終えてみて当初の目標は想定以上に達成できて、今までのコミュニティ活動ではあまり会ったことがない人たちにたくさん出会うことができました。

複数回参加してくれる方もたくさんいて、この読書会に参加してなにか楽しいことや得るものがあったのかなと思い、非常にうれしく思います。
また、自己紹介でなんらかの進捗(「XXXを試してみた」など)を聞いたりすることも非常にうれしかったです。

今回でこの読書会は終了しますが、この書籍と読書会をきっかけにPython関連コミュニティに参加、活動してくれると非常にうれしいです。
コミュニティに関わっていれば、PyCon JPなどどこかのイベントで会うこともあると思います。
その時は、同じ仲間として声をかけあえるといいかなと思います。

.. figure:: /_static/event5/P9172207.JPG
   :width: 400px
   :alt: 第5回読書会参加者の集合写真

   第5回読書会参加者の集合写真

それでは、またどこかでお会いしましょう!!
See you in Python related community everywhere!!
