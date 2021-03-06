机器组是腾讯云日志服务中 LogListener 所采集日志的服务器对象，通过机器组的方式来配置 LogListener 采集日志的服务器。一般而言，根据不同业务场景来划分不同的机器组，可以方便您管理日志服务。

## 创建机器组

通过日志服务控制台可以快速创建机器组，具体操作步骤如下：

1. 登录 [日志服务控制台](https://console.cloud.tencent.com/cls)。
2. 在左侧导航栏中，单击【机器组管理】。
3. 选择您日志服务所在的地域，例如广州，单击【创建机器组】。
4. 选择配置机器组方式，目前 CLS 支持两种方式配置机器组：[机器 IP](#.E6.9C.BA.E5.99.A8-ip-.E9.85.8D.E7.BD.AE.E6.9C.BA.E5.99.A8.E7.BB.84) 或 [机器标识](#.E6.9C.BA.E5.99.A8.E6.A0.87.E8.AF.86.E9.85.8D.E7.BD.AE.E6.9C.BA.E5.99.A8.E7.BB.84)。  

#### 机器 IP 配置机器组
填写机器组名称及其服务器对应的 IP 地址，确认信息无误后，单击【确认】，即可完成机器组创建。
<img src="https://main.qcloudimg.com/raw/3d6119154a2ad3d482bba23b584250ba.png" width="80%">
> !
> - 每行填写一个 IP 地址，暂不支持 Windows 系统机器。
> - 同园区内，腾讯云服务器填写内网 IP 即可，分行隔开。

#### 机器标识配置机器组
如果您的机器 IP 地址经常变动，利用机器 IP 配置机器组操作繁琐，每次 IP 变更将需要修改对应的机器组配置。CLS 支持利用机器标识动态配置机器组，您只需在 Loglistener 的配置信息中填入机器标识，CLS 即可识别并自动将机器添加至机器组。
> !
> - 机器标识配置机器组仅 Loglistener 2.3 及以上版本支持，低版本的 Loglistener 需手动更新，详情可参见 [手动更新 LogListener](https://intl.cloud.tencent.com/document/product/614/17414) 指引。
> - 每行填写一个标识名称，暂不支持识别 Windows 系统的机器。

1. 填写机器组名称及其机器标识，确认信息无误后，单击【确认】，完成机器组创建。
<img src="https://main.qcloudimg.com/raw/749bc422544156ee5f4f7acf7389de84.png" width="80%">
2. 登录目标机器，修改 Loglistener 安装目录下的`/etc/loglistener.conf`文件。此处安装目录以`/user/local`为例：
```plaintext
vi /usr/local/loglistener-2.3.0/etc/loglistener.conf
```
3. 键盘按 **i** 键，进入编辑模式。
4. 修改配置文件中 group_label 部分，填入用户自定义机器标识，多个标识以逗号分割。
<img src="https://main.qcloudimg.com/raw/1d17d38a70cdfbfb963a60fbec3b0c1b.png" width="80%">
5. 保存设置并退出编辑器，具体操作步骤：按 **Esc** 键，输入 **:wq**，按 **Enter** 键。
6. 执行如下命令，重启 Loglistener。
```plaintext
/etc/init.d/loglistenerd restart
```


## 查看机器状态

机器组与日志服务系统之间采用心跳机制保持连接，成功安装过 LogListener 的机器组会定时向日志服务发送心跳。

1. 您可以通过单击【查看】，查看机器组的状态来识别当前该机器是否工作正常。
   ![](https://main.qcloudimg.com/raw/4163e320b011c1593c345b80cb52e0ed.png)
2. 若状态显示为正常，则说明您的服务器可以与腾讯云日志服务正常通信。
   ![](https://main.qcloudimg.com/raw/f3c7d75d5282758fadecded57bdedb1a.png)

## 删除机器组

1. 登录 [日志服务控制台](https://console.cloud.tencent.com/cls)。
2. 选择需要删除的机器组，单击【删除】。
   ![](https://main.qcloudimg.com/raw/a5499d33aa8c2323697388334dc27584.png)
3. 单击【确认】，完成机器组删除。
   ![](https://main.qcloudimg.com/raw/e99130ce78d418e04c4f573fbcd112d0.png)

> !机器组一旦删除，所关联的日志主题将无法继续采集日志。
