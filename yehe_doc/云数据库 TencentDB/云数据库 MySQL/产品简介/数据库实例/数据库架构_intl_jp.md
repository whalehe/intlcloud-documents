MySQLは高可用版、金融版、単ノード高IO版、基本版の4つのアーキテクチャをサポートしています。現在、金融版へのアップグレードは高可用版のみです。

<span id = "gaokeyongban"></span>
## 高可用版
高可用版は1マスター1スレーブの高可用性モードを採用し、リアルタイムのホットバックアップ機能を備え、サーバーダウンの自動検出及び自動フェイルオーバーを提供します。ゲーム、インターネット、モノのインターネット、電子商取引、物流、保険、証券などの業界のアプリケーションをカバーします。
特徴は次の通りです。
- マスター／スレーブのレプリケーションは非同期（デフォルト）と半同期の2つの方法があります。レプリケーション方式は[コンソール](https://console.cloud.tencent.com/cdb)のインスタンス詳細ページで変更できます。コンソールで金融版にアップグレードすることもできます（1マスター2スレーブの同期モード）。
- 読取専用インスタンス、災害復旧インスタンス、セキュリティグループ、データマイグレーション、Multi- AZの配置など、さまざまな機能をサポートしています。詳細については、[製品の優位性](https://intl.cloud.tencent.com/document/product/236/5148)をご参照ください。
- 高可用版のインスタンスの可用性は99.95%に達します。プロトコルの詳細については [サービスレベル契約](https://intl.cloud.tencent.com/document/product/301/30977)をご参照ください。
- データノードは強力なハードウェアに配置され、基盤となるストレージにローカルのNVMe SSDディスクを使用することで、IOPSが最大240000（実際のIOPSレートは構成、ページサイズ及び業務負荷に依存します。この値は、参考として、MySQLのデフォルト16KBのページサイズのテストに基づいて得られたものです）の高いIOパフォーマンスを提供します。

アーキテクチャは次の通りです。
![Alt text](https://main.qcloudimg.com/raw/baf6c165620f79a5dd5f56b6a02d9eb0.svg)


<span id = "jrb"></span>
## 金融版
>従来の1マスター2スレーブ（強い同期のレプリケーション方式）の高可用版から金融版に名前が変更され、既存の1マスター2スレーブのインスタンスのコンソールバージョンに表示が更新されます。
>
金融版は1マスター2スレーブ3ノードのアーキテクチャを採用しており、強い同期のレプリケーション方式をサポートしています。リアルタイムのホットバックアップにより、データの高一貫性が確保され、金融レベルの信頼性と高可用性が実現されています。
- マスター／スレーブのレプリケーション方式：強い同期。
- 読取専用インスタンス、災害復旧インスタンス、セキュリティグループ、データマイグレーション、Multi- AZの配置など、さまざまな機能をサポートしています。詳細については、[製品の優位性](https://intl.cloud.tencent.com/document/product/236/5148)をご参照ください。
- 金融版のインスタンスの可用性は99.99%に達します。プロトコルの詳細については [サービスレベル契約](https://intl.cloud.tencent.com/document/product/301/30977)をご参照ください。
- データノードは強力なハードウェアに配置され、基盤となるストレージにローカルのNVMe SSDディスクを使用することで、IOPSが最大240000（実際のIOPSレートは構成、ページサイズ及び業務負荷に依存します。この値は、参考として、MySQLのデフォルト16KBのページサイズのテストに基づいて得られたものです）の高いIOパフォーマンスを提供します。

アーキテクチャは次の通りです。
![Alt text](https://main.qcloudimg.com/raw/09f1ed1756fd1b7e533a5bbe4c937b0b.png)



<span id = "danjiedian"></span>
## 単ノード高IOバージョン
単ノード高IO版は1つの物理ノードを使用して配置し、コスト・パフォーマンスに優れています。基盤となるストレージはローカルのNVMe SSDディスクを使用することで、高いIOパフォーマンスを提供します。現在、読取専用インスタンスに適用されており、サービスの読取負荷を分散することに有利となり、リード・ライト分離が必要な各業界のアプリケーションに適しています。

アーキテクチャは次の通りです。
![Alt text](https://main.qcloudimg.com/raw/9c18abaf213f5b2c66f36e538eb86273.svg)
>
>- 単ノードの配置はシングルポイントリスクが存在します。単一の読取専用インスタンスのみを購入した場合には、サービスの高可用性は保証されません。単一の読取専用インスタンスに障害が発生すると、サービスの中断が発生することで、お客様に影響が及ぶ可能性があります。
>- 単一の読取専用インスタンスのリカバリ時間はサービスのデータ量によって異なり、保証されません。このため、可用性を必要とするサービス[ROグループ](https://intl.cloud.tencent.com/document/product/236/11361)内に少なくとも2つの読取専用インスタンスを購入して可用性を保証することをお勧めします。


<span id = "jichuban"></span>
## 基本版
基本版は単ノードを使用して配置するものであり、安価でコスト・パフォーマンスが高い。特徴は次の通りです。
- 計算とストレージを分離するようにします。計算ノードに障害が発生した場合には、ノードを交換することで迅速なリカバリを実現します。基盤となるデータはクラウドストレージのトリプル・コピーを使用して保存し、データの信頼性が確保されており、ディスクの障害は、ディスクのスナップショットモードで迅速に復旧できます。
- 基本版はデータベースへの接続、アクセス、リソースなど、様々な側面から20ぐらいの監視項目を提供し、相応の警告ポリシーを設定することで、CVMの自社構築よりも手間がかからないと同時に、CVMと比較して40%のコスト削減を実現する価格優位があります。基本版のノードはクラウドサーバ上に配置されており、ユーザーが自ら構築することよりも優れたデータベースパフォーマンスを提供します。
- MySQL基本版の基盤となるストレージメディアは90%のI/Oシーンに適した高性能クラウドストレージを使用しており、優れた品質、安価、安定したパフォーマンスです。具体的なIOPSの計算式は{min 1500+8*容量、max 4500}となります。

アーキテクチャは次の通りです。
![Alt text](https://main.qcloudimg.com/raw/2293e213a7908bd8de95fa21c141c9eb.svg)

>
>- 基本版は個人学習、ミニWebサイト、非コアの小規模企業システム及び中規模から大規模の企業の開発テスト環境向けに設計されたものであり、正式なサービス環境では推奨されません。
>- MySQL基本版は単ノードアーキテクチャであるため、このノードに障害が発生した場合、CVMの障害回復よりもわずかに長い時間がかかります（インスタンスの起動とデータの復元が含まれます）。高可用性を必要とするサービスでは、MySQLの高可用版又は金融版のインスタンスを使用することをお勧めします。


