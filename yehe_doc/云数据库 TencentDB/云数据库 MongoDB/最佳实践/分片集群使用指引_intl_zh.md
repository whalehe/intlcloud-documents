分片集群为 MongoDB 的分布式版本，相较副本集，分片集群数据被均衡的分布在不同分片中， 不仅大幅提升了整个集群的数据容量上限，也将读写的压力分散到不同分片，以解决副本集性能瓶颈的难题，但分片集群的架构更加复杂，本文重点介绍使用腾讯云 MongoDB 分片集群时的注意事项。

## 分片集群组件
一个 MongoDB 分片集群由如下三个组件构成，缺一不可：
- shard：每个分片是整体数据的一部分子集，每个分片都部署为副本集。
- mongos：充当查询路由器，提供客户端应用程序和分片集群之间的接口。
- config servers：配置服务器存储集群的元数据和配置，包括权限认证相关。

## 分片集群 sharding 方式及性能影响
MongoDB 分片集群提供三种 Sharding（数据分布）方式，分别为基于范围、基于 Hash、基于 zone/tag。不同的 Sharding 方式使用不同的业务，也会对性能产生不同的影响。
- **基于范围**
优势：分片键范围查询性能较好，读性能较好。
劣势：数据分布可能不均匀，存在热点。
- **基于 Hash**
优势：数据分布均匀，写性能较好，适用于日志、物联网等高并发场景。
劣势：范围查询效率较低。
- **基于 zone/tag**
若数据具备一些天然的区分，如基于地域、时间等标签，数据可以基于标签来做区分。
优势：数据分布较为合理。


## 分片键的选择
分片键是文档中的某一个字段，用来进行路由查询，分片键是不可变的，且必须有索引。
选择合适的片键对 sharding 效率影响很大，主要基于如下四个因素：

- **取值基数**
取值基数建议尽可能大，如果用小基数的片键，因为备选值有限，那么块的总数量就有限，随着数据增多，块的大小会越来越大，导致水平扩展时移动块会非常困难。
例如：选择年龄做一个基数，范围最多只有100个，随着数据量增多，同一个值分布过多时，导致 chunck 的增长超出 chuncksize 的范围，引起 jumbo chunk，从而无法迁移，导致数据分布不均匀，性能瓶颈。

- **取值分布**
取值分布建议尽量均匀，分布不均匀的片键会造成某些块的数据量非常大，同样有上面数据分布不均匀，性能瓶颈的问题。
 
- **查询带分片**
查询时建议带上分片，使用分片键进行条件查询时，mongos 可以直接定位到具体分片，否则 mongos 需要将查询分发到所有分片，再等待响应返回。
 
- **避免单调底层或递减**
单调递增的 sharding key，数据文件挪动小，但写入会集中，导致最后一篇的数据量持续增大，不断发生迁移，递减同理。

综上，在选择片键时要考虑以上4个条件，尽可能满足更多的条件，才能降低 MoveChuncks 对性能的影响，从而获得最优的性能体验。

## 分片集群 balance 介绍及相关参数
在一个分片集群内部，MongoDB 会把数据分为 chunks，后台进程 balancer 负责 chunk 的迁移，从而均衡各个 shard server 的负载，每个 chunk 包含一部分数据，chunk 的产生和迁移会导致 balance 的产生。
>系统初始仅1个 chunk，chunk size 默认值64MB。

chunck 迁移时会造成集群的读写性能下降，因此需要通过适当配置 balance 活动窗口来避免 balance 对业务高峰期的影响，也可以通过命令来关闭 balance。

下面介绍管理 balance 的相关命令，若某些指令无权限执行，请 [提交工单](https://intl.cloud.tencent.com/contact-sales) 联系我们处理。

- **查看 mongo 集群是否开启了 balance**
```
mongos> sh.getBalancerState()
true
```
也可通过执行 sh.status() 查看 balance 状态。

- **查看是否正在有数据的迁移**
```
mongos> sh.isBalancerRunning()
false
```

- **设置 balance 窗口**
 - 修改 balance 窗口的时间：
```
db.settings.update(
   { _id: "balancer" },
   { $set: { activeWindow : { start : "<start-time>", stop : "<stop-time>" } } },
   { upsert: true }
)
```

 - 删除 balance 窗口：
```
use config
db.settings.update({ _id : "balancer" }, { $unset : { activeWindow : true } })
```

- **关闭 balance**
 - 默认 balance 的运行可以在任何时间，迁移只需要迁移的 chunk，如需关闭 balance，可执行下列命令：
```
sh.stopBalancer()
sh.getBalancerState()
```

 - 停止 balace 后，查看是否有迁移进程正在执行，可执行下列命令：
```
use config
while( sh.isBalancerRunning() ) {
          print("waiting...");
          sleep(1000);
}
```

- **打开 balance**
 - 如您需要准备重新打开 balance，可执行下列命令：
```
sh.setBalancerState(true)
```

 - 当驱动版本不支持 sh.startBalancer() 时，可执行下列命令来重新打开 balance：
```
use config
db.settings.update( { _id: "balancer" }, { $set : { stopped: false } } , { upsert: true } )
```


- **集合的 balance**
 - 关闭某个集合的 balance：
```
sh.disableBalancing("students.grades")
```

 - 打开某个集合的 balance：
```
sh.enableBalancing("students.grades")
```

 - 查看某个集合是否开启了 balance：
```
db.getSiblingDB("config").collections.findOne({_id : "students.grades"}).noBalance
```

