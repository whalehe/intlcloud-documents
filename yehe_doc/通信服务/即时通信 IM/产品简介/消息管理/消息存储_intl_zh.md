## 离线消息存储

即时通信 IM 支持离线消息缓存，即当用户不在线时，下次登录仍会拉取到离线消息。离线消息默认保存7天，如果用户7天内未登录，再次登录时将不能获取到7天前的离线消息。对于单聊消息，每个用户的离线消息缓存最多保存100个单聊会话的未读消息，每个单聊会话最多保存100条未读消息。超出限制的部分不会被计入未读计数，但这些消息仍会存到消息漫游中。对于群消息，则没有这些条数限制。

默认情况下，一个终端通过 SDK 把离线消息拉取到本地后，即时通信 IM 服务器便会删除这些离线消息。如果需要支持多终端，或更换终端后仍想拉取未读的离线消息，需要用户自行管理这些离线消息。禁用 SDK 自动已读上报功能后，只有用户显式调用已读上报接口时，即时通信 IM 服务器才会删除这些离线消息，否则这些离线消息将在到期后自动删除。如果用户没有显式调用已读上报接口，更换终端后，仍然可以拉取到未读的离线消息。

## 漫游消息存储

即时通信 IM 支持消息漫游，即用户更换终端的情况下，也可以获取到跟其他用户或者某个群的聊天记录。
默认情况下，单聊消息和群聊消息有7天漫游，超过漫游时长的消息会被删除。即时通信 IM 支持在控制台修改消息漫游时长，延长消息漫游时长是增值服务，具体计费说明请参考 [价格说明](https://intl.cloud.tencent.com/document/product/1047/34350)。
<span id="MsgType"></span>
不同版本的 SDK 支持延长历史消息存储时长的消息类型不同，详情如下表所示。

| SDK 版本 | 文本 | 自定义类消息 | 图片| 文件 | 短语音 | 短视频 | 富媒体消息 | 
|---------|---------|---------|---------|---------|---------|---------|---------|
| Android 4.X 版本 | &#10003; | &#10003;  | &#10003;| &#10003; | &#10003; | &#10003; | &#10003; |
| Android 3.X 版本 | &#10003; | &#10003;  | × | × | × | × | × |
| Android 2.X 版本 | &#10003; |  &#10003; | × | × | × | × | × |
| iOS 4.X 版本 | &#10003; | &#10003;  | &#10003;| &#10003; | &#10003; | &#10003; | &#10003; |
| iOS 3.X 版本 | &#10003; |  &#10003; | × | × | × | × | × |
| iOS 2.X 版本 | &#10003; |  &#10003; | × | × | × | × | × |
| PC SDK 2.X 版本 | &#10003; |  &#10003; | × | × | × | × | × |
| Web 与小程序 SDK 2.X 版本| &#10003; | &#10003;  | &#10003;| &#10003; | &#10003; | &#10003; | &#10003; |
| Web 与小程序 SDK 1.X 版本| &#10003; |  &#10003; | × | × | × | × | × |

>建议您升级至最新版本的 SDK，以便获得更好的用户体验。

## 最近联系人消息

最近联系人消息类似 QQ 的最近联系人列表中，可展示最近跟用户联系过的用户以及最后一条消息。

客户端默认情况下会在登录时通过 SDK 拉取最近联系人消息，如果本地之前没有存储过，会通过 onNewMessage 回调取得。

使用最近联系人，登录时会消耗一些流量，获取服务器中相关联系人的最后一条消息。如果不需要此功能，可通过 SDK 实现禁用，最近联系人默认存储最近100个联系人，但是保存时长跟最近联系人中的最后一条消息保存时间一致，例如默认如果超过7天跟联系人没有消息，最后一条消息过期后便无法在最近联系人中获取到此用户。

## App 本地存储

默认情况下，SDK 内部会对收到的消息进行存储，无需用户进行存储。用户可调用接口获取本地消息（无网络操作），另外，通过 getMessage 接口，也会获取本地消息，如果本地消息存在断层，会通过漫游消息补全。
SDK 默认不会删除用户消息，但我们提供本地消息删除的能力满足您特殊的需要。
>使用本地存储会消耗磁盘以及 CPU 性能，在不需要存储的场景（如直播场景，更注重消息处理性能，也不关心历史消息），可选择禁用本地存储。





