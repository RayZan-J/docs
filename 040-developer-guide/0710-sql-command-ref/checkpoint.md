# CHECKPOINT

强制执行事务日志检查点。

## 概要

```
CHECKPOINT
```

## 描述

预写式日志记录（WAL）每隔一段时间将一个检查点放在事务日志中。根据服务器配置参数 checkpoint\_segments 和 checkpoint\_timeout， 每个 HashData 数据库段实例设置自动检查点间隔。CHECKPOINT 命令在发出命令时强制立即检查点，而不等待计划的检查点。

检查点是事务日志序列中的所有数据文件已更新以反映日志中的信息的一点。所有数据文件将刷新到磁盘。

只有超级用户可以调用 CHECKPOINT。该命令不适用于正常操作。

## 兼容性

CHECKPOINT 是 HashData 数据库语言扩展。

**上级主题：** [SQL命令参考](./README.md)
