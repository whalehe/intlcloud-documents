## 简介

本文档提供关于版本控制的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名       | 操作描述                 |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | 设置版本控制 | 设置存储桶的版本控制功能 |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | 查询版本控制 | 查询存储桶的版本控制信息 |

## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API 参考](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/)。

## 设置版本控制

#### 功能说明

设置指定存储桶的版本控制功能。开启版本控制功能后，只能暂停，不能关闭。

#### 示例代码

[//]: # ".cssg-snippet-put-bucket-versioning"
```java
String bucket = "examplebucket-1250000000"; //格式：BucketName-APPID
PutBucketVersioningRequest putBucketVersioningRequest =
        new PutBucketVersioningRequest(bucket);
//true：开启版本控制; false：暂停版本控制
putBucketVersioningRequest.setEnableVersion(true);

cosXmlService.putBucketVersionAsync(putBucketVersioningRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketVersioningResult putBucketVersioningResult =
                (PutBucketVersioningResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/qcloud-sdk-android/tree/master/Demo/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketVersioning.java) 查看。

## 查询版本控制

#### 功能说明

查询指定存储桶的版本控制信息。

- 获取存储桶版本控制的状态，需要有该存储桶的读权限。
- 有三种版本控制状态：未启用版本控制、启用版本控制和暂停版本控制。

#### 示例代码

[//]: # ".cssg-snippet-get-bucket-versioning"
```java
String bucket = "examplebucket-1250000000"; //格式：BucketName-APPID
GetBucketVersioningRequest getBucketVersioningRequest =
        new GetBucketVersioningRequest(bucket);

cosXmlService.getBucketVersioningAsync(getBucketVersioningRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketVersioningResult getBucketVersioningResult =
                (GetBucketVersioningResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/qcloud-sdk-android/tree/master/Demo/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketVersioning.java) 查看。

