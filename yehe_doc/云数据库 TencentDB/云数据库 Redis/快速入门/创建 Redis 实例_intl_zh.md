
本文为您介绍在云数据库 Redis 控制台创建实例和修改实例名的操作。

## 操作步骤
1. 登录 [云数据库 Redis 购买页](https://buy.cloud.tencent.com/redis?regionId=1)，根据您的实际需求选择配置。
<table>
<thead>
<tr>
<th>参数</th>
<th>备注</th>
</tr>
</thead>
<tbody><tr>
<tr>
<td>网络类型</td>
<td>建议选择私有网络，实例购买后支持基础网络转换为 VPC 网络，不支持 VPC 网络转换为基础网络，请参见 <a href="https://intl.cloud.tencent.com/document/product/213/5227" target="_blank">网络环境</a>。</td>
</tr>
<tr>
<td>产品版本</td>
<td>支持内存版，基于开源 Redis 引擎的高性能版本，兼容 Redis 2.8、4.0、5.0。</td>
</tr>
<tr>
<td>兼容版本</td>
<td>兼容 Redis 2.8、4.0、5.0。2.8版暂停售卖，建议您选择4.0及以上版本，如需购买2.8版本请 <a href="https://console.cloud.tencent.com/workorder/category">提交工单</a> 申请。
</td>
</tr>
<tr>
<td>架构版本</td>
<td>支持标准版、集群版。</td>
</tr>
<tr>
<td>副本数量</td>
<td><ul><li>Redis 2.8 标准版支持0 - 1个副本。</li><li>Redis 4.0、5.0 标准版支持1 - 5个副本。</li><li>Redis 4.0、5.0 集群版支持1 - 5个副本。</li></td>
</tr>
<tr>
<td>端口</td>
<td>自定义端口号需在1024到65535之间。</td>
</tr>
<tr>
<td>指定项目/安全组</td>
<td>指定数据库的项目和安全组。</td>
</tr>
<tr>
<td>实例名/设置密码</td>
<td>实例名和密码支持直接设置和创建完后在实例列表进行设置。</td>
</tr>
</tbody></table>

3. 确认无误后单击【立即购买】，各版本详细价格请参见 [产品定价](https://intl.cloud.tencent.com/document/product/239/9894)。
4. 购买完成后返回实例列表，待实例状态显示为“运行中”，即可正常使用。
5. （可选）修改实例名，在实例列表的“实例 ID / 名称”列，单击以下小图标可修改实例名。
![](https://main.qcloudimg.com/raw/8a6917c05adb4e06731dbdd836c620da.png)

## 后续步骤
- 使用云服务器 CVM 直接访问云数据库的内网地址，请参见 [连接 Redis 数据库（内网）](https://intl.cloud.tencent.com/document/product/239/9897)。
- 通过具备外网 IP 的云服务器 CVM 进行端口转发，来实现外网连接 Redis 实例，请参见 [连接 Redis 数据库（外网）](https://intl.cloud.tencent.com/document/product/239/35905)。
