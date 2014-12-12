OpenStackハンズオン 基礎編
================

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/_title.png

----

基礎操作
================

- 目的

  - OpenStack上にHorizonを使って踏み台サーバを構築します。
  - CLIを使ってシンプルなWEBサービスを実行する環境を構築します。

----

講師
================

- @irix_jp

  - 日本OpenStackユーザ会

    - 会長

  - 一般社団法人クラウド利用促進機構

    - 技術アドバイザー

  - 国立情報学研究所

    - TOPSEコース 講師

  - SIer勤務

    - 普段はOSSを使ったクラウド技術の企画・開発

----


環境の確認
================

- 各自、ログイン情報を使って、Horizonへログインできるか確認してください。
- http://192.168.253.1/horizon/

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/01_login.png
   :width: 300

----


前半：踏み台サーバーの構築
================

----



踏み台サーバーの役割
================

- 今回の環境は、まずOpenStack上に踏み台サーバーを構築し、ここにログインしてその後の作業を行っていきます。

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/02_step-server.png
   :width: 800


----


作業の流れ
================

- 仮想ルーター Ext-Router の作成
- 仮想ルーターと、Ext-Netの接続
- 仮想ネットワーク work-net の作成

  - CIDR: 10.0.0.0/24   GW: 10.0.0.254

- キーペア key-for-step-server の作成
- セキュリティグループ sg-for-step-server の作成

  - ssh を許可する

- 踏み台サーバーの作成
- Floating IPの割り当て
- SSHで踏み台サーバーへログイン **ゴール**

----


仮想ルーターの作成
================

1 初期状態のネットワークトポロジー

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/03_router_00.png
   :width: 800

----

仮想ルーターの作成2
================

2 「ルーターの作成」を選択

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/03_router_01.png
   :width: 800

----

仮想ルーターの作成
================

3 仮想ルーター： *Ext-Router* を作成

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/03_router_02.png
   :width: 600

----

仮想ルーターの作成
================

4 作成された Ext-Router の 「ゲートウェイの設定」 を行う

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/03_router_03.png
   :width: 800

----

仮想ルーターの作成
================

5 外部ネットワーク *Ext-Net* を選択する。

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/03_router_04.png
   :width: 600

----


仮想ルーターの作成
================

6 ルーター作成後ののネットワークトポロジー

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/03_router_05.png
   :width: 800

----



仮想ネットワークの作成
================

1 「ネットワークの作成」を選択

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/04_network_01.png
   :width: 800

----

仮想ネットワークの作成
================

2 ネットワーク名： *work-net*

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/04_network_02.png
   :width: 600

----

仮想ネットワークの作成
================

3 サブネット名： *work-subnet*     ネットワークアドレス： *10.0.0.0/24*    ゲートウェイIP： *10.0.0.254*

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/04_network_03.png
   :width: 600

----

仮想ネットワークの作成
================

4 DNSサーバー： *8.8.8.8* & *8.8.4.4*

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/04_network_04.png
   :width: 600

----

仮想ネットワークの作成
================

5 *work-net* が正常に作成された状態

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/04_network_05.png
   :width: 800

----

仮想ネットワークの作成
================

6 *Ext-Router* を選択（リンクをクリック）

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/04_network_06.png
   :width: 800

----

仮想ネットワークの作成
================

7 「インターフェースの追加」を選択

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/04_network_07.png
   :width: 800

----

仮想ネットワークの作成
================

8 サムネット *work-net 10.0.0.0/24 (work-subnet)*  を選択

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/04_network_08.png
   :width: 600

----

仮想ネットワークの作成
================

9 正常にインターフェースが追加された状態

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/04_network_09.png
   :width: 800

----

仮想ネットワークの作成
================

10 ネットワーク作成後のトポロジー図

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/04_network_10.png
   :width: 800

----


キーペアの作成
================

1 「キーペアの作成」を選択します。

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/05_keypair_01.png
   :width: 800

----

キーペアの作成
================

2 キーペア *key-for-step-server* を作成します。

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/05_keypair_02.png
   :width: 600

----

キーペアの作成
================

3 作成したキーペアのダウンロードが自動的に行われます。このファイルを再取得できないので、わかりやすい場所に保存し、なくさないようにしてください。

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/05_keypair_03.png
   :width: 800

----

キーペアの作成
================

4 作成したキーペアの確認

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/05_keypair_04.png
   :width: 800

----


キーペアの作成
================

5 Linux/Macの場合は、鍵の権限設定を行ってください。

sampe command::

  $ chmod 600 key-for-step-server.pem


----


セキュリティグループの作成
================

1 「セキュリティグループの作成」を選択します。

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/06_secgroup_01.png
   :width: 800

----

セキュリティグループの作成
================

2 セキュリティグループ *sg-for-step-server* を作成します。

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/06_secgroup_02.png
   :width: 600

----

セキュリティグループの作成
================

3 セキュリティグループの作成に成功した状態。 *sg-for-step-server* 「ルールの編集」を選択します。

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/06_secgroup_03.png
   :width: 800

----

セキュリティグループの作成
================

4 「ルールの追加」を選択

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/06_secgroup_04.png
   :width: 800

----

セキュリティグループの作成
================

5 ルール： *SSH*  CIDR *0.0.0.0/0* を追加します。

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/06_secgroup_05.png
   :width: 600

----

セキュリティグループの作成
================

6 ルールの追加に成功した状態。

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/06_secgroup_06.png
   :width: 800

----


踏み台サーバーの起動
================

1 「インスタンスの起動」を選択します。

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/07_instance_01.png
   :width: 800

----

踏み台サーバーの起動
================

2 次項のパラメーターを入力

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/07_instance_02.png
   :width: 600

----

踏み台サーバーの起動
================

- アベイラビリティゾーン： *az1*
- インスタンス名： *step-server*
- フレーバー： *standard.xsmall*
- インスタンス数： *1*
- インスタンスのブートソース： *イメージから起動*
- イメージ名： *centos-base*

----


踏み台サーバーの起動
================

3 キーペア *key-for-step-server*  セキュリティグループ： *sg-for-step-server* を選択

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/07_instance_03.png
   :width: 600

----

踏み台サーバーの起動
================

4 選択済みネットワークが *work-net* になっていることを確認。

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/07_instance_04.png
   :width: 600

----

踏み台サーバーの起動
================

5 サーバー起動時に実行するスクリプトを入力。入力内容は次項を参照。

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/07_instance_05.png
   :width: 600

----


踏み台サーバーの起動
================

カスタマイズ・スクリプト::

  ---------ここから---------
  #!/bin/bash
  cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime
  yum install -q -y git
  cd /root
  git clone -q https://github.com/josug-book1-materials/install_cli.git
  cd install_cli && sh install.sh
  cat << EOF > /root/openrc
  # 以下を自分の環境に合わせて値を変えてください。
  export OS_AUTH_URL=http://192.168.253.1:5000/v2.0/
  export OS_REGION_NAME=regionOne
  export OS_TENANT_NAME=okinawaXX
  export OS_USERNAME=studentXX
  export OS_PASSWORD=your-password
  EOF
  echo "##### Userdata script completed #####"
  ---------ここまで---------

環境変数 *OS_XXXX* は、受講者個別の内容に変更が必要です。

----


踏み台サーバーの起動
================

6 起動に成功した状態。

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/07_instance_06.png
   :width: 800

----

踏み台サーバーの起動
================

7 リンク *step-server* を選択すると、起動ログの確認、コンソールへの接続が行えます。

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/07_instance_07.png
   :width: 800

----



Floating IP の割り当て
================

1 仮想サーバーのメニューから「Floating IPの割り当て」を選択します。

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/08_floating_01.png
   :width: 800

----


Floating IP の割り当て
================

2 まずは、「＋」ボタンを選択し、割り当てるFloating IPを、管理者が作成した、 *Ext-Net* から取得します。

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/08_floating_02.png
   :width: 600

----


Floating IP の割り当て
================

3 プール： *Ext-Net* からFloating IPを取得します。

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/08_floating_03.png
   :width: 600

----

Floating IP の割り当て
================

4 確保されたIPアドレスを、 *step-server* へ割り当てます。

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/08_floating_04.png
   :width: 800

----

Floating IP の割り当て
================

5 正常に割り当てられた状態。

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/08_floating_05.png
   :width: 800

----

SSHログイン
================

- 自分の端末から、SSHをクラインと使ってログインします。

  - SSHキーファイル： *key-for-step-server.pem*
  - Floating IP

- 正常に設定が行えていれば、OpenStack用の環境変数ファイルと、各種コマンドが利用できます。

実行例::

  $ ssh -i key-for-step-server.pem root@xxx.xxx.xxx.xxx

  # ls -alF openrc
  -rw-r--r-- 1 root root 171 Dec  8 22:09 openrc

----


SSHログイン
================

- 以下のコマンドが実行出来れいれば正常です。

コマンドの実行::

  # source openrc

  # nova list
  +--------------------------------------+-------------+--------+------------+-------------+--------------------------------------+
  | ID                                   | Name        | Status | Task State | Power State | Networks                             |
  +--------------------------------------+-------------+--------+------------+-------------+--------------------------------------+
  | 703fb862-faa9-44c1-9654-54866e5226a5 | step-server | ACTIVE | -          | Running     | work-net=10.0.0.100, 192.168.253.114 |
  +--------------------------------------+-------------+--------+------------+-------------+--------------------------------------+

----


前半のまとめ
================

- Horizonを使った、サーバー構築の基礎

  - 仮想ルーター
  - 仮想ネットワーク
  - セキュリティグループ
  - カスタマイズ・スクリプト
  - Floating IP

----


後半：シンプルなWEBサービスの構築
================

----


サービスの概要
================

- 踏み台サーバーからCLIを使って、サンプルアプリケーション環境を構築します。
- 以下のサンプルアプリケーションを用いて、OpenStack上にデモサービスを展開していきます。

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/10_sampleapp.png
   :width: 800

----


作業の流れ
================

- アプリケーション用仮想ネットワークの作成
- セキュリティグループの作成
- DBサーバーの構築
- APPサーバーの構築
- WEBサーバーの構築
- 動作確認

----

完成形のイメージ
================

- 作業が完了すると以下の状態になります。

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/10_sampleapp_01.png
   :width: 800

----


仮想ネットワークの作成
================

- 仮想ネットワークを作成していきます。まずは、次のコマンドで、それぞれの仮想ネットワークを定義します。

コマンド実行::

  # neutron net-create dmz-net
  # neutron net-create app-net
  # neutron net-create dbs-net

----

仮想ネットワークの作成
================

- 続いて、作成した仮想ネットワークにサブネットを割り当てて、*dmz-net* を仮想ルーター *Ext-Router* に接続します。

コマンド実行::

  # neutron subnet-create --ip-version 4 --gateway 192.168.0.254 --name dmz-subnet dmz-net 192.168.0.0/24
  # neutron subnet-create --ip-version 4 --no-gateway --name app-subnet app-net 172.16.10.0/24
  # neutron subnet-create --ip-version 4 --no-gateway --name dbs-subnet dbs-net 172.16.20.0/24
  # neutron router-interface-add Ext-Router dmz-subnet

----

セキュリティグループの作成
================

- アプリケーションの通信を許可するセキュリティグループを作成します。

コマンド実行::

  # neutron security-group-create sg-web-from-internet
  # neutron security-group-create sg-all-from-app-net
  # neutron security-group-create sg-all-from-dbs-net
  # neutron security-group-create sg-all-from-console

----


セキュリティグループの作成
================

- ルールを追加します。

コマンド実行::

  # neutron security-group-rule-create --ethertype IPv4 --protocol tcp \
  --port-range-min 80 --port-range-max 80 --remote-ip-prefix 0.0.0.0/0 sg-web-from-internet
  # neutron security-group-rule-create --ethertype IPv4 --protocol tcp \
  --port-range-min 443 --port-range-max 443 --remote-ip-prefix 0.0.0.0/0 sg-web-from-internet

  # neutron security-group-rule-create --ethertype IPv4 --protocol tcp \
  --port-range-min 1 --port-range-max 65535 --remote-ip-prefix 172.16.10.0/24 sg-all-from-app-net
  # neutron security-group-rule-create --ethertype IPv4 --protocol icmp \
  --remote-ip-prefix 172.16.10.0/24 sg-all-from-app-net

- 続く

----


セキュリティグループの作成
================

- 続き

コマンド実行::

  # neutron security-group-rule-create --ethertype IPv4 --protocol tcp \
  --port-range-min 1 --port-range-max 65535 --remote-ip-prefix 172.16.20.0/24 sg-all-from-dbs-net
  # neutron security-group-rule-create --ethertype IPv4 --protocol icmp \
  --remote-ip-prefix 172.16.20.0/24 sg-all-from-dbs-net

  # neutron security-group-rule-create --ethertype IPv4 --protocol tcp \
  --port-range-min 1 --port-range-max 65535 --remote-ip-prefix 10.0.0.0/24 sg-all-from-console
  # neutron security-group-rule-create --ethertype IPv4 --protocol icmp \
  --remote-ip-prefix 10.0.0.0/24 sg-all-from-console

----


キーペアの作成
================

- これからディプロイするサーバーに使うキーペアを準備しておきます。

コマンド実行::

  # cd $HOME
  # nova keypair-add key-for-internal | tee key-for-internal.pem
  # chmod 600 key-for-internal.pem


----

userdata の作成
================

- 先ほど、Horizonから投入したカスタマイズ・スクリプトをファイルとしｔ作成して、サーバー起動時に渡します。まず、ファイルを作成します。
- ファイルの中身は次項に記載します。

コマンド実行::

  # vi userdata_web.txt
  # vi userdata_app.txt
  # vi userdata_dbs.txt


----

userdata の作成
================

userdata_web.txt::

  ---------ここから---------
  #!/bin/bash
  cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime
  cd /root
  git clone -q https://github.com/josug-book1-materials/sample-app.git
  cd sample-app
  git checkout -b v1.0 remotes/origin/v1.0
  sh /root/sample-app/server-setup/install_web.sh
  echo "##### Userdata script completed #####"
  ---------ここまで---------

----

userdata の作成
================

userdata_app.txt::

  ---------ここから---------
  #!/bin/bash
  cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime
  cd /root
  git clone -q https://github.com/josug-book1-materials/sample-app.git
  cd sample-app
  git checkout -b v1.0 remotes/origin/v1.0
  sh /root/sample-app/server-setup/install_rest.sh
  echo "##### Userdata script completed #####"
  ---------ここまで---------

----

userdata の作成
================

userdata_dbs.txt::

  ---------ここから---------
  #!/bin/bash
  cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime
  cd /root
  git clone -q https://github.com/josug-book1-materials/sample-app.git
  cd sample-app
  git checkout -b v1.0 remotes/origin/v1.0
  sh /root/sample-app/server-setup/install_db.sh
  echo "##### Userdata script completed #####"
  ---------ここまで---------

----

サーバー起動準備
================

- ネットワークのuuidを環境変数に格納しておきます。必須の手順ではありませんが、コマンドに対してuuidを直接に記載すると可読性が悪くなるためです。

コマンド実行::

  # function get_uuid () { cat - | grep " id " | awk '{print $4}'; }
  # export MY_DMZ_NET=`neutron net-show dmz-net | get_uuid`
  # export MY_APP_NET=`neutron net-show app-net | get_uuid`
  # export MY_DBS_NET=`neutron net-show dbs-net | get_uuid`

  # env |grep MY_
  MY_DBS_NET=abecabfd-8922-4bf4-a6db-e732b99d847e
  MY_APP_NET=a420a85f-0949-4129-9b51-ffff5d56f64b
  MY_DMZ_NET=8f7ce3a4-c89f-44ef-85d6-9fbe900b4630


----

サーバー起動
================

- 実際にサーバーを起動します。

コマンド実行::

  # nova boot --flavor standard.xsmall --image "centos-base" \
  --key-name key-for-internal --user-data userdata_web.txt \
  --security-groups sg-all-from-console,sg-web-from-internet,sg-all-from-app-net \
  --availability-zone az1 --nic net-id=${MY_DMZ_NET} --nic net-id=${MY_APP_NET} \
  web01

  # nova boot --flavor standard.xsmall --image "centos-base" \
  --key-name key-for-internal --user-data userdata_app.txt \
  --security-groups sg-all-from-console,sg-all-from-app-net,sg-all-from-dbs-net \
  --availability-zone az1 --nic net-id=${MY_DMZ_NET} --nic net-id=${MY_APP_NET} --nic net-id=${MY_DBS_NET} \
  app01

  # nova boot --flavor standard.xsmall --image "centos-base" \
  --key-name key-for-internal --user-data userdata_dbs.txt \
  --security-groups sg-all-from-console,sg-all-from-dbs-net \
  --availability-zone az1 --nic net-id=${MY_DMZ_NET} --nic net-id=${MY_DBS_NET} \
  dbs01


----

サーバー起動の確認
================

- 起動したサーバーの状態を以下のコマンドで確認します。

コマンド実行::

  $ nova console-log --length 30 web01
  $ nova console-log --length 30 app01
  $ nova console-log --length 30 dbs01

- ログインプロンプトが確認できれば、起動は完了しています。

----

アプリケーションの設定
================

- アプリケーションの設定を行います。

  - APPサーバー： 接続先となるDBサーバーのIPを設定する。
  - WEBサーバー： 接続先となるAPPサーバーのIPを設定する。

- 起動したサーバーのIPアドレスを以下のコマンドで確認しておきます。

コマンド実行::

  # nova list
  +--------------------------------------+-------------+--------+------------+-------------+---------------------------------------------------------------+
  | ID                                   | Name        | Status | Task State | Power State | Networks                                                      |
  +--------------------------------------+-------------+--------+------------+-------------+---------------------------------------------------------------+
  | 5f4087e8-30b4-487f-8bd1-c55d6308c4fd | app01       | ACTIVE | -          | Running     | dmz-net=192.168.0.3; app-net=172.16.10.3; dbs-net=172.16.20.3 |
  | 105fc9c9-dde3-4552-9bf9-b6203e028b9a | dbs01       | ACTIVE | -          | Running     | dmz-net=192.168.0.4; dbs-net=172.16.20.1                      |
  | e7b50e85-6c0f-4f10-8d07-a58836e58796 | step-server | ACTIVE | -          | Running     | work-net=10.0.0.5, 15.126.218.215                             |
  | c97d3326-8417-4e83-9b5d-aa1a976d83a5 | web01       | ACTIVE | -          | Running     | dmz-net=192.168.0.1; app-net=172.16.10.1                      |
  +--------------------------------------+-------------+--------+------------+-------------+---------------------------------------------------------------+

----

アプリケーションの設定
================

- APPサーバーへSSHで接続して設定を行います(IPアドレスは読み替えが必要)

APPサーバー::

  # ssh -i key-for-internal.pem root@192.168.0.3
  [root@app01 ~]# vi /root/sample-app/endpoint.conf

endpoint.conf::

  [db-server]
  db_host = 172.16.20.1
  db_endpoint = mysql://user:password@%(db_host)s/sample_bbs?charset=utf8

- *db_host* にDBサーバーの *dbs-net* のアドレスを入力して保存します。

アプリケーションの起動::

  [root@app01 ~]# sh /root/sample-app/server-setup/rest.init.sh start


----

アプリケーションの設定
================

- WEBサーバーへSSHで接続して設定を行います(IPアドレスは読み替えが必要)

WEBサーバー::

  # ssh -i key-for-internal.pem root@192.168.0.1
  [root@web01 ~]# vi /root/sample-app/endpoint.conf

endpoint.conf::

  [rest-server]
  rest_host = 172.16.10.3
  rest_endpoint = http://%(rest_host)s:5555/bbs

- *rest_host* にDBサーバーの *app-net* のアドレスを入力して保存します。

アプリケーションの起動::

  [root@web01 ~]# sh /root/sample-app/server-setup/web.init.sh start

----


Floating IPの割り当てと、動作確認
================

- 外部からのブラウザアクセスを行うために、Floating IPを割り当てます。

コマンド実行::

  # nova floating-ip-create Ext-Net
  +---------------+-----------+----------+---------+
  | Ip            | Server Id | Fixed Ip | Pool    |
  +---------------+-----------+----------+---------+
  | 15.126.244.28 |           | -        | Ext-Net |
  +---------------+-----------+----------+---------+

  # nova floating-ip-associate web01 15.126.244.28

- 自分の端末から、割り当てたIPアドレスへアクセスしてみてください。設定が上手く行っていれば、アプリケーションの画面が確認できるはずです。

----

ここまでの状態
================

- ここまでの作業が終わっていると、以下の状態になっているはずです。

.. image:: https://raw.githubusercontent.com/irixjp/irixjp.github.io/master/20141212_okinawa/_assets/10_sampleapp_02.png
   :width: 600

----

まとめ
================

- CLIを使ったOpenStackの基本操作

  - userdataを流用する事で、何度でも同じ環境が構築可能です。

- マルチネットワーク環境への仮想
- サンプルアプリケーションの実行

----


Ansibleによる高度な自動化へ続く
================
