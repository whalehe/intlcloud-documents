
## 課金概要

Tencent Cloudが提供しているネットワークタイプのキャリアアクセスはBGPマルチ回線であり、回線の品質を保証します。
現在はトラフィックによる課金および帯域幅による課金のネットワーク課金モードのみを提供しています。
>! 
> - 現在、パブリックネットワークは帯域幅/トラフィックに応じて費用を決済します。その中で、発信帯域幅とはCVMからパブリックネットワークに転送する帯域幅のことを指します。例えば、ユーザーはクライアントを使用して、CVMインスタンスの内部リソースをダウンロードします。
> - 突発的なトラフィックによる高い費用が発生することを防ぐために、帯域幅の上限を指定して、トラフィックを制限できます。この上限を超えると、デフォルトでパッケージロスすると同時に、費用はかかりません。
> 


## 課金モード

>? この製品のサブスクリプションモデルは内部テスト中で、価格ドキュメントはご参考までにご利用くださいませ、最終価格は請求書をご覧ください。必要に応じて、[営業担当者にお問い合わせください]( https://intl.cloud.tencent.com/contact-sales )。

支払モードおよび課金サイクルの違いによる、課金モードの比較は以下のようになります：

- トラフィック（GB）に応じて使用量をカウントします：

 <table class="comparison-table">
                     <tbody><tr>
                        <th>課金モード</th>
                        <th >支払タイプ</th>
                                    <th >課金サイクル</th>
<th >使用ユースケース</th>
                     </tr>
                     <tr>
                        <td><a href="#1">トラフィックに応じて</a></td>
                        <td>  後払い</td> 
                                    <td>  時間毎に決済</td>
                                    <td>業務トラフィックのピーク値が異なる時間帯で変動が大きいユースケースに適用する。</td></tr> </tbody></table>

- 帯域幅（Mbps）に応じて使用料をカウントします：

 <table class="comparison-table">
                     <tbody><tr>
                        <th >課金モード</th>
                        <th >支払タイプ</th>
                                    <th >課金サイクル</th>
<th >使用ユースケース</th>
                     </tr>
                                     <tr>
                        <td><a href="#3">帯域幅サブスクリプション(月額課金)</a></td>
                        <td>  前払い</td> 
                                    <td>  月締め決済</td>
                                    <td>業務トラフィックのピーク値が異なる時間帯で比較的穏やかで、かつ長期使用するユースケースに適用する。</td></tr>
                                    <tr>
                        <td><a href="#4">Bandwidth Package</a></td>
                        <td>  後払い</td> 
                                    <td>  月締め決済</td>
                                    <td>大規模業務に適用し、かつパブリックネットワークの異なるインスタンスの間でトラフィックのピークシフトができるユースケースに使用します。</td></tr></tbody></table>


- トラフィックによる課金および帯域幅による課金の帯域幅のピーク値は意味がやや異なるので、以下の通り具体的に区別します。
<table>
       <tbody><tr>
            <th>トラフィックによる課金   </th>
            <th>帯域幅による課金</th>
       </tr>
       <tr>          
            <td>帯域幅ピーク値は帯域幅の<strong>最高上限</strong>ピーク値にすぎず、承諾の指標にはなりません。帯域幅リソースの争奪 が生じたときは、帯域幅のピーク値は制限を受けることになります。</td> 
            <td>帯域幅のピーク値は承諾の指標になります。帯域幅リソースの争奪が生じたとき、帯域幅のピーク値は保証され、制限を受けることはありません。</td>
            </tr> 
</tbody></table>


> ?換算ルール：1GB = 1000MB、1 MB = 1000 KB、1Gbps = 1000Mbps、1Mbps = 1000Kbps。
> 

<span id = "1"></span>
### トラフィックに応じて

使用するパブリックネットワークのトラフィック課金を基に、支払モードは後払いとし、時間毎に1回決済します。業務トラフィックのピーク値が異なる時間帯で変動が大きなユースケースに適用します。

#### 課金価格

<table>
<thead>
<tr>
<th>リージョン</th>
<th>価格（単位：米ドル/GB）</th>
</tr>
</thead>
<tbody><tr>
<td>中国大陸（香港、マカオ、台湾リージョンは含まず）、ソウル、中国香港</td>
<td>0.12</td>
</tr>
<tr>
<td>シンガポール</td>
<td>0.081</td>
</tr>
<tr>
<td>フランクフルト、トロント、シリコンバレー</td>
<td>0.077</td>
</tr>
<tr>
<td>モスクワ、東京</td>
<td>0.13</td>
</tr>
<tr>
<td>バージニア</td>
<td>0.075</td>
</tr>
<tr>
<td>バンコク、ムンバイ</td>
<td>0.1</td>
</tr>
</tbody></table>

#### 課金事例

帯域幅上シフトのあるユーザーがシンガポールリージョンのEIPを購入した場合は、トラフィックによる課金モデルを選択します。このユーザーは07:00:00 - 07:59:59の間にCVMをバインディングし、かつ使用したトラフィックの合計が10GBの場合は次のようになります。07:00:00 - 07:59:59に発生した費用：0.12元/GB × 10GB = 1.2米ドル

> ?パブリックネットワークのトラフィックは、下りバイト数のカウントを基に得たトラフィックデータで、アプリケーション層のデータです。実際のネットワーク転送では、発生したネットワークトラフィックは実質的なアプリケーション層トラフィックより5%～15%多くなければなりません。このため、Tencent Cloudがカウントしたトラフィックはユーザーがサーバーで自らカウントされるトラフィックよりも10%前後多くなることがあります。
>
> - TCP/IPヘッダーの消費：TCP/IPプロトコルに基づくHTTPリクエストでは、各パケットのサイズは最大1500バイトであり、TCPとIPプロトコルの40バイトのヘッダーが含まれます。ヘッダー部分にトラフィックが発生しますが、アプリケーション層にカウントされません。この部分のオーバーヘッドは約3%です。
> - TCP再送信：通常のネットワーク転送中、送信されるネットワークパケットは3%～10%ぐらいがインターネットによって廃棄されます。サーバーは廃棄された部分を再送信しますが、アプリケーション層はこの部分にかかったトラフィックをカウントできません。比率は約3%～7%です。


<span id = "3"></span>
### 帯域幅サブスクリプション(月額課金)

ニーズに応じて事前に固定帯域幅を購入する場合、支払モードは前払いになります。業務トラフィックのピーク値が異なる時間帯で比較的に穏やかでかつ長期使用するユースケースに適用します。

>? この機能は内部テスト中で、使用する必要がある場合は、[ビジネス照会](https://intl.cloud.tencent.com/contact-sales)をご参照ください。

#### 課金価格

<table>
<thead>
<tr>
<th rowspan="2" width="10%">リージョン</th>
<th colspan="3"  style="text-align:center;">価格（単位：米ドル/Mbps/月）</th>
</tr>
<tr>
<th>≤ 2Mbpsの部分</th>
<th>2Mbps＜帯域幅 ≤ 5Mbpsの部分 </th>
<th>＞5Mbpsの部分</th>
</tr>
</thead>
<tbody><tr>
<td>広州<br>上海<br>北京<br>中国香港<br>シンガポール   </td>
<td>2.86   </td>
<td>3.57</td>
<td>12.86</td>
</tr>
<tr>
<td >成都<br>重慶  </td>
<td>2.57</td>
<td>3.15</td>
<td rowspan="5">11.43</td>
</tr>
<tr>
<td>トロント<br>シリコンバレー<br>バージニア<br>バンコク<br>ムンバイ<br> モスクワ  </td>
<td colspan="2">4.29</td>
</tr>
<tr>
<td >ソウル<br>フランクフルト   </td>
<td colspan="2">2.86</td>
</tr>
<tr>
<td >東京</td>
<td colspan="2">3.57</td>
</tr>
</tbody></table>


#### 課金事例

帯域幅上移動のあるユーザーがシンガポールリージョンのEIPを購入した場合は、帯域幅サブスクリプション(月額課金)による課金モードを選択します。このユーザーは2か月15Mbpsの固定帯域幅を購入したので、その総額は以下のようになります。：（2.86米ドル/Mbps/月 × 2Mbps + 3.57米ドル/Mbps/月 × 3MMbps + 12.86米ドル/Mbps/月 × 10Mbps）× 2か月=290.06米ドル

<span id = "4"></span>

### Bandwidth Package

帯域幅Bandwidth Package課金モードのEIPが月締め後払いなら、大規模な業務に適用し、同時にパブリックネットワークの異なるインスタンスの間のトラフィックピークシフトが形成できるユースケースに使用します。詳細は[Bandwidth Package課金説明](https://intl.cloud.tencent.com/document/product/684/15255)をご参照ください 。






