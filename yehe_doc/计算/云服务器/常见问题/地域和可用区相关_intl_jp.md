### リージョンリストはどのように表示しますか。

次の方法で表示できます。
- [リージョンとアベイラビリティーゾーン](https://intl.cloud.tencent.com/document/product/213/6091) ドキュメントを表示します。
- API インターフェースを使用してリージョンとアベイラビリティーゾーンを表示します。
 - [リージョンリストの表示](https://intl.cloud.tencent.com/document/product/213/15708)
 - [アベイラビリティーゾーンリストの表示](https://intl.cloud.tencent.com/document/product/213/35071)


### CVMには何のリージョンおよびアベイラビリティーゾーンがありますか。選択方法は何ですか。

利用可能なCVMリージョンとアベイラビリティーゾーンの詳細については、[リージョンとアベイラビリティーゾーン]（https://intl.cloud.tencent.com/document/product/213/6091）をご参照ください。
リージョンとアベイラビリティーゾーンを選択する方法の詳細については、[リージョンとアベイラビリティーゾーンの選択方法](https://intl.cloud.tencent.com/document/product/213/6091#.E5.A6.82.E4.BD.95.E9.80.89.E6.8B.A9.E5.9C.B0.E5.9F.9F.E5.92.8C.E5.8F.AF.E7.94.A8.E5.8C.BA)をご参照ください。


### 購入したCVMのリージョンを変更できますか。

購入したCVMのリージョンを変更できません。リージョンとアベイラビリティーゾーンを変更する必要がある場合は、次の２つの対処方法をご参考ください。
- 先に[インスタンスを終了](https://intl.cloud.tencent.com/document/product/213/4930)してから、インスタントを再度購入します。

- 元のインスタンスを使用してカスタムイメージを作成します。次に、カスタムイメージを使用して新しいアベイラビリティーゾーンにインスタンスを作成し、インスタンスを起動し、新しいインスタンスの構成を更新します。
  1. 現在のインスタンスのカスタムイメージを作成するには、[カスタムイメージの作成](https://intl.cloud.tencent.com/document/product/213/4942) をご参照ください。
  2. 現在のインスタンスのネットワーク環境が [Virtual Private Cloud](https://intl.cloud.tencent.com/document/product/213/5227) であり、インスタンスが新しいアベイラビリティーゾーンに移行された後にプライベートIPアドレスを保持する必要がある場合は、まず現在のアベイラビリティーゾーンのサブネットを削除し、元のサブネットと同じIPアドレス範囲で新しいアベイラビリティーゾーンにサブネットを作成します。
  > 削除されたサブネットに利用可能なインスタンスが含まれている場合、まず現在のサブネットの全てのインスタンスを新しいサブネットに移行してから削除する必要があります。
  >
  3. 新規作成したカスタムイメージを使用して、新しいアベイラビリティーゾーンに新しいインスタンスを作成します。
  ユーザーは、元のインスタンスと同じインスタンスタイプと構成を選択するか、新しいインスタンスタイプと構成も選択できます。詳細については、[インスタンスの作成](https://intl.cloud.tencent.com/document/product/213/4855)をご参照ください。
  4. 元のインスタンスにElastic パブリックIP アドレスが関連付けられている場合は、元のインスタンスとの関連付けを解除し、新しいインスタンスに関連付けます。詳細については、 [EIP](https://intl.cloud.tencent.com/document/product/213/5733)をご参照ください。
  5. （オプション）元のインスタンスが [従量課金](https://intl.cloud.tencent.com/document/product/213/2180) タイプの場合、元のインスタンスを廃棄することができます。詳細については、 [インスタンスの廃棄](https://intl.cloud.tencent.com/zh/document/product/213/4930) をご参照ください。

### Tencent Cloudの中国国内ユーザーは、他の国や地域のリソースを購入して、中国国内リソースと同じ製品品質とサービスを享受できますか。　
はい。Tencent Cloud中国語サイトは、すべてのユーザーに同じ品質の製品とサービスを提供します。購入地域が異なっても、Tencent Cloud中国語サイトでご利用できるサービスと権益には影響しません。

### カスタムイメージのコピー機能を使用して、中国国内のCVMを他の国または地域に移行できますか。
いいえ。イメージは同じ国または地域内でのみコピーできます。異なる国の間でイメージをコピーする必要がある場合、[チケットを提出](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1)して申請してください。　　　

### 中国内外のインスタンスの違いは何ですか。どの国またはリージョンが自分に適しているかは、どのように判断しますか。
他の国または地域のインスタンスは中国本土以外のリージョンにデプロイされています。中国本土以外のユーザーにとって、地理的および市場上の明らかな利点があります。高速のローカルネットワーク接続を提供し、グローバル顧客の需要に対応でき、他の国または地域でサービスを展開するユーザーにより適しています。　

サポートするリージョンの詳細については、[リージョンとアベイラビリティーゾーン](https://intl.cloud.tencent.com/document/product/213/6091) をご参照ください。

### 中国本土以外のリージョンで購入したインスタンスは、LinuxとWindowsシステムを置き換えられますか。
どの地域のCVMも同じタイプのオペレーティングシステム（OS）の再インストールをサポートしています。（つまり、LinuxをLinuxに再インストールしたり、WindowsをWindowsに再インストールしたりします）
中国本土のCVMインスタンスのみが、異なるタイプのOSの再インストールをサポートしています。（つまり、LinuxをWindowsに再インストールしたり、WindowsをLinuxに再インストールしたります）

### 中国本土以外のリージョンで製品のアフターサービスを受けるにはどうすればよいですか。
Tencent Cloudの公式ウェブサイトで購入した場合は、Tencent Cloudの24時間365日の公式サービスホットライン（95716）にお問い合わせいただくか、[チケットを送信](https://console.cloud.tencent.com/workorder/category)してください。

### 中国以外の地域にCVMインスタンスをデプロイするにはどうすればよいですか。
中国国外リージョンのインスタンスと中国国内リージョンのインスタンスは、リージョンのみが違います。同じタイプのOSを使用している場合、同じ展開方法を採用します。

### 中国本土リージョンのインスタンスを中国本土以外のリージョンに移行できますか。
インスタンスのリージョンとアベイラビリティーゾーンは変更できません。他の国や地域でインスタンスを使用する必要がある場合は、インスタンスを再購入する必要があります。

### 一部のインスタンス仕様は中国でのみ購入でき、中国国外では購入できないのはなぜですか。
一部の地域では、一部のインスタンス仕様がサポートされていない場合があります。[CVM購入ページ](http://manage.qcloud.com/shoppingcart/shop.php?tab=cvm&_ga=1.78908498.770173325.1571651505) に移動して、インスタンスの購入可能状況をご確認できます。

### 中国本土以外のリージョンのインスタンスを使用してウェブサイトを構築した場合、ユーザーはドメイン名を介してウェブサイトにアクセスします。このドメイン名はICP登録が必要ですか。
中国本土のリージョンのウェブサイトの場合、ドメイン名にはICPファイリング番号を取得する必要があります。他の国や地域のウェブサイトの場合、ドメイン名は ICP ファイリング番号を取得する必要がありません。詳細については、[ICP登録の概要](https://intl.cloud.tencent.com/document/product/1022/30453)をご参照ください。

### インスタンスの価格はリージョンにより異なりますか。
インスタンスを購入する場合、インスタンスの価格にはインスタンスの仕様、ストレージ、ネットワーク帯域幅などが含まれます。リージョンによって、上記の価格が異なる場合があるため、インスタンスの価格も異なります。
価格情報の詳細については、[価格設定センター]（https://buy.cloud.tencent.com/price/cvm/calculator）をご参照ください。



