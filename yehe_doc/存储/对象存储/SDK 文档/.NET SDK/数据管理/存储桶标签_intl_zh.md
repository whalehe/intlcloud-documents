

## 简介

本文档提供关于存储桶标签的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名         | 操作描述                         |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | 设置存储桶标签 | 为已存在的存储桶设置标签         |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | 查询存储桶标签 | 查询指定存储桶下已有的存储桶标签 |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | 删除存储桶标签 | 删除指定的存储桶标签             |

## 设置存储桶标签

#### 功能说明

PUT Bucket tagging 用于为已存在的存储桶设置标签。

#### 方法原型

```
PutBucketTaggingResult putBucketTagging(PutBucketTaggingRequest request);

void putBucketTaggingAsync(PutBucketTaggingRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 请求示例

```
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  //设置连接超时时间，单位毫秒，默认45000ms
  .SetReadWriteTimeoutMs(40000)  //设置读写超时时间，单位毫秒，默认45000ms
  .IsHttps(true)  //设置默认 HTTPS 请求
  .SetAppid("1250000000") //设置腾讯云账户的账户标识 APPID
  .SetRegion("ap-guangzhou") //设置一个默认的存储桶地域
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
  PutBucketTaggingRequest request = new PutBucketTaggingRequest(bucket);
  string akey = "aTagKey";
  string avalue = "aTagValue";
  string bkey = "bTagKey";
  string bvalue = "bTagValue";

  request.AddTag(akey, avalue);
  request.AddTag(bkey, bvalue);
   
  //执行请求
  PutBucketTaggingResult result = cosXml.putBucketTagging(request);
  
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

#### 参数说明

| 参数名称 | 描述                                                         | 类型   |
| -------- | ------------------------------------------------------------ | ------ |
| bucket   | 设置标签的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | string |
| key      | 标签的 Key，长度不超过128字节, 支持英文字母、数字、空格、加号、减号、下划线、等号、点号、冒号、斜线 | string |
| value    | 标签的 Value，长度不超过256字节, 支持英文字母、数字、空格、加号、减号、下划线、等号、点号、冒号、斜线 | string |

#### 返回结果说明

| 成员变量 | 描述                                                     | 类型 |
| -------- | -------------------------------------------------------- | ---- |
| httpCode | HTTP Code， [200, 300)之间表示操作成功，否则表示操作失败 | int  |

## 查询存储桶标签

#### 功能说明

GET Bucket tagging 用于查询指定存储桶下已有的存储桶标签。

#### 方法原型

```
GetBucketTaggingResult getBucketTagging(GetBucketTaggingRequest request);

void getBucketTaggingAsync(GetBucketTaggingRequest request,COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 请求示例

```
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  //设置连接超时时间，单位毫秒，默认45000ms
  .SetReadWriteTimeoutMs(40000)  //设置读写超时时间，单位毫秒，默认45000ms
  .IsHttps(true)  //设置默认 HTTPS 请求
  .SetAppid("1250000000") //设置腾讯云账户的账户标识 APPID
  .SetRegion("ap-guangzhou") //设置一个默认的存储桶地域
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
  GetBucketTaggingRequest request = new GetBucketTaggingRequest(bucket);   
  //执行请求
  GetBucketTaggingResult result = cosXml.getBucketTagging(request);
  
  //请求成功
  Tagging tagging = result.tagging;
  Console.WriteLine(tagging);
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

#### 参数说明

| 参数名称 | 描述                                                         | 类型 |
| -------- | ------------------------------------------------------------ | ---- |
| bucket   | 查询标签的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | xxx  |

#### 返回结果说明

| 成员变量 | 描述                                                     | 类型 |
| -------- | -------------------------------------------------------- | ---- |
| httpCode | HTTP Code， [200, 300)之间表示操作成功，否则表示操作失败 | int  |

## 删除存储桶标签

#### 功能说明

DELETE Bucket tagging 用于删除指定存储桶下已有的存储桶标签。

#### 方法原型

```
DeleteBucketTaggingResult deleteBucketTagging(DeleteBucketTaggingRequest request);

void deleteBucketTaggingAsync(DeleteBucketTaggingRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 请求示例

```
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  //设置连接超时时间，单位毫秒，默认45000ms
  .SetReadWriteTimeoutMs(40000)  //设置读写超时时间，单位毫秒，默认45000ms
  .IsHttps(true)  //设置默认 HTTPS 请求
  .SetAppid("1250000000") //设置腾讯云账户的账户标识 APPID
  .SetRegion("ap-guangzhou") //设置一个默认的存储桶地域
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
  DeleteBucketTaggingRequest request = new DeleteBucketTaggingRequest(bucket);   
  //执行请求
  DeleteBucketTaggingResult result = cosXml.deleteBucketTagging(request);
  
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

#### 参数说明

| 参数名称 | 描述                                                         | 类型   |
| -------- | ------------------------------------------------------------ | ------ |
| bucket   | 被删除标签的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | string |

#### 返回结果说明

| 成员变量 | 描述                                                     | 类型 |
| -------- | -------------------------------------------------------- | ---- |
| httpCode | HTTP Code， [200, 300)之间表示操作成功，否则表示操作失败 | int  |
