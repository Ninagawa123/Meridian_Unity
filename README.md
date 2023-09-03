# Meridian_Unity  
MeridianをUnityで動作させるための簡易デモです。  
※Mac/Winで動作を確認しています。Winではファイアーウォールの設定が必要です。  
  
Meridianの詳細については下記をご参照ください。  
[Meridian_info](https://ninagawa123.github.io/Meridian_info/) ...基本情報  
[Meridian_TWIN](https://github.com/Ninagawa123/Meridian_TWIN) ...高機能版のボード情報  
[Meridian LITE](https://github.com/Ninagawa123/Meridian_LITE) ...簡易版のボード情報  
  
#  UnityHubに登録して起動する  
フォルダ「Unity_demo」の中のMeridian_unity_demo_20220704.zipを解凍します。  
UnityHubを開き、ProjectsのADDで解凍済みの「Meridian_unity_demo_20220704」フォルダを指定します。  
UnityHubに登録されたらプロジェクトを起動します。（Unityのバージョンは2020.3.25f1(LTS)です。） 
  
#  UnityのスクリプトのIPアドレスを書き換える
画面下の「Project」→「Assets」→「Script」よりUdp_handler_sendをダブルクリックして開きます（VScodeなどが立ち上がります）  
スクリプト9行目のconst string HOST = "192.168.1.xx"; にESP32DevKitCのIPアドレスを記入し、セーブします。

#  ESP32のIPアドレスを書き換える
これまでの手順で設定済みの場合はそのままでOKです。
Meridian_core_for_ESP32_PathThrough.inoの93行目にUnityを使うPCのIPアドレスを入力します。

### Windowsの場合はファイアーウォールを設定する
Windowsスタートメニュー→「設定」→「更新とセキュリティ」→「Windowsセキュリティ」→「ファイアーウォールとネットワーク保護」→「詳細設定」→「受信の規則」の一覧から「Unity 2020.3.25f1 Editor」の「パブリック」となっているものを選択しダブルクリック。「接続を許可する」にチェックを入れOKする。

###  UnityとMeridianボードを起動する  
<img width="713" alt="SS 985" src="https://github.com/Ninagawa123/Meridian_Unity/assets/8329123/f9d9acb3-04d4-448b-be3d-c8904458f31e">  
  
Unityを起動した後、「SampleScene」をダブルクリックし、再生ボタンを押します。  
Meridianボードを通信が成立していればロボットの関節にシンクロして画面の中のモデルが動きます。  
  
画面の「Send」にチェックを入れるとUnityからロボットを操作することができます。  
スライドバーに対応したサーボが動きます。またスライドバーの上のテキストボックスに直接数値を入力することができます。  
数値の単位はdegreeとなります。  
  
「Action」にチェックを入れるとUnityからロボットにサンプルのモーションを送信します。  
左半身の各関節角度をsinカーブで増減させます。  
このモーションはParamMaster.csの160行目-167行目で設定しているので、適宜書き換えてお試しください。  
