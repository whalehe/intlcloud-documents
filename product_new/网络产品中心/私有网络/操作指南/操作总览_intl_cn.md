您在使用私有网络时，可能碰到诸如创建私有网络、更改子网关联路由表、创建弹性网卡、绑定和解绑 HAVIP 等问题。本文将介绍使用私有网络以及与其相关产品的常用操作，供您参考。

## 私有网络和子网
[私有网络和子网](http://intl.cloud.tencent.com/document/product/215/4927) 的关系如下：子网是 VPC 内的 IP 地址块，私有网络中的所有云资源都必须部署在子网内。子网具有可用区属性，创建 VPC后，您可以在私有网络所属地域的每个可用区中添加子网。下面将介绍使用私有网络和子网及与其相关产品的常用操作，供您参考。
- [创建私有网络](https://intl.cloud.tencent.com/document/product/215/31798)
- [新增子网](https://intl.cloud.tencent.com/document/product/215/31799)
- [查看私有网络内的所有资源](https://intl.cloud.tencent.com/document/product/215/31802)
- [删除私有网络](https://intl.cloud.tencent.com/document/product/215/31804)
- [删除子网](https://intl.cloud.tencent.com/document/product/215/31805)

更多操作，请参见 [私有网络和子网操作概述](https://intl.cloud.tencent.com/document/product/215/31796)。

## 路由表
[路由表](https://intl.cloud.tencent.com/document/product/215/4954) 由一系列路由策略组成，用于控制私有网络内子网的出流量走向。腾讯云上的路由表有默认路由表和自定义路由表。每个子网都必须关联一个路由表，每个路由表可以关联多个子网。下面将介绍使用路由表及与其相关产品的常用操作，供您参考。

- [修改默认路由表](https://intl.cloud.tencent.com/document/product/215/31812)
- [创建自定义路由表](https://intl.cloud.tencent.com/document/product/215/31811)
- [删除自定义路由表](https://intl.cloud.tencent.com/document/product/215/31814)
- [更改子网关联路由表](https://intl.cloud.tencent.com/document/product/215/31813)

## 弹性网卡
[弹性网卡](https://intl.cloud.tencent.com/document/product/576) 是绑定私有网络内云服务器的一种弹性网络接口，可在多个云服务器间自由迁移，对配置管理网络与搭建高可靠网络方案有较大帮助。您可以在云服务器上绑定多个弹性网卡，实现高可用网络方案；也可以在弹性网卡上绑定多个内网 IP，实现单主机多 IP 部署。下面将介绍使用弹性网卡及与其相关产品的常用操作，供您参考。

- [查看弹性网卡](http://intl.cloud.tencent.com/document/product/576/18533)
- [创建弹性网卡](http://intl.cloud.tencent.com/document/product/576/18534)
- [绑定和配置弹性网卡](http://intl.cloud.tencent.com/document/product/576/18535)
- [删除弹性网卡](http://intl.cloud.tencent.com/document/product/576/18536)
- [解绑云服务器](http://intl.cloud.tencent.com/document/product/576/18537)

## 高可用虚拟 IP
[高可用虚拟 IP](https://intl.cloud.tencent.com/document/product/215/31790) 是一个浮动的内网 IP，支持机器通过 ARP 宣告进行绑定，更新 IP 和 MAC 地址的映射关系。在高可用部署（如 keepalived）场景下，该 IP 可从 主服务器切换至备服务器，从而完成业务容灾。下面将介绍使用高可用虚拟 IP 及与其相关产品的常用操作，供您参考。

- [创建 HAVIP](https://intl.cloud.tencent.com/document/product/215/31818)
- [绑定和解绑 HAVIP](https://intl.cloud.tencent.com/document/product/215/31819)
- [释放 HAVIP](https://intl.cloud.tencent.com/document/product/215/31820)

## 访问 Internet
### 公网网关
[公网网关](https://intl.cloud.tencent.com/document/product/215/4972) 是开启了转发功能的云服务器。没有外网 IP 的云服务器，可通过位于不同子网的公网网关访问 Internet。公网网关主机将对公网流量进行源地址转换，其他所有主机访问外网的流量经过公网网关后，IP 都被转换为公网网关主机的 IP 地址。下面将介绍使用公网网关及与其相关产品的常用操作，供您参考。

- [创建网关子网](https://intl.cloud.tencent.com/document/product/215/31824)
- [购买公网网关](https://intl.cloud.tencent.com/document/product/215/31825)
- [创建网关子网路由表](https://intl.cloud.tencent.com/document/product/215/31826)
- [配置普通子网路由表](https://intl.cloud.tencent.com/document/product/215/31827)

### NAT 网关
NAT 网关（NAT Gateway）是一种支持 IP 地址转换的网络云服务。它能够为腾讯云内的资源提供高性能的 Internet 访问服务。NAT 网关在内外网隔离时，将私有网络中内网 IP 地址和公网 IP 地址进行转换，实现私有网络访问 Internet 功能。
### 弹性公网 IP
[弹性公网 IP](https://intl.cloud.tencent.com/document/product/215/4958) 是可以独立申请的公网 IP 地址，支持与 CVM / NAT 网关实例的动态绑定和解绑。您可以将其与账户中的云服务器（或 NAT 网关实例）绑定或者解绑，起到屏蔽实例故障的作用。弹性 IP 可以实现 IP 从一个云服务器到另一个云服务器的漂移。在任何云服务器出现故障时，只需启动另一个实例并重新映射它，从而快速响应实例故障。下面将介绍使用弹性公网 IP 及与其相关产品的常用操作，供您参考。

- [申请 EIP](https://intl.cloud.tencent.com/document/product/215/31831)
- [修改 EIP 名称](https://intl.cloud.tencent.com/document/product/215/31832)
- [绑定 EIP](https://intl.cloud.tencent.com/document/product/215/31833)
- [解绑 EIP](https://intl.cloud.tencent.com/document/product/215/31834)
- [释放 EIP](https://intl.cloud.tencent.com/document/product/215/31835)

更多操作，请参见 [弹性公网 IP 操作概述](https://intl.cloud.tencent.com/document/product/215/31830)。
## 资源互通
### 对等连接
对等连接 是一种大带宽、高质量的云上资源互通服务，可以帮助您打通腾讯云上的资源通信链路。 对等连接能轻松实现云上两地三中心、游戏同服等复杂网络场景；支持 VPC 网络与基础网络、黑石网络互通，满足您不同业务的部署需求。
### 基础网络互通
[基础网络互通](https://intl.cloud.tencent.com/document/product/215/5002) 指将基础网络内的云服务器关联至指定私有网络，使基础网络中的云服务器可以与私有网络内的云服务器、数据库等云服务通信。基础网络中的云服务器可以访问私有网络中的云资源，而私有网络内的云服务器，只能访问互通的基础网络云服务器，无法访问基础网络中的其他计算资源。下面将介绍使用基础网络互通及与其相关产品的常用操作，供您参考。

- [将基础网络云服务器关联至私有网络](https://intl.cloud.tencent.com/document/product/215/31841)
- [查看与基础网络互通云服务器](https://intl.cloud.tencent.com/document/product/215/31842)
- [解除私有网络与基础网络内云服务器关联](https://intl.cloud.tencent.com/document/product/215/31853)

### VPN 连接
VPN 连接 是一种基于网络隧道技术，实现本地数据中心与腾讯云上资源连通的传输服务，它能帮您在 Internet 上快速构建一条安全、可靠的加密通道，帮您轻松实现异地容灾、混合云部署等复杂业务场景。
### 专线接入
[专线接入](https://intl.cloud.tencent.com/document/product/216) 为您提供了一种便捷地连接企业数据中心与腾讯云的方法，您可通过专线接入，建立与公网完全隔离的私有连接服务。您只需要一条运营商物理专线一点接入腾讯云，便可快速创建多条专用通道，打通部署于腾讯云的计算资源，实现灵活可靠的混合云部署。下面将介绍使用专线接入及与其相关产品的常用操作，供您参考。

- [申请物理专线](http://intl.cloud.tencent.com/document/product/216/19244)
- [裁撤物理专线](http://intl.cloud.tencent.com/document/product/216/19245)
- [申请通道](http://intl.cloud.tencent.com/document/product/216/19250)
- [变更通道](http://intl.cloud.tencent.com/document/product/216/19251)
- [创建专线网关](http://intl.cloud.tencent.com/document/product/216/19256)

更多操作，请参见 [专线接入操作概述](https://intl.cloud.tencent.com/document/product/215/31845)。

### 云联网
[云联网](https://intl.cloud.tencent.com/document/product/1003) 提供全网互联服务，助力您实现各地域的云上、云下多点互联。云联网的智能调度、路由学习等特性，可帮助您构建极速、稳定、经济的全网互联，轻松满足在线教育、游戏加速、混合云等全网互联场景下的极速体验。下面将介绍使用云联网及与其相关产品的常用操作，供您参考。

- [新建云联网实例](http://intl.cloud.tencent.com/document/product/1003/30062)
- [删除云联网实例](http://intl.cloud.tencent.com/document/product/1003/30063)
- [关联网络实例](http://intl.cloud.tencent.com/document/product/1003/30064)
- [解除网络实例关联](http://intl.cloud.tencent.com/document/product/1003/30065)
- [查看路由信息](http://intl.cloud.tencent.com/document/product/1003/30066)

更多操作，请参见 [云联网操作概述](https://intl.cloud.tencent.com/document/product/215/31846)。

## 安全管理
### 网络 ACL
[网络 ACL](https://intl.cloud.tencent.com/document/product/215/5132) 是一个子网级别无状态的可选安全层，用于控制进出子网的数据流，可以精确到协议和端口粒度。由于网络 ACL 无状态的特性，设置入站规则允许某些访问后，如果没有设置相应的出站规则，也会导致无法响应访问。下面将介绍使用网络 ACL 及与其相关产品的常用操作，供您参考。

- [创建网络 ACL](https://intl.cloud.tencent.com/document/product/215/31851)
- [查看网络 ACL 列表](https://intl.cloud.tencent.com/document/product/215/31852)
- [增加网络 ACL 规则](https://intl.cloud.tencent.com/document/product/215/31853)
- [删除网络 ACL 规则](https://intl.cloud.tencent.com/document/product/215/31854)
- [子网关联网络 ACL](https://intl.cloud.tencent.com/document/product/215/31855)

更多操作，请参见 [网络 ACL 操作概述](https://intl.cloud.tencent.com/document/product/215/31850)。

### 访问控制
[访问控制](https://intl.cloud.tencent.com/document/product/598) 是腾讯云提供的一套 Web 服务，用于帮助客户安全地管理腾讯云账户的访问权限，资源管理和使用权限。通过 CAM，您可以创建、管理和销毁用户（组），并通过身份管理和策略管理控制哪些人可以使用哪些腾讯云资源。下面将介绍使用访问控制及与其相关产品的常用操作，供您参考。

- [VPC 访问控制策略示例](https://intl.cloud.tencent.com/document/product/215/31861)
- [VPC API 操作支持的资源级权限](https://intl.cloud.tencent.com/document/product/215/31862)

### 参数模板
[参数模板](https://intl.cloud.tencent.com/document/product/215/31890) 是一组参数的集合，支持 IP 地址和协议端口，可被安全组规则引用，主要用于统一管理安全组规则的 IP 或协议端口组。下面将介绍使用参数模板及与其相关产品的常用操作，供您参考。

- [创建 IP 地址](https://intl.cloud.tencent.com/document/product/215/31865)
- [创建端口协议](https://intl.cloud.tencent.com/document/product/215/31866)
- [在安全组中引用参数模板](https://intl.cloud.tencent.com/document/product/215/31867)

## 网络探测
[网络探测](https://intl.cloud.tencent.com/document/product/215/31792) 是监控 VPC 网络连接质量的服务，可为您监控网络连接的时延、丢包率等关键指标。您可以通过网络探测设置预警、多维度监控来迅速定位问题，还可以在子网内创建网络探测对象来实时监控网络连接质量，提升业务稳定性。下面将介绍使用网络探测及与其相关产品的常用操作，供您参考。

- [创建网络探测](https://intl.cloud.tencent.com/document/product/215/31871)
- [查看网络探测时延和丢包率](https://intl.cloud.tencent.com/document/product/215/31872)
- [修改网络探测](https://intl.cloud.tencent.com/document/product/215/31873)
- [删除网络探测](https://intl.cloud.tencent.com/document/product/215/31874)
