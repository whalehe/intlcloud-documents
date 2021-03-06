## 操作场景 
由云数据库 MongoDB 的架构所决定，重启实例分为重启 Mongos 和重启  Mongod 两部分。由于重启实例会造成连接闪断，特别是重启 Mongod 时，如果有数据写入可能会造成 rollback，进而丢失数据。
重启期间，云数据库 MongoDB 实例将无法提供正常服务，请提前做好准备，以免对业务造成影响。目前，重启 Mongod 处于白名单控制，需 [提交工单](https://console.cloud.tencent.com/workorder/category) 联系我们。重启属高危操作，请谨慎处理。

## 操作步骤 
1. 登录 [MongoDB 控制台](https://console.cloud.tencent.com/mongodb)，进入副本集或者分片实例列表。
2. 勾选需要重启的实例，在上方单击【重启】，或在实例的操作列选择【更多】>【重启】。
3. 在弹出的对话框，勾选需要重启的组件，单击【确认】，等待任务完成即可。
