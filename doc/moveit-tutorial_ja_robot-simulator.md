
# ロボットシミュレータを使う

シミュレータ上のロボットを動かしてみます．  
本チュートリアルでは下記のロボットのシミュレータの利用方法を紹介します．

- NEXTAGE OPEN
- Baxter Research Robot
- MINAS TRA1


## シミュレータの種類

本チュートリアルで扱うシミュレータには次のような種類があります．

- ROS のシミュレータ
  - NEXTAGE OPEN / Baxter Research Robot / MINAS
    - MoveIt! シミュレータ : 運動学のみの動作計画シミュレータ
    - Gazebo シミュレータ : 動力学を含む環境・物理シミュレータ
- hrpsys(RTM) シミュレータ
  - NEXTAGE OPEN のみ
    - 動力学を含む物理シミュレータ

本チュートリアルではどのシミュレータを使っても最終的には
動作計画ソフトウェアの MoveIt! を起動してその動作計画機能を利用します．


## ソフトウェアのインストール

次のソフトウェアのインストールをします．

- ROS とチュートリアルパッケージ
- ロボットソフトウェア
  - NEXTAGE OPEN ソフトウェア
  - Baxter ソフトウェア
  - MINAS TRA1 ソフトウェア

ロボットソフトウェアは全てインストールしても，どれか1つでも大丈夫です．  
また，システム構成は次のとおりです．

<$ifeq <$ROS_DISTRO>|indigo>

- Ubuntu 14.04
- ROS Indigo

<$endif>

<$ifeq <$ROS_DISTRO>|kinetic>

- Ubuntu 16.04
- ROS Kinetic

<$endif>


### ROS のインストール

ターミナルから次のコマンドを実行して
[ROS ソフトウェアをインストール](http://wiki.ros.org/<$ROS_DISTRO>/Installation/Ubuntu)
します．
既に ROS がインストールされていれば，次のチュートリアルパッケージのインストールに進んでください．

<$ifeq <$ROS_DISTRO>|indigo>

```
$ sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu trusty main" > /etc/apt/sources.list.d/ros-latest.list'
$ sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net --recv-key0xB01FA116
$ sudo apt-get update
$ sudo apt-get install ros-indigo-desktop-full
```

<$endif>

<$ifeq <$ROS_DISTRO>|kinetic>

```
$ sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116
sudo apt-get update
sudo apt-get install ros-kinetic-desktop-full
```

<$endif>

- 参考 :
  - [Ubuntu install of ROS <$ROS_DISTRO>](http://wiki.ros.org/<$ROS_DISTRO>/Installation/Ubuntu)
  - [ROS <$ROS_DISTRO> の Ubuntu へのインストール](http://wiki.ros.org/ja/<$ROS_DISTRO>/Installation/Ubuntu)


### チュートリアルパッケージのインストール

ターミナルから次のコマンドを実行して
チュートリアルパッケージのソフトウェアをインストールします．

```
$ sudo apt-get install ros-<$ROS_DISTRO>-tork-moveit-tutorial
```


### NEXTAGE OPEN ソフトウェアのインストール

ターミナルから次のコマンドを実行して
NEXTAGE OPEN のソフトウェアをインストールします．

```
$ sudo apt-get update && sudo apt-get install ros-<$ROS_DISTRO>-rtmros-nextage ros-<$ROS_DISTRO>-rtmros-hironx
```


### Baxter ソフトウェアのインストール

ターミナルから次のコマンドを実行して
Baxter Research Robot のソフトウェアをインストールします．

<$ifeq <$ROS_DISTRO>|indigo>

```
$ sudo apt-get update
$ sudo apt-get install git-core python-argparse python-wstool python-vcstools python-rosdep ros-<$ROS_DISTRO>-control-msgs ros-<$ROS_DISTRO>-joystick-drivers
$ sudo apt-get install ros-<$ROS_DISTRO>-baxter-sdk ros-<$ROS_DISTRO>-baxter-moveit-config
$ sudo apt-get install gazebo2 ros-<$ROS_DISTRO>-qt-build ros-<$ROS_DISTRO>-driver-common ros-<$ROS_DISTRO>-gazebo-ros-control ros-<$ROS_DISTRO>-gazebo-ros-pkgs ros-<$ROS_DISTRO>-ros-control ros-<$ROS_DISTRO>-control-toolbox ros-<$ROS_DISTRO>-realtime-tools ros-<$ROS_DISTRO>-ros-controllers ros-<$ROS_DISTRO>-xacro python-wstool ros-<$ROS_DISTRO>-tf-conversions ros-<$ROS_DISTRO>-kdl-parser
$ sudo apt-get install ros-<$ROS_DISTRO>-baxter-simulator
```

　インストール方法については以下の公式ページにも説明があるので参照ください．このページから該当部分をコピーペーストすると上記のコマンドを打たなくても良くなります．
 - [http://sdk.rethinkrobotics.com/wiki/Workstation_Setup](http://sdk.rethinkrobotics.com/wiki/Workstation_Setup)
 - [http://sdk.rethinkrobotics.com/wiki/Simulator_Installation](http://sdk.rethinkrobotics.com/wiki/Simulator_Installation)

<$endif>

<$ifeq <$ROS_DISTRO>|kinetic>

```
$ sudo apt-get update
$ sudo apt-get install git-core python-argparse python-wstool python-vcstools python-rosdep ros-kinetic-control-msgs ros-kinetic-joystick-drivers
$ sudo apt-get install ros-kinetic-baxter-sdk ros-kinetic-baxter-moveit-config
$ sudo apt-get install gazebo7 ros-kinetic-qt-build ros-kinetic-gazebo-ros-control ros-kinetic-gazebo-ros-pkgs ros-kinetic-ros-control ros-kinetic-control-toolbox ros-kinetic-realtime-tools ros-kinetic-ros-controllers ros-kinetic-xacro python-wstool ros-kinetic-tf-conversions ros-kinetic-kdl-parser
$ sudo apt-get install ros-kinetic-baxter-simulator
```

<$endif>


### MINAS TRA1 シミュレータのインストール

ターミナルから次のコマンドを実行して
MINAS TRA1 のソフトウェアをインストールします．

```
$ sudo apt-get update && sudo apt-get install ros-<$ROS_DISTRO>-minas
```


### インストールの最後に

インストールの最後に setup.bash を読み込み，ROS の環境を設定します．

```
$ source /opt/ros/<$ROS_DISTRO>/setup.bash
```

これは新しくターミナルを立ち上げて ROS を使用する前に毎回必要になります．
下記のように .bashrc ファイルに設定を加えて
ターミナル起動時に setup.bash を自動で実行し ROS 環境になるようにしておくと便利です．

```
$ echo "source /opt/ros/<$ROS_DISTRO>/setup.bash" >> ~/.bashrc
```

- 注意: 上記コマンドの `>>` を `>` にしてしまうと元々あった .bashrc 内の設定が消えてしまうので気をつけてください．

.bashrc の設定ができていると以後のターミナルを起動するたびに行う
`source /opt/ros/<$ROS_DISTRO>/setup.bash` は不要です．


## シミュレータと MoveIt! の起動

<a id="start-nextage-hrpsys-simulator"></a>
### <a href="#start-nextage-hrpsys-simulator">NEXTAGE OPEN - hrpsys シミュレータ</a>

#### hrpsys シミュレータ・MoveIt! などの起動

NEXTAGE OPEN の動力学シミュレータの一つである
NEXTAGE OPEN hrpsys(RTM) シミュレータを起動します．
ターミナルを開いて次のコマンドを実行してください．

```
$ source /opt/ros/<$ROS_DISTRO>/setup.bash
$ rtmlaunch nextage_moveit_config nextage_demo.launch
```

コマンドを実行すると次の4つのウィンドウが開きます．

- ターミナル
- hrpsys シミュレータ (hrpsys viewer)
- MoveIt! / RViz
- Hironx Dashboard (Command Panel for Hironx / NEXTAGE Open)

![NextageROS_Demo - Starts](images/nextageros-demo_starts.png)

これで MoveIt! の動作計画機能が利用できる状態になっています．

#### シミュレータの終了

シミュレータを終了するには全体を起動したターミナル上で
Ctrl-C を入力すると全体が終了します．

<a id="start-nextage-gazebo-simulator"></a>
### <a href="#start-nextage-gazebo-simulator">NEXTAGE OPEN - Gazebo シミュレータ</a>

NEXTAGE OPEN のもうひとつの動力学シミュレータは
ROS の動力学環境シミュレータ Gazebo 上で動きます．

ターミナルを2つ開きます．

#### Gazebo シミュレータの起動

1つ目のターミナルで次のコマンドを入力しして
NEXTAGE OPEN Gazebo シミュレータを起動します．

**ターミナル-1** : Gazebo シミュレータの起動
```
$ source /opt/ros/<$ROS_DISTRO>/setup.bash
$ roslaunch nextage_gazebo nextage_world.launch
:
:
[go_initial-6] process has finished cleanly
log file: /home/robotuser/.ros/log/5d4ac8aa-baeb-11e7-af06-001c4284b313/go_initial-6*.log
:
```

Gazebo が起動して上記のターミナルの出力が得られたら Gazebo シミュレータ内の
NEXTAGE OPEN ロボットの準備が完了しています．

![NEXTAGE - Gazebo Starts](images/nextage_gazebo-starts.png)

- 注意: 最初にgazeboを立ち上げる際にはモデルデータをダウンロードするために
  以下のようにWarningやErrorが表示され数秒から数分の時間がかかる場合が有ります．
  「[トラブルシューティング (Gazebo を起動してもロボットが表示されない)](moveit-tutorial_ja_trouble-shooting.md#gazebo-start-not-show-robot)」もご参照ください．

![Gazebo Initial Error](images/gazebo_startup_error.png)

#### MoveIt! の起動

2つ目のターミナルで次のコマンドを入力して MoveIt! を起動します．

**ターミナル-2** : MoveIt! の起動
```
$ source /opt/ros/<$ROS_DISTRO>/setup.bash
$ roslaunch nextage_moveit_config moveit_planning_execution.launch
```

![NEXTAGE - MoveIt! Starts](images/nextage_moveit-starts.png)

これで MoveIt! の動作計画機能が利用できる状態になっています．

#### シミュレータの終了

シミュレータを終了するには各ターミナルで Ctrl-C を入力してください．


### Baxter Research Robot - Gazebo シミュレータ

#### Gazebo シミュレータの起動

ターミナルを3つ開きます．

**ターミナル-1** : Baxter シミュレータの起動
```
$ source /opt/ros/<$ROS_DISTRO>/setup.bash
$ roslaunch baxter_gazebo baxter_world.launch  
```

![Baxter Simulator - Starts](images/baxter-simulator_starts.png)

しばらくすると次のようなメッセージが **ターミナル-1** に表示されます．

```
[ INFO] [1509004453.402952141, 10.130000000]: Simulator is loaded and started successfully
[ INFO] [1509004453.462744480, 10.140000000]: Robot is disabled
[ INFO] [1509004453.462870807, 10.140000000]: Gravity compensation was turned off
```

これで Gazebo シミュレータの準備は終了です．

#### ロボットの準備

次にロボットを MoveIt! から操作可能な状態にします．
2つ目のターミナル上で次のコマンドを実行してください．

**ターミナル-2** : ロボットの準備
```
$ source /opt/ros/<$ROS_DISTRO>/setup.bash
$ rosrun baxter_tools enable_robot.py -e

[INFO] [WallTime: 1509004993.657452] [192.385000] Robot Enabled

$ rosrun baxter_tools tuck_arms.py -u

[INFO] [WallTime: 1509005020.475291] [0.000000] Untucking arms
[INFO] [WallTime: 1509005020.910480] [202.807000] Moving head to neutral position
[INFO] [WallTime: 1509005020.911446] [202.808000] Untucking: Arms already Untucked; Moving to neutral position.
[INFO] [WallTime: 1509005024.476011] [204.036000] Finished tuck

$ rosrun baxter_interface joint_trajectory_action_server.py

Initializing node...
Initializing joint trajectory action server...
Running. Ctrl-c to quit
```

![Baxter Simulator - Ready for MoveIt!](images/baxter-simulator_ready-for-moveit.png)

これでロボットの準備は終了です．

#### MoveIt! の起動

3つ目のターミナルで次のコマンドを実行して MoveIt! を起動します．

**ターミナル-3** : MoveIt! の起動
```
$ source /opt/ros/<$ROS_DISTRO>/setup.bash
$ roslaunch baxter_moveit_config baxter_grippers.launch
```

![Baxter MoveIt! - Starts](images/baxter-moveIt_starts.png)

これで MoveIt! の動作計画機能が利用できる状態になっています．


#### シミュレータの終了

シミュレータでの作業が終わりましたら
全てのターミナルで Ctrl-C を入力することでシミュレータを終了します．


### MINAS TRA1 - MoveIt! シミュレータ

ターミナルを2つ起動します．

1つ目のターミナルでコントローラをシミュレーションモードで起動します．

**ターミナル-1**
```
$ source /opt/ros/<$ROS_DISTRO>/setup.bash
$ roslaunch tra1_bringup tra1_bringup.launch simulation:=true
```

2つ目のターミナルで MoveIt! を起動します．

**ターミナル-2**
```
$ source /opt/ros/<$ROS_DISTRO>/setup.bash
$ roslaunch tra1_bringup tra1_moveit.launch
```

![MINAS TRA1 - MoveIt! Starts](images/minas-tra1_moveit_starts.png)

シミュレータを終了するには各ターミナルで Ctrl-C を入力してください．


### MoveIt! GUI での動作計画

MoveIt! の動作計画機能を GUI から利用してみます．

MoveIt! / RViz (GUI) 上に表示されているロボットのエンドエフェクタのところに
水色の球や赤緑青(RGB)の矢印マークが表示されています．
これは InteractiveMarker と呼ばれるもので
MoveIt! の GUI でのマニピュレータ操作を行うためのものです．

InteractiveMarker の球や矢印をマウスなどでドラッグ操作を行うと
オレンジ色のマニピュレータがそのドラッグ操作に追従して動きます．
これが目標姿勢となります．
そこで MotionPlanning 子ウィンドウ内の Planning タブ内の
` Plan and Execute` ボタンをクリックするとその目標姿勢に向かって
MoveIt! が動作計画を行い，シミュレータのロボットが動作します．

動作計画だけを行いたい場合は `Plan` ボタンをクリックします．

![MoveIt! - RViz Plan and Execute](images/nextage_moveit_plan-execute.png)

このように MoveIt! の GUI 上で
InteractiveMarker を動かして目標値を設定し，動作計画を行い実行する
という操作は基本的にどのロボットでも共通です．


<!-- EOF -->
