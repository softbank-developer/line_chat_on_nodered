## 概要
IBM BluemixのNode-RED上でIBM Watson NLCを使ったFAQ自動応答LINE用BOTを動作させることができます。  
また、このアプリケーションで使うNLCに対してNode-REDの画面上からCSVデータを使って学習させることができます。  


## 利用条件
- **Bluemix account** を持っていること(IBM Watson NLC、Node-RED用)
- **LINE@への登録及びWebhooksの設定** が完了していること

## 利用開始手順
1. IBM Bluemixで、Node-RED Starterを作成  
アプリ名、ホスト名、プランを任意で設定し作成します。  
※作成には5分程度かかることがあります。

2. Node-REDにIBM Watson NLCを接続  
接続タブから「新規に接続」を選択して、新規にNLCを作成するか、「既存に接続」を選択して既存のNLCを選択します。

3. Node-REDの初期設定  
Node-REDのアプリURLにアクセスし、画面の指示に従ってエディタ画面で使うユーザ名、パスワードなどを設定します。

4. 「node-red-contrib-linebot」を追加
フローエディタ画面右上のメニューから「パレットの管理」をクリックし、「ノードを追加」タブで「node-red-contrib-linebot」を検索し、「node-red-contrib-linebot」の「ノードを追加」ボタンをクリックします。

5. フローの読み込み  
フローエディタ画面右上のメニューから「読み込み」->「クリップボード」とクリックし、テキストエリアに「aistarter_nodered_linebot.json」の内容をコピーし、貼り付けます。

6. Cloudantバインド設定の反映  
全てのタブのCloudantノードをダブルクリックし、「Service」に「Node-REDのアプリ名+cloudantNoSQLDB」が表示されることを確認し、「完了」ボタンをクリックします。  
「完了」ボタンをクリックすると、Cloudantノードの右上に青い丸がつきます。  
![cloudant_node](https://github.com/softbank-developer/line_chat_on_nodered/blob/master/readme_images/cloudant_node.png)


7. デプロイ  
フローエディタ画面右上の「デプロイ」ボタンをクリックします。

8. 分類器を作成-1  
「NLC学習の実行」タブの「学習データ」ノードにNLCの学習データ形式のデータをセットします。  

9. デプロイ  
フローエディタ画面右上の「デプロイ」ボタンをクリックします。

10. 分類器を作成-2  
「NLC学習の実行」タブの「質問データをセットしてClick」ノードの左に付いているボタンをクリックします。  
デバッグタブに出力された情報の中からclassifier_idをメモします。

11. 分類器IDの設定  
NLCの学習が完了したら「LINE連携」タブの「NLC Request」ノードにメモしたclassifier_idを設定し、「完了」ボタンをクリックします。

12. LINE設定  
「LINE連携」タブの「Reply Message」ノードにLINEのChannel Access TokenとChannel Secretを設定し、「完了」ボタンをクリックします。  
「CallBack」ノードのURLにLINEのWebhook URLを設定し、「完了」ボタンをクリックします。  
※Node-RED側の設定値を「/callback」とした場合、LINE側の設定値は、「[Node-REDのアプリURL]/callback」となります。

13. 回答登録・Index作成-1  
「回答データベース作成」タブの「回答データをここにコピペ」ノードに「学習データで使ったclass_name(重複なし),回答文,URL(任意)」をセットします。  

13. デプロイ  
フローエディタ画面右上の「デプロイ」ボタンをクリックします。

14. 回答登録・Index作成-2  
「回答登録」ノードの左に付いているボタンをクリックします。  
「Index作成」ノードの左に付いているボタンをクリックします。  
※デバッグタブに「0」と表示されれば正常に登録処理が完了しています。


## 使い方
連携したLINEアカウントに向けてテキストメッセージを送信します。  


## ライセンス

[MIT](https://github.com/softbank-developer/line_chat_on_nodered/blob/master/LICENSE)
