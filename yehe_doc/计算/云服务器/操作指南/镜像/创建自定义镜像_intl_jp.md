## 操作シナオリ

イメージを作成する時、パブリックイメージでインスタンスを起動し、またこのイメージをインスタンスに接続して、ソフトウェア環境を自分でデプロイします。インスタンスが正常に実行されている場合、実際のニーズに応じてこのインスタンスをベースにして、新しいカスタムイメージを作成できます。新しいカスタムイメージを作成した後、そのイメージを利用して、元のインスタンスと同じカスタム設定を持つ新しいインスタンスを起動できます。

> 
> - カスタムイメージを作成する同時に、システムはデフォルトで関連するスナップショットが作成されます。このスナップショットを削除する前に、関連するイメージを削除する必要があります。現在のスナップショットはすでに商品化されているため、カスタムイメージを保持すると、一定のスナップショット費用が発生します。スナップショット課金ポリシーについては、[スナップショットの商品化に関するお知らせ](https://intl.cloud.tencent.com/document/product/362/32413)をご参照ください。
> - 2018年7月以降にパブリックイメージに基づいて作成されたCVMでは、イメージのオンライン作成がサポートされています（つまり、インスタンスをシャットダウンせずにイメージを作成できます）。
> - その他のインスタンスがカスタムイメージを作成する前に、このインスタンスをシャットダウンしてください。これにより、イメージが現在のインスタンスと同じデプロイ環境を持つようにします。

## 注意事項

- 各リージョンは、最大10個のカスタムイメージをサポートします。
- 以下のディレクトリ/ファイルがクリアされます：
 - /var/log/  
 - /root/.bash_history、/home/ubuntu/.bash_history（Ubuntu システム）
- Linuxインスタンスがカスタムイメージを作成する時、/etc/fstabにデータディスク構成が含まれていないことを確認してください。そうしないと、このイメージで作成されたインスタンスが正常に起動しなくなります。カスタムイメージを作成するLinuxインスタンスにデータディスクがマウントされている場合、/etc/ fstab内に設定されたデータディスクの関連設定をコメント化または削除する必要があります。
- 作成プロセスは10分以上かかりますが、具体的な時間はインスタンスのデータサイズによって異なります。業務への影響を避けるためには、事前に関連準備を行ってください。

## 操作手順

### コンソールを介してインスタンスからカスタムイメージを作成

1. [CVMコンソール](https://console.cloud.tencent.com/cvm)にログインします。
2. インスタンスの管理画面で、イメージを作成するインスタンスを選択し、【その他】>【インスタンス状態】>【シャットダウン】をクリックします。
3. インスタンスがシャットダウンされた後、このインスタンス行で、【詳細】>【イメージの作成】をクリックします。
4. ポップアップの「カスタムイメージの作成」ウィンドウで、「イメージ名」と「イメージ説明」を入力し、【イメージの作成】をクリックして作成します。
> コンソールの右上にある <img src="https://main.qcloudimg.com/raw/31b31c7b27848f0378932f17273feff3.png" style="margin: 0;"></img>をクリックし、イメージ作成の進行状況を確認します。
>
5. イメージが作成された後、左側のナビゲーションメニューバーで、【[イメージ](https://console.cloud.tencent.com/cvm/image)】をクリックし、イメージの管理画面に入ります。
6. イメージリストで、作成したイメージを選択し、【インスタンスの作成】をクリックし、前のイメージと同じイメージのサーバーを購入できます。

### APIを使用してカスタムイメージを作成

CreateImageインターフェースを利用しカスタムイメージを作成することができます。詳細については、[CreateImage API](https://intl.cloud.tencent.com/document/product/213/33276)をご参照ください。

## ベストプラクティス

### データディスク上のデータ移行

新しいインスタンスを起動する同時に、元のインスタンスのデータディスクのデータを保持する必要がある場合、まずデータディスクの[スナップショット](https://intl.cloud.tencent.com/document/product/362/31638)を取得してから、このデータディスクのスナップショットを使用して新しいCBSデータディスクを作成できます。
詳細情報については、[スナップショットを使用してクラウドディスクの作成](https://intl.cloud.tencent.com/document/product/362/5757)をご参照ください。




