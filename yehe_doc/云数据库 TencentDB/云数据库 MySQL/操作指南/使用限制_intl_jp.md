## データ量制限
リソースの有限性から、ユーザーの性能に影響しないように、クラウドデータベースMySQLは各種タイプのMySQLインスタンスにデータ量制限を設けました。以下、大量のデータ数におけるMySQLの単一インスタンスおよび単一テーブルの使用による影響について技術的な角度からご紹介します。

**大量データインスタンス**：クラウドデータベースのデフォルトストレージエンジンはInnoDBです。インスタンスのデータおよびインデックスページがいずれもInnoDBのcache、bufferにキャッシュされるとき、MySQLインスタンスは大規模な同時アクセスをサポートできます。インスタンスのデータ量が多すぎる場合、cache、bufferのデータが頻繁に出し入れされて、MySQLのボトルネックが即座にIOに転送され、アクセス処理量が大幅に低下します（例：あるクラウドデータベースインスタンスは本来8000回／秒のアクセスをサポートできる、データ量がcache、bufferの大きさの倍になると、700回／秒前後のアクセスしかサポートできなくなる）。


**大量データテーブル**：単一データ量が多くなると、単一テーブルリソースへのMySQLは管理コスト（データ、インデックスなど）が変更され、テーブルの処理効率に直接影響します。例えば、1つのタスクテーブル（InnoDB）データ量が5GBに達してからは、操作レイテンシーの更新は明らかに増大します。タスクの反応時間に直接影響し、そうなった場合、分割したテーブルをマイグレーションしてこの問題を緩和するしかなくなります。


>単一インスタンスのテーブル数量が100万個を超過すると、バックアップ、監視、アップグレードに失敗することがあります。同時にデータベースの監視にも影響します。テーブル数を適切に規定し、単一インスタンステーブル数が100万個を超えないよう制御してください。

## 接続数の制限
MySQLの接続数の上限はMySQLのシステム変数max_connectionsで指定されます。MySQLインスタンス接続数がmax_connectionsを超えると、新しい接続はできなくなります。
クラウドデータベースのデフォルトでの接続数は[コンソール](https://console.cloud.tencent.com/cdb)のパラメータ設定画面で確認できます。ユーザーはニーズに応じてmax_connectionsの値を自分で調整できます。しかし、接続数が増えれば、システムリソースは消費されていきます。接続数が実際のシステムの負荷許容能力の範囲を超えると、システムサービスの質に必ず影響します。
max_connectionsについては[MySQL公式ドキュメント](https://dev.mysql.com/doc/)をご参照ください。

## クラウドデータベースとMySQLクライアント端末の接続制限
CVMシステムに付属したMySQLクライアント端末とlibライブラリを使用して、クラウドデータベースインスタンスに接続することをお勧めします。

### スロークエリについての説明
- Linux CVMを使用する開発者は、クラウドデータベースのエクスポートツールからスロークエリログを取得することができます。 [バックアップファイルとログのダウンロード](https://intl.cloud.tencent.com/document/product/236/31910)をご参照ください。
- Windows CVMを使用する開発者は、現在一時的に、スロークエリログを直接取得できません。必要な場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category)し弊社に連絡のうえスロークエリログファイルを取得してください。

### クラウドデータベースのbinlog保存期間の説明
クラウドデータベースMySQL binlogログファイルは7日～732日まで保存できます。デフォルトでは7日です（自動バックアップ設定で日数を設定できます）。ログバックアップ日数はデータバックアップ日数以下でなければいけません。 
binlogは保存時間が長すぎるか、または増加が速すぎると、バックアップ領域が大きくなり、バックアップ領域がシステムが割り当てた領域を一旦超えてしまうと、追加のバックアップ領域費用が生じることがあります。

### 文字セットの説明
クラウドデータベースとMySQLデータベースは同じで、デフォルト文字セットコードフォーマットはLATIN1、つまりISO-8859-1コードフォーマットです。
クラウドデータベースはデフォルト文字コードの設定をサポートしますが、テーブル作成時にはテーブルのコードを明確に指定し、接続時には接続コードを指定することをお勧めします。そうすることで、アプリケーションの移植性がより良くなります。
MySQL文字セットの関連リソースについては[MySQL公式ドキュメント](https://dev.mysql.com/doc/)をご参照ください。

以下はクラウドデータベースの文字セットを修正する方法です。
1. 以下のステートメントでクラウドデータインスタンスのデフォルト文字セットのコードを修正できます。
```
SET @@global.character_set_client = utf8;
SET @@global.character_set_results = utf8;
SET @@global.character_set_connection = utf8;
SET @@global.character_set_server = utf8;
```
ステートメントの実行後、このうちの @@global.character_set_server 等は10分前後でこのマシンのファイルを自動で同期し、恒久化し（また、3つの変数がこのマシンのファイルを同期することはありません）、マイグレーションまたは再起動によって設定後の値を保存します。
2. 以下のステートメントを実行することで現在接続している文字セットコードを修正できます。
```
SET @@session.character_set_client = utf8;
SET @@session.character_set_results = utf8;
SET @@session.character_set_connection = utf8;
```
または
```
SET names utf8;
```
3. PHPプログラムについて、以下の関数によって現在接続する文字コードを設定できます。
```
bool mysqli::set_charset(string charset);
```
または
```
bool mysqli_set_charset(mysqli link, string charset);
```
4. Javaプログラムについては、以下の方式によって現在接続している文字コードを設定できます。
```
jdbc:mysql://localhost:3306/dbname?useUnicode=true&characterEncoding=UTF-8
```

### 操作制限
1. MySQLインスタンスが有するアカウント情報と権限は修正しないでください。修正すると、一部のクラスターサービスが失効してしまうことがあります。
2. データベースとテーブルを作成するときは、InnoDBエンジンを統一して使用することをお勧めします。この選択によって、高アクセスサポートの能力面でインスタンスのパフォーマンスが良くなります。
3. master-slaveの関係を修正、停止しないでください。この操作をした場合、ホットスタンバイを失効させる恐れがあります。

### データベースのテーブル名の制限
中国語によるテーブル名はサポートしていません。テーブル作成時には注意してください。中国語によるテーブル名の場合、ロールバック、アップグレードなどのフローが失敗することがあります。

## 注意事項
### データベースアカウントの権限
クラウドデータベースMySQLはユーザーにインスタンスsuper userの権限を再び与えることはありません。super user権限が必要になって、初めて修正するパラメータは[コンソール](https://console.cloud.tencent.com/cdb)パラメータの設定機能および[チケット提出](https://console.cloud.tencent.com/workorder/category)の2種類の方式で修正できます。


### ネットワークの選択
VPCを使用することをお勧めします。VPCネットワークではネットワークセグメントのパーティション、IPアドレスおよびパスポリシーをカスタマイズすることができます。基本ネットワークに比べると、VPCはネットワークのカスタマイズ設定ニーズに対し、よりよく対応しています。VPCおよび基本ネットワークの比較については[ネットワークの管理](https://intl.cloud.tencent.com/document/product/215/31807)をご参照ください。

