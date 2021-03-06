本方案适合集群式部署的网站/APP。

如果您的业务满足以下条件，花5分钟配置这个方案，可节省30%成本：

- 网站使用集群的方式，且集群超过1台以上的服务器；
- 网站有较长时间的空闲。根据腾讯云的统计，90%的集群在凌晨 00：00-早上 09：00 这9个小时的负载低于30%。

大部分网站的高峰时间不超过 8 个小时，剩下的 16 个小时的时间，完全可以把闲置的服务器作缩容处理，这种方式能帮助您节约大量成本。

本文以某休闲类网站为例，该网站 20：00-24：00 是访问高峰时段。

## 方案简述

- 按非高峰时段的负载部署固定资源，可采用包年包月 CVM；
- 高峰时段的不足部分采用按量计费的 CVM。通过定时任务在 20：00 扩容1台，24：00 缩容回去。

新旧方案的对比：
![](https://mc.qcloudimg.com/static/img/46cc4300131254282b894c9b1ed691ac/AS-Best+Practise-Cluster+Solution%281%29.png)

## 收益
假设原方案需要两台 4核4G 的 CVM，改成一台 4核4G 的 CVM + 每天4个小时临时CVM，能节省30%左右开支。

示例中的小网站每年可以节省1500元：

![](https://mc.qcloudimg.com/static/img/a72443a68d6f16e0a8a37d39f3b73aa7/image.jpg)

## 具体操作

实例的网站结构比较简单，只有应用服务器一个集群。如果复杂的网站，会有应用服务器集群、前端服务器集群、缓存服务器集群等，每个集群都可进行类似操作，每个集群对应一个伸缩组。

![](https://mc.qcloudimg.com/static/img/76238c1b282534b67e80a7e4d04bba17/AS-Best+Practise-Cluster+Solution%282%29.png)

### step 1. 创建集群机器的自定义镜像

这步非常简单，基于一台现成的集群机器中制作即可。如有疑问可查看 [制作自定义镜像 >>](https://intl.cloud.tencent.com/document/product/213/4942)

>注：
>您需要提前部署好镜像中的环境，保证镜像里的应用能随操作系统启动，这样扩容出来的机器就能直接工作，无需人工介入。

### step 2. 创建启动配置

扩容时 AS 以启动配置为模板创建机器，因此我们事先通过启动配置指定地域、机型、镜像。

1. 登录 [弹性伸缩控制台](https://console.cloud.tencent.com/autoscaling/config)，单击导航条中的【启动配置】。

2. 选择项目和地域，这里要注意选择 Web 应用 所在的项目和地域。
![](https://mc.qcloudimg.com/static/img/9a39d87fa90f3ae5995073a6077b1057/1.jpg)

3. 接下来的操作与购买机器类似，您可跟着指引完成启动配置创建。注意自定义镜像中，指定刚才您创建的镜像。
![](https://mc.qcloudimg.com/static/img/02220977468b12ef47c9aeb30a26b06d/2.jpg)


### step 3. 为机器创建伸缩组

在 [弹性伸缩控制台](https://console.cloud.tencent.com/autoscaling)，单击【新建】，按如下填写集群的管理信息：

- **名称**：按需起一个名字。例如这里填“应用服务器集群”
- **最小伸缩数**：集群服务器数量的下限。示例这里填 0 即可。
- **起始实例数**：伸缩组刚创建时，**自动创建**的机器数量。一般不会刚创建伸缩组就自动创建机器，建议这里填 0。
- **最大伸缩数**：集群服务器数量的上限，这里按需填写。这里以 5 为例，即伸缩组最多有 5 台机器。
- **启动配置**：选择刚才您创建的启动配置。
- **支持网络**：会话服务器的网络环境，一般选“基础网络”即可。
- **支持可用区**：即选择扩容机器落在哪个可用区里，此处按会话服务器所在的可用区勾选即可。
- **移出策略**：选择默认。
- **负载均衡**：选择集群的负载均衡。
![](https://mc.qcloudimg.com/static/img/f3ab676105c79c61ce877b92e4e6ca7c/24.jpg)

最后单击【确定】，完成创建。

### step 4. 添加现有机器进伸缩组

1. 在 [控制台](https://console.cloud.tencent.com/autoscaling) 单击伸缩组名字，进入管理页，在页面下方单击【添加云主机】。
![](https://mc.qcloudimg.com/static/img/3ff1beba2621d68ef939d7fd0df2de11/5.jpg)

2. 在弹出的对话框中，选择集群已有的服务器加入伸缩组。如果现在是非高峰时期，集群中未充分利用的服务器可以退还，节约成本。
![](https://mc.qcloudimg.com/static/img/be11ceec587195b7cf39f9183a051769/6.jpg)

3. 加入后对服务器设置“免于缩容”，这样在缩容活动中，伸缩组不会选择这台服务器缩容。这样集群中这台机器永远在服务，AS 不会更改它。
![](https://mc.qcloudimg.com/static/img/2c19119e95beb4eb820757939578c656/7.jpg)

### step 5. 设置扩缩容策略（重点！）

AS 支持定时扩容或者基于告警动态扩容，也支持您接收扩缩容通知，以及翻看历史扩缩容详情。一切尽在您的掌控中。
![](https://mc.qcloudimg.com/static/img/f348d96c002cdf79ac2033abcd7e6e4c/8.jpg)

-  **先设置一个20：00的定时扩容任务**
![](https://mc.qcloudimg.com/static/img/0721f68f33dca49f7175d1f4fd3a80aa/t1.jpg)
> 注：
> 腾讯云的CVM需要1分钟左右创建，如果自定义镜像较大，可能需要更多时间。您可以将执行开始时间提早5分钟。

- **然后再设置一个24：00的定时缩容任务**
![](https://mc.qcloudimg.com/static/img/a86e797fa59c66d304837b3017d7bc78/t2.jpg)

至此大功告成！

网站的后台集群变为“1台固定应用服务器+1台高峰时定时创建的应用服务器”。
没加入伸缩组的其他集群机器，大部分时间未充分利用，可以退还掉节约成本。
