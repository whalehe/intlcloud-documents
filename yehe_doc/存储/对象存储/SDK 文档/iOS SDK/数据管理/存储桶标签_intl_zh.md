## 简介

本文档提供关于存储桶标签的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名         | 操作描述                         |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | 设置存储桶标签 | 为已存在的存储桶设置标签         |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | 查询存储桶标签 | 查询指定存储桶下已有的存储桶标签 |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | 删除存储桶标签 | 删除指定的存储桶标签             |

## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API 参考](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)。

## 设置存储桶标签

#### 功能说明

PUT Bucket tagging 用于为已存在的存储桶设置标签。

#### 示例代码
**Objective-C**

[//]: # (.cssg-snippet-put-bucket-tagging)
```objective-c
QCloudPutBucketTaggingRequest *putReq = [QCloudPutBucketTaggingRequest new];

// 存储桶名称，格式为 BucketName-APPID
putReq.bucket = @"examplebucket-1250000000";

// 标签集合
QCloudBucketTagging *taggings = [QCloudBucketTagging new];

QCloudBucketTag *tag1 = [QCloudBucketTag new];

// 标签的 Key，长度不超过128字节, 支持英文字母、数字、空格、加号、减号、下划线、等号、点号、
// 冒号、斜线
tag1.key = @"age";

// 标签的 Value，长度不超过256字节, 支持英文字母、数字、空格、加号、减号、下划线、等号、点号
// 、冒号、斜线
tag1.value = @"20";
QCloudBucketTag *tag2 = [QCloudBucketTag new];
tag2.key = @"name";
tag2.value = @"karis";

// 标签集合，最多支持10个标签
QCloudBucketTagSet *tagSet = [QCloudBucketTagSet new];
tagSet.tag = @[tag1,tag2];
taggings.tagSet = tagSet;

// 标签集合
putReq.taggings = taggings;

[putReq setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject 包含所有的响应 http 头部
    NSDictionary* info = (NSDictionary *) outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketTagging:putReq];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/BucketTagging.m) 查看。

**Swift**

[//]: # (.cssg-snippet-put-bucket-tagging)
```swift
let req = QCloudPutBucketTaggingRequest.init();

// 存储桶名称，格式为 BucketName-APPID
req.bucket = "examplebucket-1250000000";
let taggings = QCloudBucketTagging.init();

// 标签集合
let tagSet = QCloudBucketTagSet.init();
taggings.tagSet = tagSet;
let tag1 = QCloudBucketTag.init();

// 标签的 Key，长度不超过128字节, 支持英文字母、数字、空格、加号、减号、下划线、等号、点号、
// 冒号、斜线
tag1.key = "age";

// 标签的 Value，长度不超过256字节, 支持英文字母、数字、空格、加号、减号、下划线、等号、点号
// 、冒号、斜线
tag1.value = "20";

let tag2 = QCloudBucketTag.init();
tag2.key = "name";
tag2.value = "karis";

// 标签集合，最多支持10个标签
tagSet.tag = [tag1,tag2];

// 标签集合
req.taggings = taggings;
req.finishBlock = {(result,error) in
    if error != nil{
        print(error!);
    }else{
        print( result!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketTagging(req);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/BucketTagging.swift) 查看。

## 查询存储桶标签

#### 功能说明

GET Bucket tagging 用于查询指定存储桶下已有的存储桶标签。

#### 示例代码
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-tagging)
```objective-c
QCloudGetBucketTaggingRequest *getReq = [QCloudGetBucketTaggingRequest new];

// 存储桶名称，格式为 BucketName-APPID
getReq.bucket = @"examplebucket-1250000000";

[getReq setFinishBlock:^(QCloudBucketTagging * result, NSError * error) {
    // tag的集合
    QCloudBucketTagSet * tagSet = result.tagSet;
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketTagging:getReq];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/BucketTagging.m) 查看。

**Swift**

[//]: # (.cssg-snippet-get-bucket-tagging)
```swift
let req = QCloudGetBucketTaggingRequest.init();

// 存储桶名称，格式为 BucketName-APPID
req.bucket = "examplebucket-1250000000";
req.setFinish { (result, error) in
    if error != nil{
        print(error!);
    }else{
        print( result!);
    }
};
QCloudCOSXMLService.defaultCOSXML().getBucketTagging(req);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/BucketTagging.swift) 查看。

## 删除存储桶标签

#### 功能说明

DELETE Bucket tagging 用于删除指定存储桶下已有的存储桶标签。

#### 示例代码
**Objective-C**

[//]: # (.cssg-snippet-delete-bucket-tagging)
```objective-c
QCloudDeleteBucketTaggingRequest *delReq = [QCloudDeleteBucketTaggingRequest new];

// 存储桶名称，格式为 BucketName-APPID
delReq.bucket =  @"examplebucket-1250000000";

[delReq setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject 包含所有的响应 http 头部
    NSDictionary* info = (NSDictionary *) outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketTagging:delReq];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/BucketTagging.m) 查看。

**Swift**

[//]: # (.cssg-snippet-delete-bucket-tagging)
```swift
let req = QCloudDeleteBucketTaggingRequest.init();

// 存储桶名称，格式为 BucketName-APPID
req.bucket = "examplebucket-1250000000";
req.finishBlock =  { (result, error) in
    if error != nil{
        print(error!);
    }else{
        print( result!);
    }
};
QCloudCOSXMLService.defaultCOSXML().deleteBucketTagging(req);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/BucketTagging.swift) 查看。

