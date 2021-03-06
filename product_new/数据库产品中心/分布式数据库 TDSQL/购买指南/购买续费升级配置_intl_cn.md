## 实例购买
登录 [分布式数据库 TDSQL 控制台](https://console.cloud.tencent.com/dcdb)，单击【新建】购买实例。实例最多一次性购买64个分片，超过64个分片需 [提交工单](https://console.cloud.tencent.com/workorder/category)。
实例购买后，需初始化实例方可正常运行。

## 实例升级
实例升级操作指将现有 TDSQL 实例的规格升级到更高规格，然而因分布式数据库是由多个分片组成，因此其实例升级有“新增分片，扩容分片”两种方案，升级过程中服务不会终止，但某些分片会发生若干秒的只读现象，建议您在低峰期进行升级。

### 新增分片
1. 在 TDSQL 控制台，单击实例名或操作列的【管理】，进入实例管理页面。
![](https://main.qcloudimg.com/raw/2d971c5208429a4fcd5620bfd8e9c8a0.png)
2. 选择【分片管理】页，在操作列单击【新增分片】，在弹出的对话框选择新增分片的规格和数量，即可升级。
![](https://main.qcloudimg.com/raw/d9a2e9b9261b3252a0db00472b1c3c92.png)

### 扩容分片
扩容分片指不增加分片数量，但将单个分片的规格扩容到更大。
进入实例管理页面，选择【分片管理】页，在操作列单击【扩容分片】，即可升级。
![](https://main.qcloudimg.com/raw/4e28cc10867d73661ed688ba3240fe18.png)

**升级费用=（目标规格单价-原规格单价）x 剩余到期时间**

