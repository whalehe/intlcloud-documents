## 命名空间
Namespace=QCE/CDN

## 监控指标

| 指标英文名 | 指标中文名 | 单位   |维度|
| ---------------- | ---- | ---- |  ---- |
| Bandwidth        | 带宽   | Mbps  | projectId、domain   |
| Requests         | 请求数  | 次   | projectId、domain   |
| BackOriginBandwidth | 回源带宽 | Mbps | projectId、domain   |
| BackOriginFailRate | 回源失败率 | % |projectId、domain   |
| BackOriginFlux | 回源流量 | GB |projectId、domain   |
| BackOriginSpeed | 回源速率 | KB/s |projectId、domain   |
| Flux | 流量 | GB |projectId、domain   |
| RequestsHitRate | 请求命中率 | % | projectId、domain   |

>每个指标的统计粒度（Period）可取值不一定相同，可通过 [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) 接口获取每个指标支持的统计粒度

## 各维度对应参数总览

| 参数名称               | 维度名称      | 维度解释 | 格式                     |
| ------------------ | --------- | ---- | ---------------------- |
| Instances.N.Dimensions.0.Name  | projectId | 项目维度名称 | 输入String 类型维度名称：projectId |
| Instances.N.Dimensions.0.Value | projectId | 项目具体ID | 输入项目具体 ID，例如：1         |
| Instances.N.Dimensions.0.Name  | domain    | 域名维度名称 | 输入String 类型维度名称：domain |
| Instances.N.Dimensions.0.Value | domain    | 具体域名 | 输入具体域名，例如：`www.qq.com`  |

## 入参说明

查询内容分发网络监控数据，入参取值如下：
&Namespace= QCE/CDN
&Instances.N.Dimensions.0.Name=projectId
&Instances.N.Dimensions.0.Value 为项目 ID
&Instances.N.Dimensions.1.Name=domain
&Instances.N.Dimensions.1.Value 为域名 



