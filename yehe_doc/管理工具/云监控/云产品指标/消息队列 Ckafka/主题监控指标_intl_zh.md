## 命名空间

Namespace=QCE/CKAFKA

## 监控指标

| 指标英文名                  | 指标中文名     | 单位   | 维度                     |
| ------------------------ | ----------- | ---- | ---------------------- |
| CtopicProFlow        | 主题生产流量    | MB    | instanceId,topicId    |
| CtopicConFlow   |主题消费流量  | MB    | instanceId,topicId    |
| CtopicMsgHeap      |主题落磁盘消息数量 | MB    | instanceId,topicId    |
| CtopicProCount | 主题生产消息数量 | 条    | instanceId,topicId            |
| CtopicProReqCount       | 主题生产请求次数    | 次    | instanceId,topicId    |
| CtopicConReqCount   |主题消费请求次数  | 次    | instanceId,topicId    |
| CtopicMsgCount      |主题落磁盘消息数 | 条    | instanceId,topicId    |
| CtopicConCount | 主题消费消息数量 | 条    | instanceId,topicId            |

>每个指标的统计粒度（Period）可取值不一定相同，可通过 [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) 接口获取每个指标支持的统计粒度。

## 各维度对应参数总览

| 参数名称               | 维度名称             | 维度解释          | 格式                            |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name  | instanceId              | ckafka 实例 ID 的维度名称   | 输入 String 类型维度名称：instanceId       |
| Instances.N.Dimensions.0.Value | instanceId              | ckafka 具体实例的 ID | 输入实例具体 ID，例如：ckafka-test |
| Instances.N.Dimensions.1.Name  | topicId            | 实例所在主题 ID 的维度名称 | 输入 String 类型维度名称：topicId   |
| Instances.N.Dimensions.1.Value | topicId            | 实例所在主题的具体主题 ID | 输入主题具体 ID，例如：topic-test       |

## 入参说明

查询消息队列主题监控数据，入参取值如下：
&Namespace=QCE/CKAFKA
&Instances.N.Dimensions.0.Name=instanceId
&Instances.N.Dimensions.0.Value=实例 ID
&Instances.N.Dimensions.1.Name=topicId
&Instances.N.Dimensions.1.Value=主题 ID 

