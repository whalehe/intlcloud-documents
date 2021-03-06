[コンソール](https://console.cloud.tencent.com/autoscaling/config)を開き、ナビゲーションバーの【スケーリンググループ】を選択します。

### a.エリアの選択

コンソールの上に作成したい地域を選択します。エリアを選択すると、手動で追加できるCVMとバインディングできるCLBが制限されます。例えば、起動構成のエリアは広州を選択すれば、スケーリンググループに自動的に追加されるのは広州のCVMです。エリアは広州であるスケーリンググループの中に、上海、北京、香港、トロントなど他のエリアのCVMを手動で追加することができなく、上海、北京、香港、トロントなど他のエリアのCLBもバインディングできません。

![](https://mc.qcloudimg.com/static/img/fc2af25ac2023adb97f427aa68b72ff4/image.jpg)

### b.カスタム情報
「新規作成」ボタンをクリックして、スケーリンググループの属性をカスタムします。

  - **スケーリンググループ名称**：このスケーリンググループをマークするために使用されます。例えば「Webサイト論理層」など
  - **最小スケーリンググループ**：スケーリンググループにある最小のインスタンス数を指定します
  - **開始インスタンス数**：スケーリンググループは開始するとき**自動**的に作成されたインスタンス数を指定します。スケーリンググループが作成された後、対応する数量のインスタンスが生成されます
  - **最大スケーリング数**：スケーリンググループにある最大のインスタンス数を指定します
  - **起動構成**：作成された起動構成を指定します。拡張するとき、起動構成に従って拡張CVMが作成されます
  - **サポートするネットワーク**：選択するのは拡張されたCVMのネットワーク属性です。つまり拡張されたCVMが基本ネットワークにあるかVPCにあるかを選択します。クラスタがすでにVPCを使用していない限り、通常は「基本ネットワーク」を選択します
  - **サポートするAvailability Zone**：自動拡張したCVMがどのAvailability Zoneで作成するか指定します。複数のAvailability Zoneを選択でき、自動拡張したCVMはランダムで選択したAvailability Zoneから作成され、Availability Zone間の災害復旧効果を実現します
  - **除去ポリシー**：スケーリンググループがインスタンスを削減したい、且つ複数の選択肢がある場合は、除去ポリシーに基づいて除去するCVMを選択します。一般的に「最も古いCVMを除去する」を選択します。2種類のポリシーについては、[詳細](https://cloud.tencent.com/document/product/377/4166#13.-.E4.BC.B8.E7.BC.A9.E7.BB.84.E7.A7.BB.E5.87.BA.E7.AD.96.E7.95.A5.E7.9A.84.E5.85.B7.E4.BD.93.E8.A7.84.E5.88.99.E6.98.AF.E4.BB.80.E4.B9.88.EF.BC.9F)を確認してください。
  - **CLB**：1つのCLBを指定します。拡張したCVMは自動で当該CLBにマウントされます。

スケーリンググループは作成完了です。この時点では、スケーリンググループはCVMに対応できますが、スマートで拡張と圧縮することができません。次に、以下の3つの操作を続けることを強くお勧めします。
 - 既存のCVMに追加します
 - スケーリングポリシーを作成します
 - 通知を作成します

