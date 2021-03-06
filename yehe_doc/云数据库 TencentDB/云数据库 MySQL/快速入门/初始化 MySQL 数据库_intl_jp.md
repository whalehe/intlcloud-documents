この文書では、ユーザがMySQLを簡単に使用するよう、MySQLデータベースを初期化するための完全手順を提供します。

## 前提条件
1. Tencent Cloudのアカウントを登録し、実名認証を完了させます。
Tencent Cloudのアカウントを登録しようとする場合：
<div style="background-color:#00A4FF; width: 470px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">ここをクリックしてTencent Cloudのアカウントを登録します</a></div>
実名認証を行うには：
<div style="background-color:#00A4FF; width: 370px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">ここをクリックして実名認証を行います</a></div>
2. MySQLを購入しました。
MySQLを購入するには：
<div style="background-color:#00A4FF; width: 400px; height: 35px; line-height:35px; text-align:center;"><a href="https://buy.cloud.tencent.com/cdb" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn3">ここをクリックして購入ページに進みます</a></div>

##　操作手順
1. [MySQL コンソール](https://console.cloud.tencent.com/cdb)にログインし、左側ナビゲーションから【インスタンスリスト】タブを選択します。
2. ステータスが【未初期化】のMySQLインスタンスを選択し、「操作」列で【初期化】をクリックします。
![](https://main.qcloudimg.com/raw/945a4e69bef68eb706a520d4cbac13cf.png)
3. 表示された初期化ダイアログで、初期化関連パラメータを設定し、【OK】をクリックして初期化を実行します。
 - **文字セットのサポート**：LATIN1、GBK、UTF8、UTF8MB4文字セットがサポートされます。デフォルトの文字セットはLATIN1（ISO- 8859- 1）コード・セットです。インスタンスを初期化した後、コンソールのインスタンス詳細ページで文字セットを変更することもできます。
 - **テーブル名の大文字と小文字の区別**：テーブル名の大文字と小文字が区別されるか。デフォルトはyesです。
 - **カスタムポート*：データベースのアクセスポート。デフォルトは3306です。
 - **rootアカウントのパスワードの設定**：新規作成された MySQL データベースのユーザ名はデフォルトで rootです。ここでは、root アカウントのパスワードを設定します。
 - **パスワードの確認**：パスワードを再入力します。
4. インスタンスリストに戻り、ターゲットであるMySQLインスタンスのステータスが【実行中】になると、初期化に成功したことを示しています。


## 次の手順
- Windows又はLinuxのCVMを使用して、それぞれパブリック・プライベートネットワークでMySQLにアクセスする方法については、[MySQLデータベースへのアクセス](https://intl.cloud.tencent.com/document/product/236/3130)をご参照ください。
- コンソールの【インスタンスリスト】ページ及び【インスタンス管理】ページで、インスタンスに関する情報、インスタンスの監視及びデータベース管理などを確認します。詳細については、[MySQLデータベース管理](https://intl.cloud.tencent.com/document/product/236/3131)をご参照ください。
