## 下载与安装

#### 相关资源
- 对象存储的 XML .NET SDK 源码下载地址：[ COS XML .NET SDK ](https://github.com/tencentyun/qcloud-sdk-dotnet)。
- SDK 快速下载地址：[XML .NET SDK](https://cos-sdk-archive-1253960454.file.myqcloud.com/qcloud-sdk-dotnet/latest/qcloud-sdk-dotnet.zip?_ga=1.63139823.1783616852.1583375173)。	

#### 环境依赖
COS XML .NET SDK 基于 .NET Standard 2.0 开发。

- Windows：安装 .NET Core 2.0 及以上版本，或者 .NET Framework 4.6.1 及以上版本。 
- Linux/Mac：安装 .NET Core 2.0 及以上版本。

#### 添加 SDK

我们提供 Nuget 的集成方式，您可以在工程的 csproj 文件里添加：

```
<PackageReference Include="Tencent.QCloud.Cos.Sdk" Version="5.4.*" />
```

如果是用 .NET CLI，请使用如下命令安装：

```shell
dotnet add package Tencent.QCloud.Cos.Sdk
```

您也可以在 [这里](https://github.com/tencentyun/qcloud-sdk-dotnet/releases) 手动下载我们的SDK。

## 开始使用
下面为您介绍如何使用 COS .NET SDK 完成一个基础操作，例如初始化客户端、创建存储桶、查询存储桶列表、上传对象、查询对象列表、下载对象和删除对象。


>关于文章中出现的 SecretId、SecretKey、Bucket 等名称的含义和获取方式请参见 [COS 术语信息](https://cloud.tencent.com/document/product/436/7751#.E6.9C.AF.E8.AF.AD.E4.BF.A1.E6.81.AF)。

SDK 中常用的命名空间有：

```C#
using COSXML;
using COSXML.Auth;
using COSXML.Model.Object;
using COSXML.Model.Bucket;
using COSXML.CosException;
```

### 初始化

在执行任何和 COS 服务相关请求之前，都需要先实例化`CosXmlConfig , QCloudCredentialProvider , CosXmlServer`3个对象。其中：
- `CosXmlConfig`提供配置 SDK 接口。
- `QCloudCredentialProvider`提供设置密钥信息接口。
- `CosXmlServer`提供各种 COS API 服务接口。

>下述初始化示例中使用的临时密钥，其生成和使用可参见 [临时密钥生成及使用指引](https://intl.cloud.tencent.com/document/product/436/14048)。

[//]: # (.cssg-snippet-global-init)
```C#
//初始化 CosXmlConfig 
string appid = "1250000000";//设置腾讯云账户的账户标识 APPID
string region = "COS_REGION"; //设置一个默认的存储桶地域
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  //设置连接超时时间，单位毫秒，默认45000ms
  .SetReadWriteTimeoutMs(40000)  //设置读写超时时间，单位毫秒，默认45000ms
  .IsHttps(true)  //设置默认 HTTPS 请求
  .SetAppid(appid)  //设置腾讯云账户的账户标识 APPID
  .SetRegion(region)  //设置一个默认的存储桶地域
  .SetDebugLog(true)  //显示日志
  .Build();  //创建 CosXmlConfig 对象

//初始化 QCloudCredentialProvider，COS SDK 中提供了3种方式：永久密钥、临时密钥、自定义
QCloudCredentialProvider cosCredentialProvider = null;

//方式1， 永久密钥
string secretId = "COS_SECRETID"; //"云 API 密钥 SecretId";
string secretKey = "COS_SECRETKEY"; //"云 API 密钥 SecretKey";
long durationSecond = 600;  //每次请求签名有效时长，单位为秒
cosCredentialProvider = new DefaultQCloudCredentialProvider(secretId, secretKey, durationSecond);

//方式2， 临时密钥
string tmpSecretId = "COS_SECRETID"; //"临时密钥 SecretId";
string tmpSecretKey = "COS_SECRETKEY"; //"临时密钥 SecretKey";
string tmpToken = "COS_TOKEN"; //"临时密钥 token";
long tmpExpireTime = 1546862502;//临时密钥有效截止时间
cosCredentialProvider = new DefaultSessionQCloudCredentialProvider(tmpSecretId, tmpSecretKey, 
  tmpExpireTime, tmpToken);

//初始化 CosXmlServer
CosXmlServer cosXml = new CosXmlServer(config, cosCredentialProvider);
```
[//]: # (.cssg-snippet-global-init-custom-credential-provider)
```C#
//方式3: 自定义方式提供密钥， 继承 QCloudCredentialProvider 并重写 GetQCloudCredentials() 方法
public class MyQCloudCredentialProvider : QCloudCredentialProvider
{
  public override QCloudCredentials GetQCloudCredentials()
  {
    string secretId = "COS_SECRETID"; //密钥 SecretId
    string secretKey = "COS_SECRETKEY"; //密钥 SecretKey
    //密钥有效时间, 精确到秒，例如1546862502;1546863102
    string keyTime = "SECRET_STARTTIME;SECRET_ENDTIME"; 
    return new QCloudCredentials(secretId, secretKey, keyTime);
  }

  public override void Refresh()
  {
    //更新密钥信息，密钥过期会自动回调该方法
  }
}
```

### 创建存储桶
[//]: # (.cssg-snippet-put-bucket)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  //设置连接超时时间，单位毫秒，默认45000ms
  .SetReadWriteTimeoutMs(40000)  //设置读写超时时间，单位毫秒，默认45000ms
  .IsHttps(true)  //设置默认 HTTPS 请求
  .SetAppid("1250000000") //设置腾讯云账户的账户标识 APPID
  .SetRegion("COS_REGION") //设置一个默认的存储桶地域
  .Build();

string secretId = "COS_SECRETID";   //云 API 密钥 SecretId
string secretKey = "COS_SECRETKEY"; //云 API 密钥 SecretKey
long durationSecond = 600;          //每次请求签名有效时长，单位为秒
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  string bucket = "examplebucket-1250000000"; //格式：BucketName-APPID
  PutBucketRequest request = new PutBucketRequest(bucket);
  //设置签名有效时长
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  //执行请求
  PutBucketResult result = cosXml.PutBucket(request);
  //请求成功
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  //请求失败
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  //请求失败
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

### 查询存储桶列表
[//]: # (.cssg-snippet-get-service)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  //设置连接超时时间，单位毫秒，默认45000ms
  .SetReadWriteTimeoutMs(40000)  //设置读写超时时间，单位毫秒，默认45000ms
  .IsHttps(true)  //设置默认 HTTPS 请求
  .SetAppid("1250000000") //设置腾讯云账户的账户标识 APPID
  .SetRegion("COS_REGION") //设置一个默认的存储桶地域
  .Build();

string secretId = "COS_SECRETID";   //云 API 密钥 SecretId
string secretKey = "COS_SECRETKEY"; //云 API 密钥 SecretKey
long durationSecond = 600;          //每次请求签名有效时长，单位为秒
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  GetServiceRequest request = new GetServiceRequest();
  //设置签名有效时长
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  //执行请求
  GetServiceResult result = cosXml.GetService(request);
  //得到所有的 buckets
  List<ListAllMyBuckets.Bucket> allBuckets = result.listAllMyBuckets.buckets;
}
catch (COSXML.CosException.CosClientException clientEx)
{
  //请求失败
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  //请求失败
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

### 上传对象
[//]: # (.cssg-snippet-put-object)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  //设置连接超时时间，单位毫秒，默认45000ms
  .SetReadWriteTimeoutMs(40000)  //设置读写超时时间，单位毫秒，默认45000ms
  .IsHttps(true)  //设置默认 HTTPS 请求
  .SetAppid("1250000000") //设置腾讯云账户的账户标识 APPID
  .SetRegion("COS_REGION") //设置一个默认的存储桶地域
  .Build();

string secretId = "COS_SECRETID";   //云 API 密钥 SecretId
string secretKey = "COS_SECRETKEY"; //云 API 密钥 SecretKey
long durationSecond = 600;          //每次请求签名有效时长，单位为秒
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  string bucket = "examplebucket-1250000000"; //存储桶，格式：BucketName-APPID
  string key = "exampleobject"; //对象在存储桶中的位置，即称对象键
  string srcPath = @"temp-source-file";//本地文件绝对路径
  if (!File.Exists(srcPath)) {
    // 如果不存在目标文件，创建一个临时的测试文件
    File.WriteAllBytes(srcPath, new byte[1024]);
  }

  PutObjectRequest request = new PutObjectRequest(bucket, key, srcPath);
  //设置签名有效时长
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  //设置进度回调
  request.SetCosProgressCallback(delegate (long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  //执行请求
  PutObjectResult result = cosXml.PutObject(request);
  //对象的 eTag
  string eTag = result.eTag;
}
catch (COSXML.CosException.CosClientException clientEx)
{
  //请求失败
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  //请求失败
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

### 查询对象列表
[//]: # (.cssg-snippet-get-bucket)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  //设置连接超时时间，单位毫秒，默认45000ms
  .SetReadWriteTimeoutMs(40000)  //设置读写超时时间，单位毫秒，默认45000ms
  .IsHttps(true)  //设置默认 HTTPS 请求
  .SetAppid("1250000000") //设置腾讯云账户的账户标识 APPID
  .SetRegion("COS_REGION") //设置一个默认的存储桶地域
  .Build();

string secretId = "COS_SECRETID";   //云 API 密钥 SecretId
string secretKey = "COS_SECRETKEY"; //云 API 密钥 SecretKey
long durationSecond = 600;          //每次请求签名有效时长，单位为秒
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  string bucket = "examplebucket-1250000000"; //格式：BucketName-APPID
  GetBucketRequest request = new GetBucketRequest(bucket);
  //设置签名有效时长
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  //获取 a/ 下的对象
  request.SetPrefix("a/");
  //执行请求
  GetBucketResult result = cosXml.GetBucket(request);
  //bucket的相关信息
  ListBucket info = result.listBucket;
}
catch (COSXML.CosException.CosClientException clientEx)
{
  //请求失败
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  //请求失败
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

### 下载对象
[//]: # (.cssg-snippet-get-object)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  //设置连接超时时间，单位毫秒，默认45000ms
  .SetReadWriteTimeoutMs(40000)  //设置读写超时时间，单位毫秒，默认45000ms
  .IsHttps(true)  //设置默认 HTTPS 请求
  .SetAppid("1250000000") //设置腾讯云账户的账户标识 APPID
  .SetRegion("COS_REGION") //设置一个默认的存储桶地域
  .Build();

string secretId = "COS_SECRETID";   //云 API 密钥 SecretId
string secretKey = "COS_SECRETKEY"; //云 API 密钥 SecretKey
long durationSecond = 600;          //每次请求签名有效时长，单位为秒
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  string bucket = "examplebucket-1250000000"; //存储桶，格式：BucketName-APPID
  string key = "exampleobject"; //对象在存储桶中的位置，即称对象键
  string localDir = System.IO.Path.GetTempPath();//本地文件夹
  string localFileName = "my-local-temp-file"; //指定本地保存的文件名
  GetObjectRequest request = new GetObjectRequest(bucket, key, localDir, localFileName);
  //设置签名有效时长
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  //设置进度回调
  request.SetCosProgressCallback(delegate (long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  //执行请求
  GetObjectResult result = cosXml.GetObject(request);
  //请求成功
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  //请求失败
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  //请求失败
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

//下载返回 bytes 数据
try
{
  string bucket = "examplebucket-1250000000"; //存储桶，格式：BucketName-APPID
  string key = "exampleobject"; //对象在存储桶中的位置，即称对象键

  GetObjectBytesRequest request = new GetObjectBytesRequest(bucket, key);
  //设置签名有效时长
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  //设置进度回调
  request.SetCosProgressCallback(delegate (long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  //执行请求
  GetObjectBytesResult result = cosXml.GetObject(request);
  //获取内容
  byte[] content = result.content;
  //请求成功
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  //请求失败
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  //请求失败
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

### 删除对象
[//]: # (.cssg-snippet-delete-object)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  //设置连接超时时间，单位毫秒，默认45000ms
  .SetReadWriteTimeoutMs(40000)  //设置读写超时时间，单位毫秒，默认45000ms
  .IsHttps(true)  //设置默认 HTTPS 请求
  .SetAppid("1250000000") //设置腾讯云账户的账户标识 APPID
  .SetRegion("COS_REGION") //设置一个默认的存储桶地域
  .Build();

string secretId = "COS_SECRETID";   //云 API 密钥 SecretId
string secretKey = "COS_SECRETKEY"; //云 API 密钥 SecretKey
long durationSecond = 600;          //每次请求签名有效时长，单位为秒
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  string bucket = "examplebucket-1250000000"; //存储桶，格式：BucketName-APPID
  string key = "exampleobject"; //对象在存储桶中的位置，即称对象键
  DeleteObjectRequest request = new DeleteObjectRequest(bucket, key);
  //设置签名有效时长
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  //执行请求
  DeleteObjectResult result = cosXml.DeleteObject(request);
  //请求成功
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  //请求失败
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  //请求失败
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```
