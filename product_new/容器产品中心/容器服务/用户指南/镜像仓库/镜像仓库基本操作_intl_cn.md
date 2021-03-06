## 操作场景
镜像仓库用于存放 Docker 镜像，Docker 镜像用于部署容器服务，每个镜像有特定的唯一标识（镜像的 Registry 地址+镜像名称+镜像 Tag）。目前镜像支持 Docker Hub 官方镜像和用户私有镜像。

## 操作步骤

### 开通镜像仓库
>首次使用镜像仓库的用户，需要先开通镜像仓库。
>
1. 登录容器服务控制台，选择左侧导航栏中的【镜像仓库】>【[我的镜像](https://console.cloud.tencent.com/tke2/registry/user/self)】。
2. 根据以下提示填写相关信息，并单击【开通】进行初始化。
 - **用户名**：默认是当前用户的账号，是您登录到腾讯云 docker 镜像仓库的身份。
 - **密码**：是您登录到腾讯云 docker 镜像仓库的凭证。

### 创建命名空间
1. 选择左侧导航栏中的【镜像仓库】>【[我的镜像](https://console.cloud.tencent.com/tke2/registry/user/self)】，进入“我的镜像”页面。
2. 在“我的镜像”页面中，选择【命名空间】页签并单击【新建】。
3. 在弹出的“新建命名空间”窗口中，输入命名空间名并单击【提交】。如下图所示：
>?命名空间名称全局唯一，若您希望使用的命名空间名称已被其他用户使用，请尝试其他适用的命名空间名称。
>


### 创建镜像
1. 选择左侧导航栏中的【镜像仓库】>【[我的镜像](https://console.cloud.tencent.com/tke2/registry/user/self)】，进入“我的镜像”页面。
2. 在“我的镜像”页面，单击镜像列表页上方的【新建】。
2. 输入镜像名称和描述，然后【提交】。
>?命名空间将用于分类容器镜像，也是您创建的私人镜像地址的前缀，本文以 `tkefiletest` 为例。
>

### 推送镜像到镜像仓库
#### 登录到腾讯云 registry
1. 在终端替换以下命令中的相关信息并执行，登录腾讯云 registry。
```
$ sudo docker login --username=[username] ccr.ccs.tencentyun.com
```
**username**：腾讯云账号，开通时已注册。
2. 输入密码后即登录完成。

#### 上传镜像
根据以下提示替换命令中的相关信息并执行，上传镜像。
```
$ sudo docker tag [ImageId] ccr.ccs.tencentyun.com/[namespace]/[ImageName]:[镜像版本号]
$ sudo docker push ccr.ccs.tencentyun.com/[namespace]/[ImageName]:[镜像版本号]
```
- **ImageId 和镜像版本号**：根据已有镜像信息补充。
- **namespace**：开通镜像仓库时填写的命名空间。
- **ImageName**：在控制台创建的镜像名称。


#### 下载镜像
1. 执行以下命令登录到镜像仓库，需输入在 [开通镜像仓库](#create) 中已设置的密码。
```
$ sudo docker login --username=[username] ccr.ccs.tencentyun.com
```
2. 替换命令中的相关信息并执行，下载镜像。
```
$ sudo docker pull ccr.ccs.tencentyun.com/[namespace]/[ImageName]:[镜像版本号]
```

### 删除镜像
1. 选择左侧导航栏中的【镜像仓库】>【[我的镜像](https://console.cloud.tencent.com/tke2/registry/user/self)】，进入“我的镜像”页面。
2. 在“我的镜像”页面，选择需删除镜像所在行右侧【删除】。
3. 在弹出的“删除镜像仓库”窗口中，单击【确定】即可**删除该镜像所有版本**。
