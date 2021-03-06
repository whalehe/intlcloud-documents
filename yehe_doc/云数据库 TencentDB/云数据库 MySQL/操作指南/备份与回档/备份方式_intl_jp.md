## バックアップ概要
### バックアップ方法
MySQLの高可用バージョンは、**自動バックアップ**と**手動バックアップ**の2種類の方法でデータベースをバックアップします。

### バックアップタイプ
MySQLの高可用バージョンは、2種類のバックアップタイプをサポートしています。
- **物理バックアップ**は、物理データをフルコピーすることです（自動バックアップと手動バックアップの両方はサポート）。
- **論理バックアップ**は、SQL文をバックアップすることです（手動バックアップはサポート）。
>
>- 物理バックアップを使って復元するには、xbstreamを利用して展開する必要があります。詳細については、[物理バックアップでデータベースを復元する](https://intl.cloud.tencent.com/document/product/236/31910)をご参照ください。
>- 単一インスタンスのテーブル数が100万を超えた場合は、バックアップのエラーになる恐れがあり、データベースへの監視にも影響を与えます。そのために、単一インスタンスのテーブル数が100万を超えないようにテーブルの数を適切に管理してください。
>- Memoryエンジンテーブルのデータがメモリに格納されているので、Memoryエンジンテーブルを物理バックアップすることができません。データの紛失を避けるために、MemoryエンジンテーブルをInnoDBテーブルに変換することをお勧めします。

| 物理バックアップのメリット | 論理バックアップのデメリット |
|---------|---------|
| <li>バックアップ速度が速いです。<li>ストリーミングバックアップと圧縮をサポートします。<li>バックアップの成功率が高いです。<li>復元は簡単で効率的です。<li>バックアップとの結合作業、例えば、ROの増やし、災難対策の増加で速度がより速くなります。<li>物理バックアップにかかる平均時間は論理バックアップの1/8程度です。<li>物理バックアップのインポート速度は論理バックアップより10倍ほど早いです。| <li>復元するにはSQLの実行とインデックスの作成が必要なので、かかる時間が長いです。<li>バックアップ速度が遅いです、大量のデータがある場合は特に速度が低下します。<li>バックアッププロセスは、インスタンスに負荷をかけ、マスタースレーブの遅延を大きくする可能性があります。<li>単精度浮動小数点数の精度情報が紛失する可能性があります。<li>各種エラー（エラービューなど）によって、バックアップエラーになる可能性があります。<li>バックアップとの結合作業、例えば、 ROの増加、災難対策の増加で速度が遅くなる可能性があります。 |

### バックアップのオブジェクト
 | データバックアップ | ログバックアップ |
|---------|---------|
 | MySQL 5.5、5.6、5.7（高可用バージョン）：<li>自動バックアップはフル物理バックアップをサポートします。<li>手動バックアップは、フル物理バックアップ、フル論理バックアップ及び単一データベース・単一テーブルの論理バックアップをサポートします。<li>自動バックアップと手動バックアップの両方は圧縮とダウンロードをサポートします。<li>自動バックアップは、手動で削除されませんが、その保持期間が設定できます。<li>手動バックアップは、手動で削除されますが、削除されるまで保持します。 | MySQL 5.5、5.6、5.7（高可用バージョン）：<li>ログファイルはインスタンスのバックアップスペースを占用します。<li>ログファイルはダウンロードをサポートしますが、圧縮をサポートしません。<li>ログファイルの保持期間を設定することが可能です。|

## 注意事項
- MySQLの自動バックアップでは、2019年02月26日より、物理バックアップのみサポートされています。自動バックアップは、デフォルトで物理バックアップに設定され、論理バックアップを提供されなくなりました。既存の自動バックアップが論理バックアップを使用するインスタンスは、次々に自動的に物理バックアップに切り替えられます。
この切り替え作業は、サービスへのアクセスに影響しませんが、自動バックアップを使う習慣のある方に若干の影響を与える可能性があります。論理バックアップを実行したい場合、[ MySQL コンソール](https://console.cloud.tencent.com/cdb)の手動バックアップ方法或いは [API の呼び出し](https://intl.cloud.tencent.com/document/product/236/15844) で論理バックアップを生成します。
- 論理バックアップと物理バックアップを実行する際、ファイルが圧縮処理されるため、ダウンロードすると、一部のファイルが使えない場合があります。その場合、手動論理バックアップで一部のデータベーステーブルのバックアップ機能をもって取り替えることができます。[手動バックアップ](#manual- backup)をご参照ください。
- インスタンスのバックアップファイルはバックアップスペースを使用します。無料のクォータを超えたバックアップスペースに対して追加料金が発生する可能性があるため、バックアップサイクルを適切に設定し、バックアップスペースを適切に使用してください。
- サービス量の少ない時期にバックアップすることをお勧めします。
- 一定の保持期間を過ぎた場合、ファイルが自動的に削除されますので、必要なバックアップファイルをローカルにダウンロードしてください。
- テーブルロックによるバックアップエラーの発生を避けるために、バックアップ中は、DDL操作をしないでください。
- 無料限度額を超えたバックアップスペースは課金されます。課金の詳細については[バックアップスペースの課金説明](https://intl.cloud.tencent.com/document/product/236/32344)をご参照ください。

## MySQLデータの自動バックアップ
1. [MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、インスタンスリストのページでインスタンス名をクリックすると、管理画面に入り、【バックアップで復元する】>【自動バックアップの設定】を選択します。
![](https://main.qcloudimg.com/raw/69fed1aac393a518bd8cc2ad1fea550f.png)
2. ポップアップで表示されているバックアップ設定のダイアログボックスで、各バックアップパラメータを選択し、【OK】をクリックします。パラメータは次のように説明されています。
>[ロールバック機能](https://intl.cloud.tencent.com/document/product/236/7276) バックアップ間隔とバックアップの保持期間内のバックアップファイルに基づき、自動バックアップ頻度と保持日数を減らすとインスタンスデータのロールバック機能に影響を与えるため、バックアップのコンフィグレーションをよく考慮してください。
>
<table>
<thead>
<tr>
<th>パラメータ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr>
<td>バックアップ周期</td>
<td>データの安全性を確保するために、少なくとも１週間に2回バックアップを実行してください。デフォルトは月曜日から日曜日までとします。</td>
</tr>
<tr>
<td>バックアップ時間</td>
<td><ul><li>デフォルトの時間はシステムが自動的に割り当てたバックアップスタート時間です。<li>時間帯をカスタム設定でき、サービスの低いピーク期間に設定することをお勧めします。バックアップ開始時刻は、バックアップ終了時刻ではなく、バックアップがスタートする時刻を表します。<br>例えば、02:00～06:00時を選択した場合、システムは、02:00～06:00の時間帯にある特定の時刻にバックアップをスタートします。具体的なスタート時刻は、バックエンドのバックアップポリシーとバックアップシステム状況に依存します。
</td>
</tr>
<tr>
<td>データバックアップの保持期間</td>
<td>データバックアップファイルは7〜732日保持でき、デフォルト値は7日です。</td>
</tr>
<tr>
<td>ログバックアップの保持期間</td>
<td>ログバックアップファイルは7～732日保持でき、デフォルト値は7日です。<strong>ログバックアップ保持日数の値はデータバックアップ保持日数の値以下である必要があります。</strong>  </td>
</tr>
</tbody></table>

<img src="https://main.qcloudimg.com/raw/a371d4ba960264aa5630b59a3bfe5096.png"  style="margin:0;">


<span id = "manual-backup"></span>
## MySQLデータの手動バックアップ
手動バックアップ機能により、ユーザーは自分でバックアップタスクをスタートすることができます。
>
>- 手動バックアップでは、フル物理バックアップ、フル論理バックアップ及び単一データベース・単一テーブル論理バックアップがサポートされています。
>- 手動バックアップは、スペースの浪費や占用を避けるために、バックアップリストから自動削除され、バックアップスペースを解放することができます。
>- インスタンスは毎日の自動バックアップタスクを実行する期間内に手動バックアップがスタートすることができません。
>
1. インスタンスリストページで、インスタンス名をクリックすると、管理ページに入ります。【バックアップの復元】>【手動バックアップ】タブを選択します。
2. ポップアップで表示されているバックアップ設定ダイアログボックスから、バックアップ方法とオブジェクトを選択して【OK】をクリックします。
![](https://main.qcloudimg.com/raw/a16e644f51756b6a98597945e45329cd.png)
>論理バックアップにおける単一データベース又は単一テーブルのバックアップである場合、左側の【データベーステーブルの選択】でバックアップするデータベース又はデータベースを選択し、データベース又はテーブルを右側のリストに追加します。データベースがない場合は、まずデータベース或いはテーブルを作成してください。
>
![](https://main.qcloudimg.com/raw/76924e2c76ac348b68ed113d679d6907.png)
