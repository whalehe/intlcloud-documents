

## 简介

本文档提供关于自定义域名的 API 概览以及 SDK 示例代码。

| API               | 操作名         | 操作描述                   |
| ----------------- | -------------- | -------------------------- |
| PUT Bucket domain | 设置自定义域名 | 设置存储桶的自定义域名信息 |
| GET Bucket domain | 查询自定义域名 | 查询存储桶的自定义域名信息 |

## 设置自定义域名

#### 功能说明

PUT Bucket domain 用于为存储桶配置自定义域名。

#### 方法原型

```
PutBucketDomainResult putBucketDomain(PutBucketDomainRequest request) throws CosXmlClientException, CosXmlServiceException;

void putBucketDomainAsync(PutBucketDomainRequest request, CosXmlResultListener cosXmlResultListener);
```

#### 请求示例

```
String bucket = "examplebucket-1250000000"; //格式：BucketName-APPID
PutBucketDomainRequest putBucketDomainRequest = new PutBucketDomainRequest(bucket);
DomainConfiguration.DomainRule domainRule = new DomainConfiguration.DomainRule(
        DomainConfiguration.STATUS_ENABLED,
        "www.example.com",
        DomainConfiguration.TYPE_REST
);
domainRule.forcedReplacement = DomainConfiguration.REPLACE_CNAME;
putBucketDomainRequest.addDomainRule(domainRule);

// 使用同步方法
try {
    PutBucketDomainResult putBucketDomainResult = cosXmlService.putBucketDomain(putBucketDomainRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 使用异步回调请求
cosXmlService.putBucketDomainAsync(putBucketDomainRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketDomainResult putBucketDomainResult = (PutBucketDomainResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
    }
});
```

#### 参数说明

| 参数名称          | 描述                                                         | 类型   |
| ----------------- | ------------------------------------------------------------ | ------ |
| bucket            | 设置自定义域名的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| name              | 自定义域名                                                   | String |
| status            | 域名上线状态，可选值有 ENABLED、DISABLED                     | String |
| type              | 绑定的源站类型，可选值有 REST、WEBSITE                       | String |
| forcedReplacement | 强制覆盖已存在的配置，可选值有 CNAME、TXT                    | String |

#### 返回结果说明

| 成员变量 | 描述                                                     | 类型 |
| -------- | -------------------------------------------------------- | ---- |
| httpCode | HTTP Code， [200, 300)之间表示操作成功，否则表示操作失败 | int  |

#### 返回错误码说明

该请求可能会发生的一些常见的特殊错误如下：

| 状态码                                 | 说明                                                         |
| -------------------------------------- | ------------------------------------------------------------ |
| HTTP 409 Conflict                      | 该域名记录已存在，且请求中没有设置强制覆盖。或者该域名记录不存在，且请求中设置了强制覆盖 |
| HTTP 451 Unavailable For Legal Reasons | 该域名是中国境内域名，并且没有备案                           |

## 查询自定义域名

#### 功能说明

GET Bucket domain 用于查询存储桶的自定义域名信息。

#### 方法原型

```
GetBucketDomainResult getBucketDomain(GetBucketDomainRequest request) throws CosXmlClientException, CosXmlServiceException;

void getBucketDomainAsync(GetBucketDomainRequest request, CosXmlResultListener cosXmlResultListener);
```

#### 请求示例

```
String bucket = "examplebucket-1250000000"; //格式：BucketName-APPID
GetBucketDomainRequest getBucketDomainRequest = new GetBucketDomainRequest(bucket);
//设置签名校验 Host, 默认校验所有 Header
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
// 使用同步方法
try {
    GetBucketDomainResult getBucketTaggingResult = cosXmlService.getBucketDomain(getBucketDomainRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 使用异步回调请求
cosXmlService.getBucketDomainAsync(getBucketDomainRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketDomainResult getBucketTaggingResult = (GetBucketDomainResult)result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
    }
});
```

#### 参数说明

| 参数名称 | 描述                                                         | 类型   |
| -------- | ------------------------------------------------------------ | ------ |
| bucket   | 查询自定义域名的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### 返回结果说明

| 成员变量            | 描述                                                     | 类型                |
| ------------------- | -------------------------------------------------------- | ------------------- |
| httpCode            | HTTP Code， [200, 300)之间表示操作成功，否则表示操作失败 | int                 |
| domainConfiguration | 返回 Bucket 对象 DomainConfiguration 信息                | DomainConfiguration |

#### 返回参数说明

<table>
<thead>
<tr>
<th>参数名称</th>
<th>描述</th>
<th>类型</th>
</tr>
</thead>
<tbody><tr>
<td nowrap="nowrap">x-cos-domain-txt-verification</td>
<td>域名校验信息，该字段是一个 MD5 校验值，原串格式为：<code>cos[Region][BucketName-APPID][BucketCreateTime]</code>，其中 Region 为存储桶所在地域，BucketCreateTime 为存储桶 GMT 创建时间</td>
<td>String</td>
</tr>
</tbody></table>
