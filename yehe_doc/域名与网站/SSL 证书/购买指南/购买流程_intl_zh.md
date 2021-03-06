### 1. 选择证书品牌以及型号

腾讯云目前支持四种品牌 SSL 证书的售卖，详细如下：

#### SecureSite
SecureSite 是全球最大的信息安全厂商和服务商，最权威的数字证书颁发机构，为企业、个人用户和服务供应商提供广泛的内容和网络安全解决方案。全球500强中有93%选择了 VeriSign SSL 数字证书，SecureSite 于2010年8月收购 VeriSign，并于2012年4月对 VeriSign 的产品名称和品牌标识进行变更，目前 VeriSign 认证服务均由 SecureSite 提供。

#### GeoTrust
GeoTrust 是全球第二大数字证书颁发机构（CA），也是身份认证和信任认证领域的领导者，该公司各种先进的技术使得任何大小的机构和公司都能安全地低成本地部署 SSL 数字证书和实现各种身份认证。从2001年成立到2006年占领全球市场25%的市场份额， VeriSign 于2006年5月 - 2006年9月以1.25亿美元收购 GeoTrust，目前也同为 SecureSite 旗下 SSL 证书的**性价比高**的品牌。

单纯从技术角度，SecureSite（原 Verisign）和 GeoTrust 的区别如下：
- 算法支持上 SecureSite（支持 RSA、DSA、ECC 三种算法）优于 GeoTrust（支持 RSA、DSA 两种算法）。
- 兼容性 SecureSite 优于 GeoTrust，SecureSite 可兼容市面上所有的浏览器，对移动端的支持也是极好的。
- OCSP 响应速度上 SecureSite 优于 GeoTrust。
- CA 安全性方面 SecureSite 优于 GeoTrust，SecureSite 是国际知名安全厂商，CA 的安全级别也是国际第一的安全系数。
- SecureSite 证书除实现加密传输以外，还另外有恶意软件扫描和漏洞评估的附加功能。
- SecureSite 对证书有商业保险赔付保障，金额最高为175万美金，GeoTrust 最高为150万美金。

#### TrustAsia
亚洲诚信是亚数信息科技（上海）有限公司应用于信息安全领域的品牌，是 SecureSite 的白金合作伙伴，专业为企业提供包含数字证书在内的所有网络安全服务。同时，TrustAsia 品牌 SSL 证书由 SecureSite 根证书签发。

#### GlobalSign
GlobalSign 成立于1996年，是一家声誉卓著，备受信赖的 CA 中心和 SSL 数字证书提供商，在全球总计颁发超过2000万张数字证书。GlobalSign 的专业实力获得中国网络市场众多服务器、域名注册商、系统服务供应商的青睐，成为其数字证书服务的合作伙伴。

#### 品牌的差异
不同品牌的证书在浏览器地址栏、加密强度、赔付保障上均存在差异，最重要的差异点在于根证书。例如，GeoTrust 通配符是 GeoTrust 根证书签发的，而 SecureSite 通配符是 SecureSite 根证书签发的。SecureSite 根证书可以兼容市面上所有的浏览器，对移动端的支持也是最好的，而 Trustasia 通配符也是 SecureSite 的根证书，GlobalSign 通配符是 GlobalSign 的根证书签发的。

详细参考官网售卖提供的参数对比。如下图所示：
![](https://main.qcloudimg.com/raw/f33d982ede59c72696add01f28c84c5c.jpg)

### 2. 选择支持域名数目

#### 单个域名
即只支持绑定1个域名，可以是二级域名 example.domain.com，也可以是三级域名 example.example.domain.com，或者是一级域名 domain.com，均可以支持，**但不支持一级域名下的所有子域名**。域名级数最多可以支持100级。
> 绑定 www.domain.com 域名（子域名是 www）的 SSL 证书，会同时支持 domain.com 一级域名。

#### 多个域名
即单个证书可以绑定多个域名，最多可以支持数量以控制台展示为准。如下图所示：
> 
> - SecureSite 多域名证书的价格即按域名数目进行叠加。
> - GeoTrust、TrustAsia、GlobalSign 多域名证书除默认支持域名数量外，附加域名再另叠加计价。

![](https://main.qcloudimg.com/raw/f58e72c57294735d23a21b2815710822.jpg)

#### 泛域名
即支持绑定一个且只有一个泛域名，泛域名至允许添加一个通配符。例如，\*.domain.com，\*.example.domain.com，最多支持100级；\*.\*.domain.com 多个通配符的泛域名是不支持的。如下图所示：
> 绑定 \*.domain.com 域名（必须是二级泛域名）的 SSL 证书，会同时支持 domain.com 一级域名。

![](https://main.qcloudimg.com/raw/2d984c38bd2ee35ddd04b86009ada117.jpg)

#### 多个泛域名（通配符多域名）
支持绑定多个泛域名，例如 \*.domain.com、\*.ssl.domain.com、\*.another.com，共计3个泛域名。包含同一级的全部子域名，最多可以支持数量以控制台展示为准。如下图所示：
![](https://main.qcloudimg.com/raw/a458616c337d4dc1dc083019679f793a.png)

### 3. 选择证书年限
OV 型与 EV 型证书最多可以支持2年，DV 型证书只能支持1年。同时按照1年85折、2年75折进行销售中（价格按官网销售价为准）。

### 4. 订单支付
完成品牌、型号、支持域名、和证书年限的选择后，则可以提交订单，继续完成支付流程。


### 5. 提交申请
证书购买完成后，需在 [SSL 证书管理控制台](https://console.cloud.tencent.com/ssl) 中提交审核材料进行证书申请，CA 机构审核通过后将签发证书。详情请查看  [付费证书申请流程](https://intl.cloud.tencent.com/document/product/1007/30160)。


