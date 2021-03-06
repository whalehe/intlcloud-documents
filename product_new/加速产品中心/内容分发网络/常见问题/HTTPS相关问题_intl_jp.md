### HTTPSとは？
HTTPSとは、ハイパーテキスト転送セキュリティプロトコル（Hypertext Transfer Protocol Secure）のことです。HTTPプロトコルに基づいて暗号化されたセキュリティプロトコルを転送し、データ送信のセキュリティを効果的に保証できます。HTTPSを設定する場合、ネットワーク全体でデータの暗号化転送機能を実現するために、ユーザーは、ドメイン名に対応する証明書を提供し、ネットワーク全体のCDNノードにデプロイする必要があります。

### CDNはHTTPS構成をサポートしますか？
Tencent Cloud CDNは現在、HTTPS構成を全面的にサポートしています。ユーザーはお持ちの証明書をアップロードしてデプロイするか、[証明書管理コンソール](https://console.cloud.tencent.com/ssl)にアクセスしてTrustAsiaが無料で提供するサードパーティの証明書を申請することができます。

### HTTPS証明書はどう構成しますか？
CDNコンソールでHTTPS証明書を構成することができます。詳細については、[HTTPS設定](https://intl.cloud.tencent.com/document/product/228/6295)を参照してください。

### オリジンサーバーのHTTPS証明書が更新されましたが、CDNは同期に更新する必要がありますか？
ユーザーのback to origin方式に依存します。
HTTPback to origin：必要ではありません。
HTTPS back to origin：オリジンサーバーの証明書が更新された場合、CDNノードも同期的に更新する必要があります。クライアントからノード、ノードからオリジンサーバーへの証明書は一致する必要があります。そうでないと、back to originが失敗することがあります。

### CDNはユーザーにHTTPSのみのアクセスを許可し、HTTPのアクセスを禁止するように制御する方法がありますか？
強制HTTPS機能を使用します。証明書の構成が完了する後、「強制リダイレクト」スイッチが表示されますが、有効にすると、ユーザーがHTTPリクエストを開始しても、HTTPSに強制的にリダイレクトしてアクセスします。
![](https://main.qcloudimg.com/raw/0352df67305e2e7f4c6df51b0b1afc09.png)
