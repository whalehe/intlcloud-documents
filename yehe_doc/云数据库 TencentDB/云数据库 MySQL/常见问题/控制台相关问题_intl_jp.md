### クラウドデータベースMySQLの作成にはどのくらい時間がかかりますか。
通常、クラウドデータベースは10分間以内に作成できます。読み取り専用インスタンスの作成時間はマスターインスタンスのデータ量と関係があり、データ量が多いほど、作成時間は長くなります。
この時間を過ぎると、作成過程に問題があるかもしれませんので、すぐに[お問い合わせ](https://intl.cloud.tencent.com/document/product/236/32996)からご連絡ください。

### 購入したデータベースが違っていたときはどのように返却すればよいですか。
[MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、インスタンスリストの「更なる操作」または【その他】>【廃棄/返却】または【廃棄/返却返金】を選択して返品します。詳細は[インスタンスの終了](https://intl.cloud.tencent.com/document/product/236/31895)をご参照ください。

<span id = "shilixiaohui"></span>
### クラウドデータベースMySQLのインスタンスが破損したらどうすればいいですか。
インスタンス返品後、ゴミ箱に一定期間保管します。従量課金インスタンスで1日保管します。この期間内では、ゴミ箱内で対応するインスタンスを探してから元に戻す操作により、戻すことができます。

<span id = "zhanghaomima"></span>
### アカウントを誤って削除してしまい、パスワードも忘れた場合、どうすればいいですか。
- アカウントを誤って削除した場合、[MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、インスタンス名をクリックしてインスタンス管理画面に入り、【データベース管理】>【アカウント管理】>【アカウントの作成】をクリックするか、またはsql言語を使用して新規作成します。詳細は[アカウントの作成](https://intl.cloud.tencent.com/document/product/236/31900)をご参照ください。
- rootパスワードを忘れた場合は、【データベース管理】>【アカウント管理】画面から対応するアカウントを探して【パスワードのリセット】の操作を行います。詳細は[パスワードのリセット](https://intl.cloud.tencent.com/document/product/236/31901)をご参照ください。
以上の操作は[クラウドAPIインターフェイス](https://intl.cloud.tencent.com/document/product/236/17497)でも実現できます。

### クラウドデータベースMySQLの最大接続数はどれくらいです。また、どうやって修正しますか。
クラウドデータベースMySQLの最大接続数はコンソールで調べられます。接続数が多すぎる場合、まず原因を徹底して調べて解決することをお勧めします。接続数を直接増やすことはお勧めしません。
[MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、インスタンス名をクリックしてインスタンス管理画面に入り、【データベース管理】>【パラメータ設定】画面を選択し、`max_connections`パラメータを探して修正できます。


### MySQLインスタンス監視中にmax_connections値がいつも1000を表示して、実際の現在の最大接続数を表示しないのはなぜですか。
インスタンス監視ではmax_connectionsは許可している最大接続数を表示し、カスタマイズすると最大で10240まで値を取ることができます。【現在開いている接続数】は現在時刻の実際の接続数を表示し、リアルタイムで変化する値です。


### ディスク領域の不足はどうすればわかりますか。
クラウドデータベースのディスク領域についてはモニターセンターが監視を行います。クラウドデータベースの使用領域が90%を超えるときは、ショートメッセージやメールによるアラームを作動させ、クラウドモニターで対応するアラーム受信者（設定方法は[アラーム機能](https://intl.cloud.tencent.com/document/product/236/8457)）をご参照ください）を設定するだけで、領域が不足するとアラームで通知されるようになります。


### MySQLを初期化した後、テーブル名の大文字小文字の区別をどうやって修正しますか。
大文字小文字の区別は、調整が必要なデータベースの`lower_case_table_names`のパラメータを調整します。
[MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、インスタンス名をクリックしてインスタンス管理画面に入り、【データベース管理】>【パラメータ設定】画面を選択し、`lower_case_table_names`パラメータを探して修正します。0が区別あり、1が区別無しです。
