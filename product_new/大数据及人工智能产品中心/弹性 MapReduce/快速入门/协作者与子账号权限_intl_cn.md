您可以在控制台中对各协作者/子账号进行权限授权，授权方法请参见 [访问管理](https://intl.cloud.tencent.com/document/product/598/10602)。

目前 EMR 提供了3种权限角色，您可以在 [访问管理控制台](https://console.cloud.tencent.com/cam/overview) 的策略页中搜索 EMR 关键字进行查找。

| 角色 | 权限| 
|---------|---------|
| QcloudEMRObserverAccess（观察者访问权限）	| 组件配置信息获取接口。<br>监控信息接口。<br>节点信息获取接口。<br>获取集群列表 。|
| QcloudEMROperationAccess（运维访问权限）	| 继承观察者权限。<br> 修改参数，下发配置。<br>重启服务。<br>更改密码。 |
| QcloudEMRAdministratorAccess（管理员权限）| 继承运维访问权限。<br>扩容。<br>缩容。<br>创建新集群。<br>销毁集群。<br>更改密码 。|
