### 定价

 后付费的 CKafka 定价主要取决于以下两个因素：分别是单个吞吐量 Unit 以及百万消息条数。其价格如下： 

- 吞吐量Unit（1MB/s）:  0.36 USD/day
- 百万消息条数：0.028 USD per 1,000,000 messages （此处仅显示精确到小数点后三位的产品价格，准确价格请以参考账单。）

## 预付费价格

消息队列 CKafka 可以按实例的形式售卖，采用**包年包月-预付费**的计费形式。

当前消息队列 CKafka 根据**峰值吞吐性能**及**磁盘容量**，标准版分为入门型、标准型和独占型等9种实例类型，支持单独扩容磁盘。
消息队列 CKafka 计费方式灵活实惠，仅需测算业务所需性能和磁盘容量，按需购买即可。提供的实例都是多节点集群模式部署，用户无需关心底层部署，就可以拥有高可靠高可用的服务。

>
- 吞吐量指出入带宽，40MB吞吐指出和入的带宽峰值为40MB。考虑实例的副本个数，需要均分吞吐量。例如，客户要求40MB吞吐、3副本，则需要购买120MB/s的吞吐带宽。
- 会影响消息队列 CKafka 数据可靠性的几种情况，请参考 [CKafka 数据可靠性说明](https://intl.cloud.tencent.com/document/product/597/31586)。
- 非独占型实例不能直接升配为独占型实例，请参考 [迁移数据到 CKafka](https://intl.cloud.tencent.com/document/product/597/17272)。如需独占型实例，请联系商务经理或 [提交工单](https://console.cloud.tencent.com/workorder/category?level1_id=876&level2_id=951&source=0&data_title=%E6%B6%88%E6%81%AF%E9%98%9F%E5%88%97%20CKafka&level3_id=955&radio_title=%E9%85%8D%E9%A2%9D%E6%8F%90%E5%8D%87%E7%94%B3%E8%AF%B7&queue=81&scene_code=18356&step=2)处理


<span id="standard"></span>
### 标准版实例价格

| 实例类别  | 峰值吞吐量（MB/s） | 磁盘容量（GB）| 实例级别 Topic 数|实例级别 partition 数|价格（USD/月）|
|---------|---------|-----|------|--------|------|
| 入门型 | 40 | 300 | 25| 60 |870 |
| 标准型 | 100 |1000 | 40 | 100 |1510 |
| 进阶型 |  150 |2500 | 50 | 150|1920 |
| 容量型 |  180 |4000 | 150| 300|2330 |
| 高阶型L1 |  300 |6000 | 250| 500|2740 |
| 高阶型L2 |  400 |6000 | 250| 500|3970 |
| 高阶型L3 |  600 |6000 | 350| 600|5170 |
| 高阶型L4 |  900 |9000 | 450| 700|7030 |
| 独占型|  1200 |24000 | 1000| 1500|13900 |

>- 单 Topic 支持的 partition 数量限制为24个。
- 实例级别 Consumer Group 默认限制个数为50个。
- 实例级别的 paritition 限制包含了副本数。例如，一个实例下有1个双副本、4分区的 Topic、 2个3副本、3分区的 Topic，则该实例的总 partition 个数为 （1 × 2 × 4）+（2 × 3 × 3）= 26个。
- Consumer Group 空闲存活时间为7天。
- 如需更高规格的消息队列 CKafka 实例，请联系商务经理或 [提交工单](https://console.cloud.tencent.com/workorder/category)处理。

### 单独扩容磁盘价格
| 实例类别  | 磁盘容量（GB）| 价格（USD/月）|
|---------|-----|------|
|非独占性-扩磁盘|100|8|