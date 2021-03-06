## 操作场景
弹性 MapReduce 已接入云监控，用户可在云监控控制台配置弹性 MapReduce 主机和服务监控指标的告警策略。

## 操作步骤
1. 登录云监控控制台，进入【[告警策略](https://console.cloud.tencent.com/monitor/policylist)】单击【新增】。
![](https://main.qcloudimg.com/raw/624095be6772081ea7a6b1c9191b676e.png)
2. 在【策略类型】下拉菜单中选择弹性 MapReduce 服务监控指标或主机监控指标告警策略。
 - 服务监控指标包含：HDFS、YARN、PRESTO、HBASE、SPARK、HIVE、ZOOKEEPER。
 - 主机监控指标包含：内存、文件句柄、CPU、进程等。
![](https://main.qcloudimg.com/raw/55593982839191bd9f83e331f91c1b30.png)
3. 配置【告警对象】。有三种方式，全部对象、选择部分对象和选择实例组，默认为选择部分对象，用户可自行选择。若没有实例组，可单击【新建实例组】创建。
![](https://main.qcloudimg.com/raw/b3e822f3c2592da181c4ad81efab67a4.png)
4. 设置【触发条件】。有两种方式触发条件模板和配置触发条件，您可选择其中一种触发条件。触发条件设置详见 [创建告警策略](https://intl.cloud.tencent.com/document/product/248/6215)。
![](https://main.qcloudimg.com/raw/c92810fba840f4b079ba9a2b595a3048.png)
5. 配置【告警渠道】。根据需求配置告警接收对象（接收人、接收组）、有效时段、接收渠道（邮件、短信）。
![](https://main.qcloudimg.com/raw/24762d7963bbd302fdfadd1926839faf.png)
6. 回调接口具备将告警信息通过 HTTP 的 POST 请求推送到可访问公网 URL 的功能，您可基于 [回调接口](https://intl.cloud.tencent.com/document/product/248/9066) 推送的告警信息做进一步的处理。
7. 告警限制短信配额和策略组数量与云监控 [使用限制](https://intl.cloud.tencent.com/document/product/248/32803) 一致。
