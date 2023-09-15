# Meridian_Unity  
MeridianをUnityで動作させるための簡易デモです.  
※Mac/Winで動作を確認しています. Winではファイアーウォールの設定が必要です.   
  
Meridianの詳細については下記をご参照ください.  
[Meridian_info](https://ninagawa123.github.io/Meridian_info/) ...基本情報  
[Meridian_TWIN](https://github.com/Ninagawa123/Meridian_TWIN) ...高機能版のボード情報  
[Meridian LITE](https://github.com/Ninagawa123/Meridian_LITE) ...簡易版のボード情報  
  
#  UnityHubに登録して起動する  
フォルダ「Meridian_Unity_demo1」の中のMeridian_unity_demo_20220704.zipを解凍します.   
UnityHubを開き, ProjectsのADDで解凍済みの「Meridian_unity_demo_20220704」フォルダを指定します.   
UnityHubに登録されたらプロジェクトを起動します.（Unityのバージョンは2020.3.25f1(LTS)です） 
  
#  UnityのスクリプトのIPアドレスを書き換える
画面下の「Project」→「Assets」→「Script」よりUdp_handler_sendをダブルクリックして開きます.（VScodeなどが立ち上がります）  
スクリプト9行目のconst string HOST = "192.168.1.xx"; にESP32DevKitCのIPアドレスを記入し, セーブします. 

#  ESP32のIPアドレスを書き換える
これまでの手順で設定済みの場合はそのままでOKです.  
Meridian_TWINもしくはMeridian_LITEのESP32用ファイルのconfig.hに, Unityを使うPCのIPアドレスを入力します.  
  
### Windowsの場合はファイアーウォールを設定する
Windowsスタートメニュー→「設定」→「更新とセキュリティ」→「Windowsセキュリティ」→「ファイアーウォールとネットワーク保護」→「詳細設定」→「受信の規則」の一覧から「Unity 2020.3.25f1 Editor」の「パブリック」となっているものを選択しダブルクリック.「接続を許可する」にチェックを入れOKします. 

###  UnityとMeridianボードを起動する  
<img width="713" alt="SS 985" src="https://github.com/Ninagawa123/Meridian_Unity/assets/8329123/f9d9acb3-04d4-448b-be3d-c8904458f31e">  
  
Unityを起動した後, 「SampleScene」をダブルクリックし, 再生ボタンを押します.    
Meridianボードと通信が成立していればロボットの関節にシンクロして画面の中のモデルが動きます.   
  
画面の「Send」にチェックを入れるとUnityからロボットを操作することができます.   
スライドバーに対応したサーボが動きます。またスライドバーの上のテキストボックスに直接数値を入力することができます.   
数値の単位はdegreeとなります.  
  
「Action」にチェックを入れるとUnityからロボットにサンプルのモーションを送信します.  
左半身の各関節角度をsinカーブで増減させます.  
このモーションはParamMaster.csの160行目-167行目で設定しているので, 適宜書き換えてお試しください.  

###  トラブルシューティング  
うまく接続できない場合, ESP32をテストモードに設定することで, ESP32単体とUnityの接続の確立のみに問題を絞ることができます.  
[Meridian LITE](https://github.com/Ninagawa123/Meridian_LITE) を以下のように改定し, ESP32に書き込みます.  
- config.h内 #define ESP32_STDALONE 1 としてテストモードを有効にする.  
- keys.hにWifi設定も書き込む. この時, 接続先が2.4GHz帯となるように注意する.  
また, 当UnityファイルのUDP_SendHandler.csのConst String Host = ""にESP32のIPアドレスが正しく書き込まれているか確認してください.  
  
ESP32はMeridian Boardに挿す必要はなく、ESP32DevkitC単体で試すことができます。  
ESP32に電源が供給され, かつUnityの再生ボタンが押された状態となれば接続が完了します.  
<img width="600" alt="SS 1071" src="https://github.com/Ninagawa123/Meridian_Unity/assets/8329123/bf4f53e0-c676-4926-af17-b79a60cd3c8b">  
接続が成功すると, ESP32側からL0番のサーボに+-30度のダミーデータが送信され, 首を左右に振るような動きになります. 機体の向きは画面に背を向けた状態になります.  
