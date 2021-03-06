﻿## 操作场景
魅族推送通道是由**魅族官方提供**的系统级推送通道。在魅族手机上，推送消息能够通过魅族的系统通道抵达终端，并且无需打开应用，即可收到推送。

>
>- 魅族推送通道通知标题不超过32字符，通知内容不超过100字符。
>- 魅族推送通道不支持透传消息。
>- 魅族通道支持抵达回调，支持点击回调，不支持透传。

## 操作步骤
### 获取密钥
进入 [魅族推送官网](https://open.flyme.cn/open-web/views/push.html)，注册并登录开发者账号，获取 AppID，AppKey，AppSecret 三种信息。更多详情请参见 [魅族开发文档](http://open.res.flyme.cn/fileserver/upload/file/201709/a271468fe23b47408fc2ec1e282f851f.pdf)。


### 集成方式
#### AndroidStudio 集成
```js
implementation 'com.tencent.tpns:meizu:[VERSION]-release'//meizu 推送 [VERSION] 为当前SDK版本号,版本号可在SDK下载页查看
```

#### Eclipse 集成
1. 下载 [SDK 安装包](https://console.cloud.tencent.com/tpns/sdkdownload)。
2. 打开 Other-Push-jar 文件夹， 导入魅族推送相关 jar 包，将 mz4tpns1.1.2.1.jar 导入项目工程中。
3. 在 Android manifest 下配置以下配置：

```xml
<application>
<service
                 android:name="com.meizu.cloud.pushsdk.NotificationService"
                 android:exported="true"/>
<receiver android:name="com.meizu.cloud.pushsdk.SystemReceiver" >
 <intent-filter>
                <action android:name="com.meizu.cloud.pushservice.action.PUSH_SERVICE_START"/>
                <category android:name="android.intent.category.DEFAULT" />
 </intent-filter>
 </receiver>
</application>
 <!-- 注：魅族push 需要的权限 begin -->
 <!-- 兼容flyme5.0以下版本，魅族内部集成pushSDK必填，不然无法收到消息-->
<uses-permission android:name="com.meizu.flyme.push.permission.RECEIVE"></uses-permission>
<permission android:name="应用包名.push.permission.MESSAGE" 
                android:protectionLevel="signature"/>
<uses-permission android:name="应用包名.push.permission.MESSAGE"></uses-permission>
<!--  兼容flyme3.0配置权限-->
<uses-permission android:name="com.meizu.c2dm.permission.RECEIVE" />
<permission android:name="应用包名.permission.C2D_MESSAGE"
                android:protectionLevel="signature">
</permission>
<uses-permission android:name="应用包名.permission.C2D_MESSAGE"/>
<!-- 注：魅族push 需要的权限 end -->
```
4. 魅族消息 receiver：在 ```AndroidManifest.xml``` 增加 ```Receiver``` 配置如下：

```xml
<receiver android:name="com.tencent.android.mzpush.MZPushMessageReceiver">
    <intent-filter>
        <!-- 接收push消息 -->
        <action android:name="com.meizu.flyme.push.intent.MESSAGE" />
        <!-- 接收register消息-->
         <action android:name="com.meizu.flyme.push.intent.REGISTER.FEEDBACK"/>
        <!-- 接收unregister消息-->
         <action android:name="com.meizu.flyme.push.intent.UNREGISTER.FEEDBACK"/>
         <action android:name="com.meizu.c2dm.intent.REGISTRATION" />
         <action android:name="com.meizu.c2dm.intent.RECEIVE" />
         <category android:name="应用包名"></category>
     </intent-filter>
</receiver>
```


5.  Flyme 6.0 及以下版本的魅族手机，使用手动集成方式，需要在 drawable 不同分辨率的文件夹下对应放置一张名称必须为 stat_sys_third_app_notify 的图片，详情请参考 [TPNS Android SDK](https://console.cloud.tencent.com/tpns/sdkdownload) 中的 flyme-notification-res 文件夹。

### 开启魅族推送
在启动移动推送 TPNS ，调用 `XGPushManager.registerPush` 之前，配置如下代码：

```java
//设置魅族APPID和APPKEY
XGPushConfig.enableOtherPush(context, true);
XGPushConfig.setMzPushAppId(this, APP_ID);
XGPushConfig.setMzPushAppKey(this, APP_KEY);
```

注册成功的日志如下：

```java
//成功的获取到移动推送 TPNS 的token和魅族的token，并且绑定成功说明注册成功
INFO16:24:27.94313075XINGE[a] >> bind OtherPushToken success ack with [accId = 2100273138 , rsp = 0] token = 08d7ea8e4b93952cbfdd2cb68461342c314d281a otherPushType = meizu otherPushToken = ULY6c5968627059714a475c63517f675b7f655e62627e
```

如需通过点击回调获取参数或者跳转自定义页面，您可使用 Intent 来实现。更多详情请参见 [Android 常见问题](https://intl.cloud.tencent.com/document/product/1024/32624#.E5.A6.82.E4.BD.95.E8.AE.BE.E7.BD.AE.E6.B6.88.E6.81.AF.E7.82.B9.E5.87.BB.E4.BA.8B.E4.BB.B6.EF.BC.9F)。

### 代码混淆
```xml
-dontwarn com.meizu.cloud.pushsdk.**
-keep class com.meizu.cloud.pushsdk.**{*;}
```

>混淆规则需要放在 App 项目级别的 proguard-rules.pro 文件中。

### 魅族通道抵达回执配置
魅族通道抵达回执需要开发者自行配置，您可参照 [魅族厂商通道回执配置指引](https://intl.cloud.tencent.com/document/product/1024/35246#.E9.AD.85.E6.97.8F.E5.8E.82.E5.95.86.E9.80.9A.E9.81.93.E5.9B.9E.E6.89.A7.E9.85.8D.E7.BD.AE.E6.8C.87.E5.BC.95) 进行配置，完成后，可在推送记录中查看魅族推送通道的抵达数据。
![](https://main.qcloudimg.com/raw/2f978f623566b9f6b664dea3dca30923.png)

