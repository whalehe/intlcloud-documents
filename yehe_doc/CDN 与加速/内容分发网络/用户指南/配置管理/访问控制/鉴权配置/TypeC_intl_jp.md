## アルゴリズムの説明
**アクセスURL形式**
`http://DomainName/md5hash/timestamp/FileName`

**アルゴリズムの説明**
- timestamp：UNIX形式の16進数のタイムスタンプです。
- md5hash：MD5（カスタマイズキー+ファイルパス+タイムスタンプ）。

**リクエスト例**
`http://cloud.tencent.com/8fe9b5597c809d7ace147468c7c7eadb/5e577978/test/test.jpg`

>MD5を計算する際に、リクエストパスが`http://cloud.tencent.com/test.jpg`の場合、MD5を計算する際のパスは`/test.jpg`となります。

## 設定ガイド
### パラメータの説明
TypeCに必要な設定は以下のとおりです。
![](https://main.qcloudimg.com/raw/b1fc7e25fa6503cdcd49786e2eda04d3.png)
**認証キーのカスタマイズ：**キーは6～32文字の大文字と小文字および数字で構成されています。キーを大切に保管してください。ユーザー側とサーバー側のみ知っている必要があります。
**有効時間のカスタマイズ：**リクエストのタイムスタンプ値と設定された有効時間を介して、現在の時刻と比較し、リクエストの有効期限が切れているかどうかを判断します。有効期限切れの場合、直接に403エラーを返します。

### オブジェクト
キー、パラメータ名、および有効期間を設定した後、必要に応じて認証オブジェクトを指定でき、以下の3つのモードがサポートされています。
![](https://main.qcloudimg.com/raw/1952a0ac13633a87d4b676e52bf2eb10.png)
+ 指定されたドメイン名配下のすべてのファイルは認証される必要があります。
+ 指定されたタイプのファイルを認証不要に、他のすべてのファイルは認証される必要があります。
+ 指定されたタイプのファイルは認証される必要があります。

## 注意事項
**キャッシュヒット率**
ドメイン名のTypeC認証モードを有効にしている場合、アクセスURLには認証パスが含まれます。CDNノードでリソースをキャッシュする時、認証パスは自動的に無視されるため、キャッシュヒット率には影響しません。
**back to originポリシー**
TypeC認証モードが有効になっているドメイン名のアクセス形式は次のとおりです。
`http://DomainName/md5hash/timestamp/FileName`

認証が成功した後、CDNノードがヒットしない場合は、ノードはback to originリクエストを送信します。**back to originリクエストは、パス中のmd5hashとtimestampパスを削除します**。オリジンサーバーは特別な処理を行う必要はありません。
