# DROP SEQUENCE

移除一个序列。

## 概要

```
DROP SEQUENCE [IF EXISTS] name [, ...] [CASCADE | RESTRICT]
```

## 描述

DROP SEQUENCE 移除序数生成器表。一个序列只能被其拥有者（或超级用户删除）。

## 参数

IF EXISTS

如果该序列不存在则不要抛出一个错误，而是发出一个提示。

name

要移除序列的名称（可以是方案限定的）。

CASCADE

自动删除依赖于该序列的对象，然后删除所有依赖于那些对象的对象。

RESTRICT

如果有任何对象依赖于该序列，则拒绝删除它。这是默认值。

## 示例

移除一个名为 myserial 的序列：

```
DROP SEQUENCE myserial;
```

## 兼容性

DROP SEQUENCE 符合 SQL 标准，不过该标准只允许每个命令中删除一个序列并且没有 IF EXISTS 选项。该选项是一个 HashData 扩展。

## 另见

[ALTER SEQUENCE](./alter-sequence.md), [CREATE SEQUENCE](./create-sequence.md)

**上级主题：** [SQL命令参考](./README.md)

