在使用 NAT 网关时，您需要注意以下几点：
- 用户删除 NAT 网关会解除其弹性 IP 地址的关联，但不会从用户帐号释放该弹性 IP 地址。

- 用户不能为 NAT 网关关联安全组，但可以为私有子网中的实例绑定安全组，以控制进出这些实例的流量。

- 用户无法直接使用网络 ACL 控制进出 NAT 网关的流量，但可以使用网络 ACL 控制进出 NAT 网关所关联子网的流量。

- 用户无法通过 VPC 对等连接、VPN 连接或专线接入将流量路由到 NAT 网关，因为此类连接另一端的资源不能使用 NAT 网关。
例如，VPC 1 发往 Internet 的流量都可通过 NAT 网关实现， VPC 1 和 VPC 2 建立了对等连接，VPC 2 中所有的资源可访问 VPC 1 中的所有资源，但 VPC 2 中的所有资源不可以通过 NAT 网关访问 Internet。

- NAT 网关支持 TCP、UDP 和 ICMP 协议，而 GRE 隧道和 IPSec 使用的 ESP、AH 无法使用 NAT 网关，且暂不支持 ALG 相关技术。这是由 NAT 网关本身的特性决定的，与服务提供商无关。但互联网大部分应用都是 TCP 应用，TCP 和 UDP 应用合起来占互联网应用类型的99%。

- NAT 网关支持的资源限制如下表所示：<!--，您还可以查看 [VPC 其它产品的使用限制](https://cloud.tencent.com/doc/product/215/537)-->
<table>
<tbody>
<tr>
<th >资源</th>
<th >限制</th>
</tr>
<tr>
<td >每个 VPC 支持的 NAT 网关数</td>
<td >3 个</td>
</tr>
<tr>
<td >每个 NAT 网关支持弹性 IP 个数</td>
<td >10</td>
</tr>
<tr>
<td >每个 NAT 网关最多支持转发能力</td>
<td >5 Gbps</td>
</tr>
<tr>
<td >每个 NAT 网关的最大端口转发条数</td>
<td >200</td>
</tr>
</tbody></table>
