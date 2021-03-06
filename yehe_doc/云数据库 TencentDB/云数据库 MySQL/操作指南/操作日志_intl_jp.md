## 操作シナリオ
指定時間を超過したSQL言語の照会を「スロークエリ」といいます。対応言語は「スロークエリ言語」といい、データベース管理員（DBA）はスロークエリ言語を分析し、スロークエリが生じた原因を探し出す過程を「スロークエリ分析」といいます。

クラウドデータベースMySQLの高可用性バージョンと単一ノードHigh IOバージョンのインスタンスはログ操作管理機能を提供し、故障箇所の迅速な特定をサポートします。コンソールの操作ログ画面で、インスタンスのスローログの詳細、エラーログの詳細、ロールバックログ、およびスローログのダウンロードを確認することができます。
コマンドラインインターフェース（CLI）、またはクラウドデータベースAPIを使用して、データベースログを確認、ダウンロードすることもできます。[バックアップログの確認](https://intl.cloud.tencent.com/document/product/236/15842)および[バイナリログの確認](https://intl.cloud.tencent.com/document/product/236/15843)をご参照ください。

#### MySQLスロークエリ関連の説明
- long_query_time：スロークエリの閾値パラメータで、精度はマイクロ秒クラスまででき、デフォルトは10sです。SQL言語の実行時間がこの数値を超過すると、スローログが記録されます。 
long_query_timeパラメータを調整すれば、元のスローログに影響することはありません。例えば、スローログの閾値パラメータが10sであれば、10sを超過したスローログの記録を報告し、その後続けて1sに調整します。元々報告していたログはそのまま表示されます。
- log_queries_not_using_indexes：未使用のインデックスの照会を記録するかどうかについて、デフォルトはOFFです。


## 操作手順
1. [クラウドデータベースMySQLコンソール](https://console.cloud.tencent.com/cdb)にログインします。
2. インスタンスリストでインスタンス名または操作列の【管理】をクリックし、インスタンス管理画面に進みます。
3. 【操作ログ】画面で、インスタンスのスローログの詳細、エラーログの詳細、ロールバックログ、およびスローログのダウンロードを選択し確認できます。
<table>
<thead>
<tr>
<th>機能項目</th>
<th>説明</th>
</tr>
</thead>
<tbody><tr>
<td>スローログの詳細</td>
<td>1か月以内のデータベースで実行時間が10sを超過したSQL言語を記録</td>
</tr>
<tr>
<td>スローログのダウンロード</td>
<td>スローログのダウンロードの提供</td>
</tr>
<tr>
<td>エラーログの詳細</td>
<td>データベースの動作によるエラーログを記録</td>
</tr>
<tr>
<td>ロールバックログ</td>
<td>ロールバックタスクの運行状態と進捗の記録</td>
</tr>
</tbody></table>

4. 【スローログのダウンロード】画面で操作列の【ダウンロード】をクリックしてスローログをダウンロードできます。
5. ポップアップのダイアログボックスで【ローカルダウンロード】をクリックして直接ダウンロードできます。ダウンロードアドレスを選択、コピーして、このクラウドデータベースと同じVPC下のLinux CVMにログインし、wgetコマンドを運用してダウンロードすることもできます。
>?
>- wgetコマンドフォーマット：wget -c 'ログファイルダウンロードアドレス' -O カスタマイズファイル名.log
>作成例は次のとおりです。
```
wget -c 'http://szx.dl.cdb.tencentyun.com:303/cfdee?appid=1210&time=1591&sign=aIGM%3D' -O test.log
```
>- ログのサイズが0KBの場合、ダウンロードはできません。

