## 命名空间
Namespace=QCE/CKAFKA

## 监控指标

| 指标英文名              | 指标中文名 | 指标含义 | 单位   | 维度                     |
| ------------------------ | ----------- | ---- | ---------------------- | ---------------------- |
| InstanceMsgHeap        | 占用磁盘容量 | 实例磁盘占用量（包含副本），按照所选择的时间粒度取最新值 | MB    | instanceId                |
| InstanceProCount   | 生产消息条数 | 实例的实际生产消息条数，按照所选择的时间粒度统计求和。 | 条    | instanceId                |
| InstanceConCount      | 消费条数 | 实例消费消息条数，按照所选择的时间粒度统计求和 | 次    | instanceId                |
| InstanceProReqCount | 生产请求数 | 实例级别生产请求次数，按照所选择的时间粒度统计求和 | 次    | instanceId                |
| InstanceConReqCount  | 消费请求数 | 实例级别消费请求次数，按照所选择的时间粒度统计求和 | 次   | instanceId                |
| InstanceMsgCount      | 落盘消息条数 | 实例落盘的消息总条数（不包含副本），按照所选择的时间粒度取最新值 | 条   | instanceId             |
| InstanceProFlow       | 生产流量 | 实例生产流量（不包含副本产生的流量），按照所选择的时间粒度统计求和 | MB/min    | instanceId   |
| InstanceConFlow        | 消费流量 | 实例消费流量（不包含副本产生的流量），按照所选择的时间粒度统计求和 | MB/min    | instanceId   |
| InstanceDiskUsage       | 磁盘使用百分比 | 当前磁盘占用与实例规格磁盘总容量的百分比 |无，该指标含义为当前磁盘使用容量与磁盘总容量比值|instanceId|
| InstanceMaxConFlow      | 消费峰值带宽 | 实例消费消息峰值带宽（消费时无副本的概念） | MB/s | instanceId |
| InstanceMaxProFlow      | 生产峰值带宽 | 实例生产消息峰值带宽（不包含副本生产的带宽） | MB/s | instanceId |

>每个指标的统计粒度（Period）可取值不一定相同，可通过 [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) 接口获取每个指标支持的统计粒度。

## 各维度对应参数总览

| 参数名称               | 维度名称             | 维度解释          | 格式                            |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name  | instanceId              | ckafka 实例的维度名称    | 输入 String 类型维度名称：instanceId        |
| Instances.N.Dimensions.0.Value | instanceId              | ckafka 实例的具体 ID    | 输入实例具体 ID，例如：ckafka-test |

## 入参说明

查询消息队列实例监控数据，入参取值如下：
&Namespace=QCE/CKAFKA
&Instances.N.Dimensions.0.Name=instanceId
&Instances.N.Dimensions.0.Value=实例 ID 

