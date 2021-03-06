## 操作场景
本文介绍如何向已创建的边缘集群中添加节点。


## 前提条件
按照以下条件准备好边缘节点：
- 节点来源：可使用 [云服务器控制台](https://console.cloud.tencent.com/cvm) 或 [边缘计算机器控制台](https://console.cloud.tencent.com/ecm/instance) 中已有的服务器、其他平台或自建机房的服务器。
- 节点处理器：支持 x86_64 处理器。 
- 支持的节点操作系统如下：
 - Ubuntu 18.04/16.04
 - CentOS 7.6/7.5/7.4
 - Tencent Linux Release 2.4/2.2 (Final)
 -  SUSE Linux Enterprise Server 12 SP3
 -  Debian 9.0
- 请确保需添加节点已安装 `wget`、`systemctl` 及 `iptable`。
- 节点网络需具备主动访问公网能力。

## 操作步骤
1. 登录 [腾讯云容器服务控制台](https://console.cloud.tencent.com/tke2)，选择左侧导航栏中的【边缘集群】。
2. 在“边缘集群”列表页面，选择集群 ID 进入集群 “Deployment” 管理页面。
3. 选择左侧菜单栏中的【节点管理】>【节点】，进入“节点列表”页面。
4. 在“节点列表”页面中，单击【添加节点】。
5. 在弹出的“添加节点”窗口中，按照以下步骤进行配置，得到节点侧初始化脚本。
   1. 在“配置”步骤中，获取初始配置，并可修改以下参数值：
      - **Interface**：节点内网通信使用的网卡。
      - **NodeName**：节点在集群中的名称，需确保该名称在集群内的唯一性。
   2. 单击【下一步：安装】，若提示需开启集群外网访问功能，则单击<img src="https://main.qcloudimg.com/raw/fd1ae3941057881ca71bcf8b2874b510.png" style="margin:-6px 0px">进行开启。如下图所示：
![](https://main.qcloudimg.com/raw/07bd1050fa0ea9677f2fed954a74666d.png)
   3. 在“安装”步骤中，复制脚本下载命令用来获取到对应的节点初始化脚本。
4. 登录已准备好的服务器，并切换至 `root` 帐户执行已复制的命令。
5. 依次执行以下命令，运行初始化节点脚本。
```
chmod +x script.sh
```
```
./script.sh
```
6. 脚本执行成功后，稍后前往“节点列表”页面并刷新，即可查看已新增的节点。
您还可进行节点的其他操作，例如驱逐、移出、封锁、编辑标签或取消封锁等。

## 相关操作
### 关闭集群外网访问<span id="OpenExtranetAccess"></span>
1. 在“边缘集群”列表页面，单击需关闭外网访问集群所在行右侧的【查看集群凭证】。
2. 在弹出的“集群凭证”窗口中，单击“外网访问”中的<img src="https://main.qcloudimg.com/raw/84c11b68fbbd46c46c2cae68d45baee2.png" style="margin:-6px 0px">，即可关闭该集群的外网访问。
