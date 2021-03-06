

## 简介

本文档提供关于自定义域名的 API 概览以及 SDK 示例代码。

| API                  | 操作名         | 操作描述                   |
| -------------------- | -------------- | -------------------------- |
| PUT Bucket domain    | 设置自定义域名 | 设置存储桶的自定义域名信息 |
| GET Bucket domain    | 查询自定义域名 | 查询存储桶的自定义域名信息 |
| DELETE Bucket domain | 删除自定义域名 | 删除存储桶的自定义域名     |

## 设置自定义域名

#### 功能说明

PUT Bucket domain 用于为存储桶配置自定义域名。

#### 方法原型

```
put_bucket_domain(Bucket, DomainConfiguration={}, **kwargs)
```

#### 请求示例

```
response = client.put_bucket_domain(
    Bucket='bucket',
    DomainConfiguration={
        'DomainRule': [
            {
                'Name': 'example.com',
                'Type': 'REST'|'WEBSITE'|'ACCELERATE',
                'Status': 'ENABLED'|'DISABLED',
                'ForcedReplacement': 'CNAME'|'TXT'
            },
        ]
    }
)
```

#### 参数说明

| 参数名称          | 参数描述                                                     | 类型   | 是否必填 |
| ----------------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket            | 设置自定义域名的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String | 是       |
| DomainRule        | 自定义域名的集合                                             | List   | 是       |
| Name              | 自定义域名名称                                               | String | 是       |
| Type              | 绑定的源站类型，可选值有 REST、WEBSITE                       | String | 是       |
| Status            | 域名上线状态，可选值有 ENABLED、DISABLED                     | String | 是       |
| ForcedReplacement | 强制覆盖已存在的配置，可选值有 CNAME、TXT                    | String | 否       |

#### 返回结果说明

该方法返回值为 None。

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
get_bucket_domain(Bucket, **kwargs)
```

#### 请求示例

```
response = client.get_bucket_domain(
    Bucket='examplebucket-1250000000'
)
```

#### 参数说明 

| 参数名称 | 参数描述                                                     | 类型   | 是否必填 |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket   | 查询自定义域名的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String | 是       |

#### 返回结果说明

Bucket 自定义域名配置，类型为 dict。

```
{
    'x-cos-domain-txt-verification': 'string',
    'DomainRule': [
        {
            'Name': 'example.com',
            'Type': 'REST'|'WEBSITE'|'ACCELERATE',
            'Status': 'ENABLED'|'DISABLED',
            'ForcedReplacement': 'CNAME'|'TXT'
        },
    ]
}
```

| 参数名称                      | 参数描述                                                     | 类型   |
| ----------------------------- | ------------------------------------------------------------ | ------ |
| x-cos-domain-txt-verification | 域名校验信息，该字段是一个 MD5 校验值，原串格式为：`cos[Region][BucketName-APPID][BucketCreateTime]`，其中 Region 为存储桶所在地域，BucketCreateTime 为存储桶 GMT 创建时间 | String |
| DomainRule                    | 自定义域名的集合                                             | List   |
| Name                          | 自定义域名名称                                               | String |
| Type                          | 绑定的源站类型，可选值有 REST、WEBSITE                       | String |
| Status                        | 域名上线状态，可选值有 ENABLED、DISABLED                     | String |
| ForcedReplacement             | 强制覆盖已存在的配置，可选值有 CNAME、TXT  |String|

## 删除自定义域名

#### 功能说明

DELETE Bucket domain 用于删除指定存储桶下已有的自定义域名配置。

#### 方法原型

```
delete_bucket_domain(Bucket, **kwargs)
```

#### 请求示例

```
response = client.delete_bucket_domain(
    Bucket='examplebucket-1250000000'
)
```

#### 参数说明

| 参数名称 | 参数描述                                                     | 类型   | 是否必填 |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket   | 被删除自定义域名的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String | 是       |

#### 返回结果说明

该方法返回值为 None。
