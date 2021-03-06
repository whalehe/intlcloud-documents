## 简介

您可以通过对象存储控制台，随时对已上传的对象进行存储类型的修改，以满足不同场景的业务需求。对象存储 COS 提供：标准存储、低频存储和归档存储，详情请参阅 [存储类型](https://intl.cloud.tencent.com/document/product/436/30925)。下面将为您详细介绍如何修改对象存储类型。

>
>- 若对象属于**归档存储**类型，则需要恢复到标准存储类型才可修改其他存储类型，详情请参阅 [恢复归档对象](https://intl.cloud.tencent.com/document/product/436/30961)。
>- 不支持对大于5GB的对象进行存储类型的修改。

## 操作步骤

1. 登录 [对象存储控制台](https://console.cloud.tencent.com/cos5)。
2. 在左侧导航栏中，单击【存储桶列表】。
3. 单击存储桶名称，进入对象所在的存储桶。
![](https://main.qcloudimg.com/raw/156823c7ad23708feb85f5d682c61d50.png)
4. 在存储桶的“文件列表”模块下，找到需要设置存储类型的对象，在其右侧操作栏中，单击【详情】。
![](https://main.qcloudimg.com/raw/2bdec7021171ddb5bea5868783dfaee4.png)
5. 下拉页面找到**存储类型**配置项，选择修改的存储类型。
![](https://main.qcloudimg.com/raw/9ef26cd5ea448fbc048cc5ba890218e4.png)
6. 单击【保存】，即可修改对象存储类型。
