## 简介

腾讯云数据万象 CI 支持多地域存储，不同地域的默认访问域名不同。创建存储桶时选定的地域不可修改，建议您根据自己的业务场景选择就近的地域存储，可以提高对象上传、下载速度。


>
> - 创建存储桶后会生成对应的默认域名，可通过 [数据万象控制台](https://console.cloud.tencent.com/ci/bucket) 的存储桶【域名管理】中查看。
> - BucketName 是您在创建存储桶时所输入的自定义名称，可通过 [数据万象控制台](https://console.cloud.tencent.com/ci/bucket)  的存储桶【Bucket配置】中查看。
> - APPID 是在成功申请腾讯云账户后，系统分配的账户标识之一，可通过 [腾讯云控制台](https://console.cloud.tencent.com/developer) 【账号信息】查看。


## 中国大陆地域
| 地域         | 处理域名            |
| ------------ | ----------|
| 北京 | &lt;BucketName-APPID&gt;.cos.ap-beijing.myqcloud.com   | 
|南京| &lt;BucketName-APPID&gt;.cos.ap-nanjing.myqcloud.com   | 
| 上海 | &lt;BucketName-APPID&gt;.cos.ap-shanghai.myqcloud.com  |
| 广州 | &lt;BucketName-APPID&gt;.cos.ap-guangzhou.myqcloud.com | 
| 成都 | &lt;BucketName-APPID&gt;.cos.ap-chengdu.myqcloud.com   | 
| 重庆 | &lt;BucketName-APPID&gt;.cos.ap-chongqing.myqcloud.com  |


## 中国香港及境外地域
| 地域     | 上传域名                                         | 下载域名                               |
| :------- | :----------------------------------------------- | :------------------------------------- |
| 中国香港 | &lt;BucketName-APPID&gt;.pic.ap-hongkong.myqcloud.com  | &lt;BucketName-APPID&gt;.pichk.myqcloud.com  |
| 莫斯科   | &lt;BucketName-APPID&gt;.pic.eu-moscow.myqcloud.com    | &lt;BucketName-APPID&gt;.picru.myqcloud.com  |
| 新加坡  | &lt;BucketName-APPID&gt;.pic.ap-singapore.myqcloud.com| &lt;BucketName-APPID&gt;.picsgp.myqcloud.com |
| 多伦多  | &lt;BucketName-APPID&gt;.pic.na-toronto.myqcloud.com | &lt;BucketName-APPID&gt;.picca.myqcloud.com  |
| 孟买    | &lt;BucketName-APPID&gt;.pic.ap-mumbai.myqcloud.com | &lt;BucketName-APPID&gt;.picin.myqcloud.com  |
| 美国硅谷    | &lt;BucketName-APPID&gt;.pic.na-siliconvalley.myqcloud.com | &lt;BucketName-APPID&gt;.picusw.myqcloud.com|

**示例**：
用户在所属地域广州创建了一个存储桶，存储桶名称中用户自定义字符串部分为 examplebucket，系统自动为用户生成的数字串 APPID 为 1250000000。
则其数据万象的处理域名为：`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`。

