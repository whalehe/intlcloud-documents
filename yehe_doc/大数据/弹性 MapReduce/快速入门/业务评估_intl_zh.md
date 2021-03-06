## 选择集群类型
EMR 集群提供三种集群类型，可根据实际业务需要选择集群类型：
- **Hadoop 集群：**提供了 hadoop、Hbase、Hive、Spark、flink、presto 等开源大数据组件，主要应用于离线数据分析、实时数据分析、Ad hoc 等大数据处理场景。
- **ClickHouse 集群：**提供了开源列式数据库 ClickHouse 组件，主要应用于结构良好清晰且不可变的事件或日志流分析场景。
- **Druid 集群：**提供了分布式时序数据库 Druid 组件，主要应用于大量的基于时序的数据聚合查询的场景。

## 选择计费模式
EMR 集群提供的计费模式：
- **按量计费集群：**集群的全部节点计费模式均为按量计费，适用于短时间存在或周期性存在的集群。

节点类型介绍，请参见 [节点类型说明](https://intl.cloud.tencent.com/document/product/1026/31094)。

## 选择机型规格
EMR 提供了多种云服务器机型，包括 EMR 标准型、EMR 计算型、EMR 高 IO 型、EMR 内存型及 EMR 大数据型（若您需要黑石机型，请 [提交工单](https://console.cloud.tencent.com/workorder/category) 联系我们）。
>
>- Hadoop 集群和 Druid 集群在高可用（HA）下节点最小节点数为8个，包含2个 Master 节点，3个 Common 节点，最少3个 Core 节点。非高可用（HA）下存储为单副本，可作为测试使用，不建议作为生产环境，最小节点数为3个，包含1个 Master 节点，最少2个 Core 节点。
>- Clickhouse 集群在高可用（HA）下节点最小节点数为5个，包含2个 core 节点，3个 Common 节点。非高可用（非 HA）下，存储为单副本，可作为测试使用，不建议作为生产环境，最少1个 core 节点。

您可以根据自身的业务需要及成本考量，进行机型的选择。
- 如您对离线计算的时延有一定的要求，我们建议您选择本地盘或大数据机型。
- 如您需要使用实时数据库 Hbase，我们建议您选择 EMR 高 IO 型，并选择本地 SSD 盘，以实现最高的性能。

### 节点规格推荐
<table>
   <tr>
      <th width=13%>节点类型</th>
      <th width=17%>集群类型</th>
      <th width=70%>推荐规格</th>
   </tr>
   <tr>
      <td rowspan="3">Master 节点</td>
      <td>Hadoop 集群</td>
      <td>Master 节点建议选择内存较大的实例规格，推荐内存大小至少8G。磁盘建议选择云盘可以让集群获得更高的稳定性。</td>
   </tr>
   <tr>
      <td>ClickHouse 集群</td>
      <td>-</td>
   </tr>
   <tr>
      <td>Druid 集群</td>
      <td>Master 节点建议选择内存较大的实例规格，推荐内存不低于16G。磁盘推荐使用 SSD 盘，可以获得更好的 IO 性能。</td>
   </tr>
	    <tr>
      <td rowspan="3">Core 节点</td>
      <td>Hadoop 集群</td>
      <td><li>若您的大部分数据在 COS 对象存储上，Core 节点与 Task 节点的功能则类似，大小不少于500G。<strong>Core 节点不具备弹性功能。</strong>
<li>若您的架构未使用 COS 对象存储，则 Core 节点负责集群的计算与存储任务，EMR 默认开启三备份，在做数据盘大小预估时需考虑三备份空间，推荐使用大数据机型。
</td>
   </tr>
   <tr>
      <td>ClickHouse 集群</td>
      <td>Core 节点建议选择 CPU 和内存较高的机型，由于本地磁盘遇到坏盘情况存在数据丢失风险，磁盘建议选择云硬盘。</td>
   </tr>
   <tr>
      <td>Druid 集群</td>
      <td>Core 建议选择内存较大的实例规格，推荐内存不低于16G。磁盘建议选用 SSD 盘，可以获得更好的 IO 性能。</td>
   </tr>
	 <tr>
	 <td rowspan="3">Task 节点</td>
      <td>Hadoop 集群</td>
      <td><li>若您的架构未使用 COS 对象存储，则可以不使用 Task 节点。
<li>若您的大部分数据在 COS 对象存储上，则 Task 节点可用作弹性计算资源，按需获取。
</td>
   </tr>
   <tr>
      <td>ClickHouse 集群</td>
      <td>-</td>
   </tr>
   <tr>
      <td>Druid 集群</td>
      <td><li>若您的架构未使用 COS 对象存储，则可以不使用 Task 节点。
<li>若您的大部分数据在 COS 对象存储上，则 Task 节点可用作弹性计算资源，按需获取。
</td>
   </tr>
	 <tr>
	 <td rowspan="3">Common 节点</td>
      <td>Hadoop 集群</td>
      <td>Common 节点主要做 zk 节点使用，建议选择2C4G云盘100G的规格即可满足需求。</td>
   </tr>
   <tr>
      <td>ClickHouse 集群</td>
      <td>Common 节点建议 CPU 和内存最小配置不低于4C16G。</td>
   </tr>
   <tr>
      <td>Druid 集群</td>
      <td>Common 节点主要做 zk 节点使用，建议选择2C4G云盘100G的规格即可满足需求。</td>
   </tr>
	 <tr>
	 <td rowspan="3">Router 节点</td>
      <td>Hadoop 集群</td>
      <td>Router 节点主要用于缓解主节点负载和用作任务提交机，因此建议选择较大内存的机型，最好不低于 Master 规格。</td>
   </tr>
   <tr>
      <td>ClickHouse 集群</td>
      <td>-</td>
   </tr>
   <tr>
      <td>Druid 集群</td>
      <td>Router 节点主要用于缓解主节点负载和用作任务提交机，因此建议选择较大内存的机型，最好不低于 Master 规格。</td>
   </tr>
</table>

## 网络及安全
为保证集群的网络安全，EMR 集群将会被放置在一个 VPC 中，我们会给该 VPC 增加一个安全组策略。同时，为了保证 Hadoop 软件的 WebUI 能够便捷访问，我们为其中一个 Master 节点开启了外网 IP，采用按照流量计费的模式；Router 节点默认不开通外网 IP，如需开通，可以在 [CVM 控制台](https://console.cloud.tencent.com/cvm/eip) 自由绑定弹性公网 IP。
>
>- Master 节点在创建集群时默认开启外网 IP，但用户可根据情况选择不开启外网 IP。
- 开启集群 Master 节点公网，主要用于 ssh 登录和组件 WebUI 查看。
- 主节点 Master 节点会开启外网，按流量付费，带宽上限为5M。创建集群后，您可在控制台对该网络进行调整。
