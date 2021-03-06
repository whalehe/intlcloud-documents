通过手机短信发送验证码，是最普遍、最安全验证用户真实身份的方式。目前，短信验证码广泛应用于用户注册、密码找回、登录保护、身份认证、随机密码、交易确认等应用场景。
本文以使用 [云函数](https://intl.cloud.tencent.com/document/product/583) 开发一个短信验证码登录注册服务为例，帮助您了解如何实现短信验证码功能。

## 准备工作
- 已 [注册腾讯云](https://intl.cloud.tencent.com/document/product/378/17985) 账号，并完成 企业实名认证。
- 已 购买 短信套餐包。
- 准备短信签名归属方资质证明文件。
 本文以使用企业营业执照作为资质证明文件为例。
- 了解短信正文内容审核规范。
- 已获取短信应用的 SDKAppID。

## 相关资料
- [Demo 源码](https://github.com/qcloudsms/smsLogin)
- 其他产品文档
 - [私有网络产品文档](https://intl.cloud.tencent.com/document/product/215)
 - [云数据库 MySQL 产品文档](https://intl.cloud.tencent.com/document/product/236)
 - [NAT 网关产品文档](https://intl.cloud.tencent.com/document/product/1015)
 - [云函数产品文档](https://intl.cloud.tencent.com/document/product/583)



<span id="Step1"></span>
## 步骤1：配置短信内容
短信签名、短信正文模板提交后，我们会在2个小时左右完成审核，您可以 [配置告警联系人](https://intl.cloud.tencent.com/document/product/382/35470) 并设置接收模板和签名审核通知，便于及时接收审核通知。

<span id="Step1_1"></span>
### 步骤1.1：创建签名

1. 登录 [短信控制台](https://console.cloud.tencent.com/smsv2)。
2. 在左侧导航栏选择【国内短信】>【签名管理】，单击【创建签名】。
3. 结合实际情况 设置以下参数：
 <table>
     <tr>
         <th width="20%">参数</th>  
         <th>取值样例</th>  
     </tr>
	 <tr>      
       <td>签名用途</td>   
	     <td>自用（签名为本账号实名认证的公司、网站、产品名等）</td>   
     </tr> 
	 <tr>      
       <td>签名类型</td>   
	     <td>APP</td>   
     </tr> 
	 <tr>      
       <td>签名内容</td>   
	     <td>测试 Demo</td>   
     </tr> 
	 <tr>      
       <td>证明类型</td>   
	     <td>小程序设置页面截图</td>   
     </tr> 
	 <tr>      
       <td>证明上传</td>   
	<td><img src="https://main.qcloudimg.com/raw/48ad431a784461465054160737b9b166.png" width=400/></td>    
     </tr> 
</table>
3. 单击【确定】。
 等待签名审核，当状态变为【已通过】时，短信签名才可用。


<span id="Step1_2"></span>
### 步骤1.2：创建正文模板
1. 登录 [短信控制台](https://console.cloud.tencent.com/smsv2)。
2. 在左侧导航栏选择【国内短信】>【正文模板管理】，单击【创建正文模板】。
3. 结合实际情况 设置以下参数：
 <table>
     <tr>
         <th width="20%">参数</th>  
         <th>取值样例</th>  
     </tr>
	 <tr>      
        <td>模板名称</td>   
	     <td>验证码短信</td>   
     </tr> 
	 <tr>      
        <td>短信类型</td>   
	     <td>普通短信</td>   
     </tr> 
	 <tr>      
        <td>短信内容</td>   
	     <td>您的注册验证码：{1}，请于{2}分钟内填写，如非本人操作，请忽略本短信。</td>   
     </tr> 
</table>
4. 单击【确定】。
 等待正文模板审核，当状态变为【已通过】时，正文模板才可用，请记录模板 ID。

<span id="Step2"></span>
## 步骤2：设置短信发送频率限制（可选）
>!个人认证用户不支持修改频率限制，如需使用该功能，请将 “个人认证” 变更为 “企业认证”。

为了保障业务和通道安全，减少业务被刷后的经济损失，建议 [设置发送频率限制](https://intl.cloud.tencent.com/document/product/382/35469#.E8.AE.BE.E7.BD.AE.E5.8F.91.E9.80.81.E9.A2.91.E7.8E.87.E9.99.90.E5.88.B6)。另外，您也可以结合使用腾讯云验证码 以便最大程度地保护业务安全。
本文以短信的默认频率限制策略为例。

- 同一号码同一内容30秒内最多发送1条。
- 同一手机号一个自然日最多发送10条。

<span id="Step3"></span>
## 步骤3：配置私有网络和子网
默认情况下，云函数部署在公共网络中，只可以访问公网。如果开发者需要访问腾讯云的 TencentDB 等资源，需要建立私有网络来确保数据安全及连接安全。

1. 按需 [规划网络](https://intl.cloud.tencent.com/document/product/215/31795)。
2. 创建私有网络，具体操作请参见 [创建 VPC](https://intl.cloud.tencent.com/document/product/215/31805)。
 >!私有网络和子网的 CIDR 创建后不可修改。
 >
 <table>
     <tr>
         <th width="20%">参数</th>  
         <th>取值样例</th>  
     </tr>
	 <tr>      
        <td>所属地域</td>   
	     <td>	华南地区(广州)</td>   
     </tr> 
	 <tr>      
        <td>名称</td>   
	     <td>Demo VPC</td>   
     </tr> 
	 <tr>      
        <td>IPv4 CIDR</td>   
	     <td>10.0.0.0/16</td>   
     </tr> 
	 <tr>      
        <td>子网名称</td>   
	     <td>Demo 子网</td>   
     </tr> 
	 <tr>      
        <td>IPv4 CIDR</td>   
	     <td>10.0.0.0/16</td>   
     </tr> 
	 <tr>      
        <td>可用区</td>   
	     <td>广州三区</td>   
     </tr> 
</table>

<span id="Step4"></span>
## 步骤4：配置 MySQL 数据库
云数据库 MySQL 实例需与 [步骤3](#Step3) 配置私有网络的地域和子网的可用区保持一致。

1. 购买云数据库 MySQL 实例，具体操作请参见 [购买方式](https://intl.cloud.tencent.com/document/product/236/5160)。
 <table>
     <tr>
         <th width="20%">参数</th>  
         <th>取值样例</th>  
     </tr>
	 <tr>      
        <td>计费模式</td>   
	     <td>	按量计费</td>   
     </tr> 
	 <tr>      
        <td>地域</td>   
	     <td>广州</td>   
     </tr> 
	 <tr>      
        <td>数据库版本</td>   
	     <td>MySQL5.7</td>   
     </tr> 
	 <tr>      
        <td>架构</td>   
	     <td>高可用版</td>   
     </tr> 
	 <tr>      
        <td>主可用区</td>   
	     <td>广州三区</td>   
     </tr> 
	 <tr>      
        <td>备可用区</td>   
	     <td>广州四区</td>   
     </tr> 
	 <tr>      
        <td>实例规格</td>   
	     <td>4核8000MB</td>   
     </tr> 
	 <tr>      
        <td>硬盘</td>   
	     <td>200GB</td>   
     </tr> 
	 <tr>      
        <td>网络</td>   
	     <td>Demo VPC，Demo 子网</td>   
     </tr> 
	 <tr>      
        <td>实例名</td>   
	     <td>立即命名：Demo 数据库</td>   
     </tr> 
	 <tr>      
        <td>购买数量</td>   
	     <td>1</td>   
     </tr> 
</table>
2. 初始化 MySQL 数据库，具体操作请参见 [初始化 MySQL 数据库](https://intl.cloud.tencent.com/document/product/236/3128)。
 <table>
     <tr>
         <th width="20%">参数</th>  
         <th>取值样例</th>  
     </tr>
	 <tr>      
        <td>支持字符集</td>   
	     <td>UTF8</td>   
     </tr> 
	 <tr>      
        <td>表名大小写敏感</td>   
	     <td>是</td>   
     </tr> 
	 <tr>      
        <td>自定义端口</td>   
	     <td>3306</td>   
     </tr> 
	 <tr>      
        <td>设置 root 帐号密码</td>   
	     <td>请自定义设置</td>   
     </tr> 
	 <tr>      
        <td>确认密码</td>   
	     <td>请再次输入密码</td>   
     </tr> 
</table>
3. 登录 MySQL 数据库，具体操作请参见 [登录 phpMyAdmin](https://intl.cloud.tencent.com/document/product/236/32341)。
4. 根据实际需求，创建数据表和字段用于存储用户的手机号、头像、用户昵称等信息，具体操作请参见 [创建数据库和表](https://intl.cloud.tencent.com/document/product/236/8465)。

<span id="Step5"></span>
## 步骤5：新建云函数
云函数目前支持 Python、Node.js、PHP、Java 以及 Golang 语言开发，本文以 Node.js 为例。

1. 在 [步骤3](#Step3) 创建的 VPC 所属地域中新建函数，具体操作请参见 [编写函数](https://intl.cloud.tencent.com/document/product/583/32742)。
  <table>
     <tr>
         <th width="20%">参数</th>  
         <th>取值样例</th>  
     </tr>
	 <tr>      
        <td>函数名称</td>   
	     <td>Demo</td>   
     </tr> 
	 <tr>      
        <td>运行环境</td>   
	     <td>Nodejs 8.9</td>   
     </tr> 
	 <tr>      
        <td>创建方式</td>   
	     <td>模板函数：helloworld</td>   
     </tr> 
</table>
2. 部署函数并配置触发方式为【API网关触发器】，具体操作请参见 [部署函数](https://intl.cloud.tencent.com/document/product/583/32742)。

<span id="Step6"></span>
## 步骤6：启用公网访问配置（可选）
- 2020年4月29日前，部署在 VPC 中的云函数默认隔离外网。若需使云函数同时具备内网访问和外网访问能力，可通过启用公网配置方式实现。
 登录 [云函数控制台](https://console.cloud.tencent.com/scf/index?rid=1)，选择【函数服务】，在云函数列表中单击目标函数名进入函数配置页。单击【编辑】，勾选【公网访问】并单击【保存】保存配置。
- 2020年4月29日及以后，新部署的云函数默认已启用公网访问，无需额外操作。


<span id="Step7"></span>
## 步骤7：部署短信 SDK
1. 执行以下命令，安装 SDK。
```
npm install tencentcloud-sdk-nodejs --save
```
2. 在代码中引用短信模块代码。
3. 配置发送短信核心逻辑。
<pre>
/*
 * 功能：通过 SDK 发送短信
 * 参数：手机号、短信验证码
 */
async function sendSms(phone, code) {
  const tencentcloud = require('tencentcloud-sdk-nodejs');
  const SmsClient = tencentcloud.sms.v20190711.Client;
  const Credential = tencentcloud.common.Credential;
  const ClientProfile = tencentcloud.common.ClientProfile;
  const HttpProfile = tencentcloud.common.HttpProfile;
  //腾讯云账户 secretId，secretKey，切勿泄露
  const secretId = "secretId";//需要配置为真实的 secretId
  const secretKey = "secretKey";//需要配置为真实的 secretKey

  let cred = new Credential(secretId, secretKey);
  let httpProfile = new HttpProfile();
  httpProfile.endpoint = "sms.tencentcloudapi.com";
  let clientProfile = new ClientProfile();
  clientProfile.httpProfile = httpProfile;
  let client = new SmsClient(cred, "ap-guangzhou", clientProfile);
  phone = "+86" + phone;//国内手机号

  let req = {
      PhoneNumberSet: [phone],//发送短信的手机号
      TemplateID: "",//<a href="#Step1_2">步骤1.2</a> 中创建并记录的模板 ID
      Sign: "",//<a href="#Step1_1">步骤1.1</a> 中创建的签名
      TemplateParamSet: [code],//随机验证码
      SmsSdkAppid: ""//短信应用 ID
  }

  function smsPromise() {
      return new Promise((resolve, reject) => {
          client.SendSms(req, function(errMsg, response) {
              if (errMsg) {
                  reject(errMsg)
              } else {
                  if(response.SendStatusSet && response.SendStatusSet[0] && response.SendStatusSet[0].Code === "Ok") {
                      resolve({
                          errorCode: 0,
                          errorMessage: response.SendStatusSet[0].Message,
                          data: {
                              codeStr: response.SendStatusSet[0].Code,
                              requestId: response.RequestId
                          }
                      })
                  } else {
                      resolve({
                          errorCode: -1003,//短信验证码发送失败
                          errorMessage: response.SendStatusSet[0].Message,
                          data: {
                              codeStr: response.SendStatusSet[0].Code,
                              requestId: response.RequestId
                          }
                          
                      })
                  }
              }                
          });
      })
  }
  let queryResult = await smsPromise()
  return queryResult
}
</pre>

<span id="Step8"></span>
## 步骤8：检验验证码核心逻辑
验证码的时效性要求较高，您可以把验证码存在内存中或存在云数据库 Redis 中。以手机号作为 key，存储发送时间、验证码、验证次数、是否已验证过等信息。出于安全考虑，建议设置防止暴力破解的限制，本文以验证码最多验证3次为例。
```
/*
 * 功能：根据手机号获取短信验证码
 */
async function getSms(queryString) {
  const code = Math.random().toString().slice(-6);//生成6位数随机验证码
  const sessionId = Math.random().toString().slice(-8);//生成8位随机数
  const sessionCode = {
      code: code,
      sessionId: sessionId,
      sendTime: new Date().getTime(),
      num: 0,//验证次数，最多可验证3次
      used: 1//1-未使用，2-已使用
  }
  clearCacheCode()

  cacheCode[queryString.phone] = sessionCode
```

<span id="Step9"></span>
## 步骤9：配置登录模块
登录模块主要用于用户注册或登录，首次登录（即注册）时将保存用户的手机号、用户名、头像、注册时间等信息。
```
/*
* 功能：登录
*/
async function loginSms(queryString) {
  const connection = mysql.createConnection({
    host: '', // The ip address of cloud database instance, 云数据库实例 IP 地址
    user: '', // The name of cloud database, for example, root, 云数据库用户名，例如 root
    password: '', // Password of cloud database, 云数据库密码
    database: '' // Name of the cloud database, 数据库名称
  });
  connection.connect();

  if(queryString.token) {
    return await verifyToken(connection, queryString)
  }

  if(!queryString.code || !queryString.sessionId) {
    return {
        errorCode: -1001,
        errorMessage: "缺少参数"
    }
  }

  let result = cacheCode[queryString.phone]
  if(!result || result.used === 2 || result.num >= 3) {
    return {
      errorCode: -1100,
      errorMessage: "验证码已失效"
    }
  }
  if(result.sessionId !== queryString.sessionId) {
    return {
      errorCode: -1103,
      errorMessage: "sessionId不匹配"
    }
  }
  
  if(result.code == queryString.code) {
    cacheCode[queryString.phone].used = 2;//将验证码更新为已使用
    const queryInfoSql = `select * from info where phone = ?`
    let queryInfoResult = await wrapPromise(connection, queryInfoSql, [queryString.phone])
    if(queryInfoResult.length === 0) {//没有找到记录，未注册
      return await generateInfo(connection, queryString)
    } else {
      let infoResult = queryInfoResult[0]
      return {
        errorCode: 0,
        errorMessage: "登录成功",
        data: {
          phone: infoResult.phone,
          token: getToken(infoResult.userId, infoResult),
          name: infoResult.name,
          avatar: infoResult.avatar,
          userId: infoResult.userId.toString()
        }
      }
    }
  } else {
    updateCacheCode(queryString.phone, result)
    return {
      errorCode: -1102,
      errorMessage: "验证码错误，请重新输入"
    }
  }
}
```

另外，为了登录更便捷，您可以通过 Json web token 标准来生成 token 维护登录状态，实现短时间内登录无需短信验证码的功能。

```
/*
* 功能：利用 json web token 签发一个 token
*/
function getToken(userId, infoResult) {
  return jwt.sign({
    phone: infoResult.phone,
    userId: userId,
    name: infoResult.name,
    avatar: infoResult.avatar
  }, privateKey, {expiresIn: tokenExpireTime});
}
```


