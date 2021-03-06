### 云服务器与云数据库部署在同一区域上，如何连接 Redis？
云服务器与云数据库部署在同一区域上时，使用内网访问，请参见 [连接数据库实例](https://intl.cloud.tencent.com/document/product/239/9897)。

### 云服务器与云数据库部署在不同区域上，如何连接 Redis？
基础网络和私有网络互通，请参见 [基础网络互通](https://intl.cloud.tencent.com/document/product/215/31807)。
私有网络之间互通，请参见 [对等连接](https://intl.cloud.tencent.com/document/product/553/18827)。

### 如何处理云数据库 Redis 无法 ping 通？ 
Redis 默认禁`ping`，可以使用 telnet 来检测连通性。

### 如何开通 Redis 的外网访问？ 
云数据库 Redis 暂时不支持外网地址。如需通过外网访问，可使用带有外网的云服务器通过 [Iptable 代理](https://intl.cloud.tencent.com/document/product/239/35905) 的方式来实现。
>iptable 转发的方式存在稳定性风险，不建议在生产环境使用外网接入。
