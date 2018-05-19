# 最佳实践提纲

## 数据模型

* HashData 数据仓库是一个基于大规模并行处理（MPP）和无共享架构（shared nothing）的分布式分析型数据库。这种数据库的数据模式与高度规范化的事务性（OLTP）数据库显著不同。通过使用非规范化数据库模式，例如具有大事实表和小维度表的星型或者雪花模式，HashData 数据仓库在处理分析型业务（OLAP）时表现优异。
* 跨表关联（JOIN）时字段使用相同的数据类型。

## 堆存储和追加优化存储

* 若表和分区表需要进行迭代式的批处理或者频繁执行单个 UPDATE、DELETE 或 INSERT                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          操作，使用堆存储。
* 若表和分区表需要并发执行 UPDATE、DELETE 或 INSERT 操作，使用堆存储。
* 若表和分区表在数据初始加载后更新不频繁，且仅以批处理方式插入数据，则使用 AO 存储。
* 不要对 AO 表执行单个 INSERT、UPDATE 或 DELETE 操作。
* 不要对 AO 表执行并发批量 UPDATE 或 DELETE 操作，但可以并发执行批量 INSERT 操作。

## 行式存储和列式存储

* 若数据需要经常更新或者插入，则使用行存储。
* 若需要同时访问一个表的很多字段，则使用行存储。
* 对于通用或者混合型业务，建议使用行存储。
* 若查询访问的字段数目较少，或者仅在少量字段上进行聚合操作，则使用列存储。
* 若仅常常修改表的某一字段而不修改其他字段，则使用列存储。

## 压缩

* 对于大 AO 表和分区表使用压缩，以提高系统 I/O。
* 在字段级别配置压缩。
* 考虑压缩比和压缩性能之间的平衡。

## 分布

* 为所有表定义分布策略：要么定义分布键，要么使用随机分布，不要使用缺省分布方式。
* 优先选择可均匀分布数据的单个字段做分布键。
* 不要选择经常用于 WHERE 子句的字段做分布键。
* 不要使用日期或时间字段做分布键。
* 分布键和分区键不要使用同一字段。
* 对经常执行 JOIN 操作的大表，优先考虑使用关联字段做分布键，尽量做到本地关联，以提高性能。
* 数据初始加载后或者每次增量加载后，检查数据分布是否均匀。
* 尽可能避免数据倾斜。

## 内存管理

* 使用 statement\_mem 控制节点数据库为单个查询分配的内存量。
* 使用资源队列设置队列允许的当前最大查询数（ACTIVE\_STATEMENTS）和允许使用的内存大小（MEMORY\_LIMIT）。
* 不要使用默认的资源队列，为所有用户都分配资源队列。
* 根据负载和时间段，设置和队列实际需求相匹配的优先级（PRIORITY）。
* 保证资源队列的内存配额不超 gp\_vmem\_protect\_limit。
* 动态更新资源队列配置以适应日常工作需要。

## 分区

* 只为大表设置分区，不要为小表设置分区。
* 仅在根据查询条件可以实现分区裁剪时使用分区表。
* 建议优先使用范围 \(Range\) 分区，否则使用列表 \(List\) 分区。
* 根据查询特点合理设置分区。
* 不要使用相同的字段既做分区键又做分布键。
* 不要使用默认分区。
* 避免使用多级分区；尽量创建少量的分区，每个分区的数据更多些。
* 通过查询计划的 EXPLAIN 结果来验证查询对分区表执行的是选择性扫描（分区裁剪）。
* 对于列存储的表，不要创建过多的分区，否则会造成物理文件过多：
  _Physical files = Segments × Columns × Partitions_ 。

## 索引

* 一般来说 HashData 数据仓库中索引不是必需的。
* 对于高基数的列式存储表，如果需要遍历且查询选择性较高，则创建单列索引。
* 频繁更新的列不要建立索引。
* 在加载大量数据之前删除索引，加载结束后再重新创建索引。
* 优先使用 B 树索引。
* 不要为需要频繁更新的字段创建位图索引。
* 不要为唯一性字段，基数非常高或者非常低的字段创建位图索引。
* 不要为事务性负载创建位图索引。
* 一般来说不要索引分区表。如果需要建立索引，则选择与分区键不同的字段。

## 资源队列

* 使用资源队列管理集群的负载。
* 为所有角色定义适当的资源队列。
* 使用 ACTIVE\_STATEMENTS 参数限制队列成员可以并发运行的查询总数。
* 使用 MEMORY\_LIMIT 参数限制队列中查询可以使用的内存总量。
* 不要设置所有队列为 MEDIUM，这样起不到管理负载的作用。
* 根据负载和时间段动态调整资源队列。

## ANALYZE

* 不要对整个数据库运行 ANALYZE，只对需要的表运行该命令。
* 建议数据加载后即刻运行 ANALYZE。
* 如果 INSERT、UPDATE 和 DELETE 等操作修改大量数据，建议运行 ANALYZE。
* 执行 CREATE INDEX 操作后建议运行 ANALYZE。
* 如果对大表 ANALYZE 耗时很久，则只对 JOIN 字段、WHERE、SORT、GROUP BY 或 HAVING 字句的字段运行 ANALYZE。

## VACCUM

* 批量 UPDATE 和 DELETE 操作后建议执行 VACUUM。
* 不建议使用 VACUUM FULL。建议使用 CTAS（CREATE TABLE…AS） 操作，然后重命名表名，并删除原来的表。
* 对系统表定期运行 VACUUM，以避免系统表臃肿和在系统表上执行 VACUUM FULL 操作。
* 禁止杀死系统表的 VACUUM 任务。
* 不建议使用 VACUUM ANALYZE。

## 加载

* 使用 gpfdist 进行数据的加载和导出。
* 随着 Segment 数据库个数的增加，并行性增加。
* 尽量将数据均匀地分布到多个 ETL 节点上。
* 将非常大的数据文件切分成相同大小的块，并放在尽量多的文件系统上。
* 一个文件系统运行两个 gpfdist 实例。
* 在尽可能多的网络接口上运行 gpfdsit。
* 使用 gp\_external\_max\_segs 控制访问每个 gpfdist 服务器的 Segment 数据库的个数。 **建议 gp\_external\_max\_segs 的值和 gpfdist 进程个数为偶数。**
* 数据加载前删除索引，加载完后重建索引。
* 数据加载完成后运行 ANALYZE 操作。
* 数据加载过程中，设置 gp\_autostats\_mode 为 NONE，取消统计信息的自动收集。
* 若数据加载失败，使用 VACUUM 回收空间。

## gptransfer

* 为了更好的性能，建议使用 gptransfer 迁移数据到相同大小或者更大的集群。
* 避免使用 –full 或者 –schema-only 选项。建议使用其他方法拷贝数据库模式到目标数据库，然后迁移数据。
* 迁移数据前删除索引，迁移完成后重建索引。
* 使用 SQL COPY 命令迁移小表到目标数据库。
* 使用 gptransfer 批量迁移大表。
* 在正式迁移生产环境前测试运行 gptransfer。试验 –batch-size 和 –sub-batch-size 选项以获得最大平行度。如果需要，迭代运行多次 gptransfer 来确定每次要迁移的表的批次。
* 仅使用完全限定的表名。表名字中若含有点、空格、单引号和双引号，可能会导致问题。
* 如果使用 –validation 选项在迁移后验证数据，则需要同时使用 -x 选项，以在源表上加排它锁。
* 确保在目标数据库上创建了相应的角色、函数和资源队列。gptransfer -t 不会迁移这些对象。
* 从源数据库拷贝 postgres.conf 和 pg\_hba.conf 到目标数据库集群。
* 使用 gppkg 在目标数据库上安装需要的扩展。

## 安全

* 妥善保护 gpadmin 账号，只有在必要的时候才能允许系统管理员访问它。
* 仅当执行系统维护任务（例如升级或扩容），管理员才能以 gpadmin 登录 HashData 数据仓库集群。
* 限制具有 SUPERUSER 角色属性的用户数。HashData 数据仓库中，身为超级用户的角色会跳过所有访问权限检查和资源队列限制。仅有系统管理员具有数据库超级用户权限。参考《HashData 数据仓库管理员指南》中的“修改角色属性”。
* 严禁数据库用户以 gpadmin 身份登录，严禁以 gpadmin 身份执行 ETL 或者生产任务。
* 为有登录需求的每个用户都分配一个不同的角色。
* 考虑为每个应用或者网络服务分配一个不同的角色。
* 使用用户组管理访问权限。
* 保护好 ROOT 的密码。
* 对于操作系统密码，强制使用强密码策略。
* 确保保护好操作系统的重要文件。

## 加密

* 加密和解密数据会影响性能，仅加密需要加密的数据。
* 在生产系统中实现任何加密解决方案之前都要做性能测试。
* HashData 数据仓库生产系统使用的服务器证书应由证书签名颁发机构（CA）签名，这样客户端可以验证服务器。如果所有客户端都是本地的，则可以使用本地 CA。
* 如果客户端与 HashData 数据仓库的连接会经过不安全的链路，则使用 SSL 加密。
* 加密和解密使用相同密钥的对称加密方式比非对称加密具有更好的性能，如果密钥可以安全共享，则建议使用对称加密方式。
* 使用 pgcrypto 包中的函数加密磁盘上的数据。数据的加密和解密都由数据库进程完成，为了避免传输明文数据，需要使用 SSL 加密客户端和数据库间的连接。
* 数据加载和导出时，使用 gpfdists 协议保护 ETL 数据安全。

## 高可用

* 使用 8 到 24 个磁盘的硬件 RAID 存储解决方案。
* 使用 RAID1、5 或 6，以使磁盘阵列可以容忍磁盘故障。
* 为磁盘阵列配备热备磁盘，以便在检测到磁盘故障时自动开始重建。
* 在重建时通过 RAID 卷镜像防止整个磁盘阵列故障和性能下降。
* 定期监控磁盘利用率，并在需要时增加额外的空间。
* 定期监控段数据库倾斜，以确保在所有段数据库上数据均匀分布，存储空间均匀消耗。
* 配置备用主服务器，当主服务器发生故障时由备用主服务器接管。
* 规划好当主服务器发生故障时如何切换客户端连接到新的主服务器实例，例如通过更新 DNS 中主服务器的地址。
* 建立监控系统，当主服务器发生故障时，可以通过系统监控应用或电子邮件发送通知。
* 分配主段数据库和其镜像到不同的主机上，以防止主机故障。
* 建立监控系统，当主段数据库发生故障时，可以通过系统监控应用或电子邮件发送通知。
* 使用 gprecoverseg 工具及时恢复故障段，并使系统返回最佳平衡状态。
* 在主服务器上配置并运行 gpsnmpd 以发送 SNMP 通知给网络监控器。
* 在 $Master\_DATA\_DIRECTORY/postgresql.conf 配置文件中设置邮件通知，以便检测到关键问题时, HashData 数据仓库系统可以通过电子邮件通知管理员。
* 考虑双集群配置，提供额外的冗余和查询处理能力。
* 除非 HashData 数据仓库数据仓库的数据很容易从数据源恢复，否则定期备份。
* 如果堆表相对较小，或者两次备份之间仅有少量 AO 或列存储分区有变化，则使用增量备份。
* 如果备份保存在集群的本地存储系统上，则备份结束后，将文件移到其他的安全存储系统上。
