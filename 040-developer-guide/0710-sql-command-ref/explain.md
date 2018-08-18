# EXPLAIN

显示一个语句的查询计划

## 概要

```
EXPLAIN [ANALYZE] [VERBOSE] statement
```

## 描述

EXPLAIN 显示 HashData 计划器为提供的语句所生成的查询计划。查询计划是一颗节点计划树。在计划中的每个节点代表了一个操作，例如表扫描、连接、聚集或者是一个排序操作。

因为每个节点直接向它上面的节点提供行结果，所以计划应该从下往上进行阅读。最底层的节点通常是一些表扫描操作（顺序扫描、索引扫描或者是位图扫描）。如果查询要求连接、聚集或者排序（或者其他在原始行上的操作），那么需要再扫描节点增加这些操作的节点。计划最顶层的节点通常是 HashData 的 motion 节点（重分布、显式重分布、广播或者聚集 motion）。这些操作符代表了在查询处理期间在分片示例之间移动行数据。

EXPLAIN 的输出是树中每个节点有一行，显示基本的节点类型，紧接着是由计划器为执行该计划节点时的代价评估：

* **cost** — 通过读取磁盘页面的次数来度量。即，1.0 代表一个连续磁盘页面的读取。首先是启动代价（获取第一行的代价），第二个代价是总的代价（获取所有行的代价）。注意总的代价假设所有的行都将要被取回，但并不是总是这种情况（比如使用 LIMIT 语句）。
* **rows** — 该计划节点总的输出行数。这通常是小于实际由计划节点处理或者扫描的行数，主要是由于任何一个 WHERE 条件语句的评估选择性。理想情况下，最高层的节点估计近似等于实际由该查询返回、更新或者删除的行数。
* **width** — 该计划节点所有行输出的总的字节数。

值得注意的是更上一层的节点的代价包括了所有它孩子节点的代价。计划中最顶层节点是估计执行整个计划的代价。该数字是计划器寻求最小化的地方。同时也需要意识到代价仅仅反应了查询优化器关心的部分。特别是，代价没有考虑将结果行传输到客户端所花费的时间。

EXPLAIN ANALYZE 导致该语句被实际执行，而不仅仅是被计划。EXPLAIN ANALYZE 计划显示实际的结果以及计划器的评估。这个对于看是否计划器评估接近实际的情况非常有用。除了显示在 EXPLAIN 计划中的信息，EXPLAIN ANALYZE 还要外加显示下面的信息：

* 总的花费在执行该查询的时间间隔（以毫秒为单位）。
* 在一个计划节点操作中涉及到的 workers（Segment）的数量。只有返回行的 Segment 被计入。
* 一个操作中输出最多行的 Segment 返回的最大行数。如果多个 Segment 输出了相同数量的行数，取 time to end 最长的那个 Segment。
* 在一个操作中输出最多行的 Segment 的 ID。
* 对于相关的操作，该操作使用的 work\_mem。如果 work\_mem 不足以在内存中执行操作，计划将显示有多少数据溢出到磁盘上以及对于使用工作内存最少的执行 Segment 要求了多少趟对数据的处理。例如：

  ```
  Work_mem used: 64K bytes avg, 64K bytes max (seg0).
      Work_mem wanted: 90K bytes avg, 90K bytes max (seg0) to abate workfile
      I/O affecting 2 workers.
      [seg0] pass 0: 488 groups made from 488 rows; 263 rows written to
      workfile
      [seg0] pass 1: 263 groups made from 263 rows
  ```

* 产生最多行的 Segment 检索到第一行所花的时间（以毫秒计），以及在该 Segment 上获取所有行所花费的时间。如果 `<time> to first row` 同 `<time> to end` 相等，则前者有可能被省略。

> 重要： 记住当使用 EXPLAIN ANALYZE 语句会被实际执行。尽管 EXPLAIN ANALYZE 将丢弃 SELECT 所返回的任何输出，照例该语句的其他副作用还是会发生。如果用户希望在一个 DML 语句上执行EXPLAIN ANALYZE 而不希望它们影响用户的数据，可以使用下面的方法：

```
BEGIN;
EXPLAIN ANALYZE ...;
ROLLBACK;
```

## 参数

name

将要执行的预备语句的名称。

parameter

预备语句的实际参数值。这一定是一个产生与该参数数据类型兼容的值的表达式，参数的数据类型则是在预备语句被创建时定义的。

## 注解

为了允许查询计划器在优化查询时能做出合理的知情决策，ANALYZE 语句需要被执行用来记录关于在表内数据的分布统计信息。如果用户还没有完成这个操作（或者如果表内数据从上一次执行 ANALYZE 语句后的统计分布发生了很大的变化），那么评估代价不会很符合实际的查询属性，同时因此会导致选择一个较差的计划被选中。

一个 SQL 语句在一个 EXPLAIN ANALYZE 命令被执行时执行会从 HashData 资源队列中排出。

更多关于资源队列的信息见 HashData 数据库管理员指南中的“用资源队列进行工作负载管理”部分。

## 示例

为了展示如何阅读一个 EXPLAIN 查询计划，考虑下面的一个简单查询的例子：

```
EXPLAIN SELECT * FROM names WHERE name = 'Joelle';
                     QUERY PLAN
------------------------------------------------------------
Gather Motion 2:1 (slice1) (cost=0.00..20.88 rows=1 width=13)

   -> Seq Scan on 'names' (cost=0.00..20.88 rows=1 width=13)
         Filter: name::text ~~ 'Joelle'::text
```

如果我们从下往上阅读该计划，查询优化器开始于顺序扫描表names。注意 WHERE 子句作为一个过滤条件被应用。这意味着一个扫描操作要检验扫描中的每一行是否满足该条件，同时返回那些满足条件的行。

扫描操作的结果将向上传递到一个 gather motion 操作。在 HashData 数据库中， gather motion 是 Segment 向上传递行到 Master 的时机。在该例子中，我们有 2 个 Segment 实例发送到 1 个 Master 实例（2：1）。该操作工作在并行查询执行计划的 slice1 上。在 HashData 数据库中，一个查询计划被分成切片，这样每个查询计划的多个部分能够被 Segment 并行地执行。

该计划的估计启动代价是 00.00（没有代价）以及总代价为 20.88 次取磁盘页。计划器认为该查询将会返回一行。

## 兼容性

在 SQL 标准中没有定义 EXPLAIN 语句。

## 另见

[ANALYZE](./analyze.md)

**上级主题：** [SQL命令参考](./README.md)
