You can choose from several load balancer attributes on the purchase page. Here we talk about how to select load balancers that are suitable for different application scenarios.
## Region
1. It is recommended to select the region closest to your client to reduce latency and improve downloading speed.
2. CLB can only route traffic to CVM instances within the same region. Therefore, please select the region before creating any load balancer.
3. CLB can route traffic to the CVM instances across multiple Availability Zones within the same region. For example, CLB in Beijing can route traffic to the CVM instances of Beijing Zone 1, Beijing Zone 2 and Beijing Zone 3.
4. Public network Application CLB can be bound with CVM across regions. Users can select the region of the backend server, bind backend instances across VPCs and regions. For example, CLB in Beijing can be bound with CVM of Shanghai, and route the traffic to it. For more, see [Binding Cross-region CLBs](https://intl.cloud.tencent.com/document/product/214/12014).

## Instance Type
There are two types of CLB instances: Classic CLB Instance and Application CLB Instance.
Classic CLB Instance is an earlier version while Application CLB Instance is an optimized version.  Application CLB Instance includes almost all earlier version features. The Application CLB Instance is recommended for better functionalities and performance. For detailed comparison, see [Application and Conventional CLB comparison](https://intl.cloud.tencent.com/document/product/214/8847).

## Network Type (Public/Private)
### Public Network CLB
If you need CLB to allocate requests from the public network, please select "Public network". Public network CLB instance accepts requests from the client over the Internet, and allocates these requests to the backend server bound with it. After a public network CLB is created, Tencent Cloud assigns a VIP address to the load balancer. At the same time, DNS server resolves the VIP address. A public network CLB also supports binding CNAME and A Record, and mapping them to user-readable custom domain names. Each VIP of the public network load balancer is a fixed BGP public IP and can receive the HTTP, HTTPS, TCP, and UDP requests forwarded from the client.

1. Application scenarios
  - When a server cluster is used to provide services to the public network, a single entry is required, and public network user requests need to be properly allocated to the server cluster.
  - Connecting users of different ISPs to the closest network to improve network access speed.
2. Billing
  - Public network-based CLB charges a rental fee only. For details, see [Billing Description](https://intl.cloud.tencent.com/document/product/214/8848).
  - Public network bandwidth or traffic generated by the service will be billed at the backend server. For details, see [Network Bandwidth Purchase](https://intl.cloud.tencent.com/document/product/213/10578).

### Private Network CLB
If you need CLB to allocate requests from the private network, please select "Private network". The server and client of the private network CLB are both inside the Tencent Cloud, so that the private network CLB can only be accessed from within Tencent Cloud, and cannot be accessed over the Internet (for no public IP is available). A private network CLB instance routes the traffic to the backend CVM instances in the same region by using [private IP](https://intl.cloud.tencent.com/doc/product/213/5225), and this is how an internal CVM cluster is formed. If the application has a multi-layered architecture (such as Web servers that can communicate with the Internet and database servers that cannot communicate with the Internet but only communicate with each other via private networks), you can design an architecture with both private network and public network load balancers. You can connect all the Web servers to the public network load balancers, and connect the database servers to the private network load balancers. The public network load balancers receive requests from the Internet and send them to the backend Web servers. After processing, the requests for databases are sent to the private network load balancers, which then route the requests to the database servers.

1. Application scenarios
 - When Tencent Cloud has more than one internal servers and the requests from client need to be allocated to the servers properly;
 - When fault tolerance and fault recovery are needed for the internal server cluster;
 - When the service provider wants to block its own physical IP address and provide transparent services to the client;
2. Billing
  - Private network load balancers are free of charge.
