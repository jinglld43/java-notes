# Table of Contents

- [索引](#索引)
  - [B+ Tree 原理](#b-tree-原理)
    - [数据结构](#数据结构)
    - [查询过程](#查询过程)
    - [分类](#分类)
  - [不同存储结构的索引](#不同存储结构的索引)
    - [1. B+Tree 索引](#1-btree-索引)
    - [2. 哈希索引](#2-哈希索引)
    - [3. 全文索引](#3-全文索引)
    - [4. 空间数据索引](#4-空间数据索引)
  - [索引优化](#索引优化)
    - [1. 建立单列索引](#1-建立单列索引)
    - [2. 建立联合索引](#2-建立联合索引)
    - [3. 联合索引的顺序](#3-联合索引的顺序)
    - [4. 前缀索引](#4-前缀索引)
    - [5. 覆盖索引](#5-覆盖索引)
    - [6. 避免索引失效](#6-避免索引失效)
  - [索引失效](#索引失效)
  - [索引的优点](#索引的优点)
  - [索引的使用条件](#索引的使用条件)
- [事务](#事务)
  - [概念](#概念)
  - [ACID](#acid)
    - [1. 原子性（Atomicity）](#1-原子性（atomicity）)
    - [2. 一致性（Consistency）](#2-一致性（consistency）)
    - [3. 隔离性（Isolation）](#3-隔离性（isolation）)
    - [4. 持久性（Durability）](#4-持久性（durability）)
  - [AUTOCOMMIT](#autocommit)
- [并发一致性问题](#并发一致性问题)
  - [丢失修改](#丢失修改)
  - [读脏数据](#读脏数据)
  - [不可重复读](#不可重复读)
  - [幻影读](#幻影读)
- [隔离级别](#隔离级别)
  - [未提交读（READ UNCOMMITTED）](#未提交读（read-uncommitted）)
  - [提交读（READ COMMITTED）](#提交读（read-committed）)
  - [可重复读（REPEATABLE READ）](#可重复读（repeatable-read）)
  - [可串行化（SERIALIZABLE）](#可串行化（serializable）)
- [多版本并发控制](#多版本并发控制)
  - [版本号](#版本号)
  - [隐藏的列](#隐藏的列)
  - [Undo 日志](#undo-日志)
  - [实现过程](#实现过程)
    - [1. SELECT](#1-select)
    - [2. INSERT](#2-insert)
    - [3. DELETE](#3-delete)
    - [4. UPDATE](#4-update)
  - [快照读与当前读](#快照读与当前读)
    - [1. 快照读](#1-快照读)
    - [2. 当前读](#2-当前读)
- [查询性能优化](#查询性能优化)
  - [1. 开启慢查询](#1-开启慢查询)
  - [2. 使用 Explain 进行分析](#2-使用-explain-进行分析)
  - [3. 优化数据访问](#3-优化数据访问)
    - [1. 减少请求的数据量](#1-减少请求的数据量)
    - [2. 减少服务器端扫描的行数（索引优化）](#2-减少服务器端扫描的行数（索引优化）)
  - [4. 重构查询方式](#4-重构查询方式)
    - [1. 切分大查询](#1-切分大查询)
    - [2. 分解大连接查询](#2-分解大连接查询)
- [封锁](#封锁)
  - [封锁粒度](#封锁粒度)
  - [封锁类型](#封锁类型)
    - [1. 读写锁](#1-读写锁)
    - [2. 意向锁](#2-意向锁)
    - [3. 乐观锁VS悲观锁](#3-乐观锁vs悲观锁)
  - [行锁优化](#行锁优化)
    - [两阶段锁](#两阶段锁)
    - [死锁处理方式](#死锁处理方式)
    - [分段锁的思想](#分段锁的思想)
  - [Next-Key Locks](#next-key-locks)
    - [Record Locks](#record-locks)
    - [Gap Locks](#gap-locks)
    - [Next-Key Locks](#next-key-locks-1)
- [存储引擎](#存储引擎)
  - [InnoDB](#innodb)
  - [MyISAM](#myisam)
  - [比较](#比较)
- [数据类型](#数据类型)
  - [整型](#整型)
  - [浮点数](#浮点数)
  - [字符串](#字符串)
  - [TEXT 与 BLOB](#text-与-blob)
  - [时间和日期](#时间和日期)
    - [1. DATETIME](#1-datetime)
    - [2. TIMESTAMP](#2-timestamp)
- [分区分表](#分区分表)
  - [分区](#分区)
  - [分表](#分表)
    - [水平切分](#水平切分)
    - [垂直切分](#垂直切分)
  - [Sharding 策略](#sharding-策略)
  - [Sharding 存在的问题](#sharding-存在的问题)
    - [1. 事务问题](#1-事务问题)
    - [2. 连接](#2-连接)
    - [3. ID 唯一性](#3-id-唯一性)
- [集群](#集群)
  - [主从复制：同步问题](#主从复制：同步问题)
  - [读写分离](#读写分离)
  - [高可用](#高可用)
- [范式](#范式)
  - [1. 第一范式 (1NF)](#1-第一范式-1nf)
  - [2. 第二范式 (2NF)](#2-第二范式-2nf)
  - [3. 第三范式 (3NF)](#3-第三范式-3nf)
- [count(*)优化](#count优化)
  - [count(*)原理](#count原理)
  - [用缓存系统保存计数](#用缓存系统保存计数)
  - [在数据库保存计数](#在数据库保存计数)
  - [不同的 count 用法](#不同的-count-用法)
- [分析工具](#分析工具)
  - [show profiles](#show-profiles)
  - [explain](#explain)
  - [慢查询](#慢查询)
- [日志系统](#日志系统)
  - [一条SQL查询语句是如何执行的](#一条sql查询语句是如何执行的)
  - [redo](#redo)
  - [binlog](#binlog)
    - [mysql的两阶段提交协议](#mysql的两阶段提交协议)
  - [undo](#undo)
  - [从innodb事务执行流程感受日志系统](#从innodb事务执行流程感受日志系统)
- [参考资料](#参考资料)



# 索引

## B+ Tree 原理

### 数据结构

B+树：多叉树+搜索树+平衡树+每个节点多个数据+叶子节点存放数据(聚簇索引)

### 查询过程

进行查找操作时，首先在根节点进行二分查找，找到一个 key 所在的指针，然后递归地在指针所指向的节点进行查找。直到查找到叶子节点，然后在叶子节点上进行二分查找，找出 key 所对应的 data。

插入删除操作会破坏平衡树的平衡性，因此在插入删除操作之后，需要对树进行一个分裂、合并、旋转等操作来维护平衡性。所以这就是自增主键出现的原因

### 分类

聚簇索引

```
主键索引的叶子节点存的是整行数据。在 InnoDB 里，主键索引也被称为聚簇索引 （clustered index）。

非主键索引的叶子节点内容是主键的值。在 InnoDB 里，非主键索引也被称为二级索引 （secondary index）。

基于主键索引和普通索引的查询有什么 区别：主键索引直接查询，非主键索引要进行二次查询（回表）

自增主键插入可以避免页分裂。
```

聚簇索引：主键

非聚簇索引：

```
普通索引，唯一索引：普通索引的性能优于唯一索引（存在channel buffer）

联合索引，覆盖索引：针对普通索引的优化
```

## 不同存储结构的索引

索引是在存储引擎层实现的，而不是在服务器层实现的，所以不同存储引擎具有不同的索引类型和实现。

### 1. B+Tree 索引

是大多数 MySQL 存储引擎的默认索引类型。

因为不再需要进行全表扫描，只需要对树进行搜索即可，所以查找速度快很多。

因为 B+ Tree 的有序性，所以除了用于查找，还可以用于排序和分组。

可以指定多个列作为索引列，多个索引列共同组成键。

适用于全键值、键值范围和键前缀查找，其中键前缀查找只适用于最左前缀查找。如果不是按照索引列的顺序进行查找，则无法使用索引。

InnoDB 的 B+Tree 索引分为主索引和辅助索引。主索引的叶子节点 data 域记录着完整的数据记录，这种索引方式被称为聚簇索引。因为无法把数据行存放在两个不同的地方，所以一个表只能有一个聚簇索引。

辅助索引的叶子节点的 data 域记录着主键的值，因此在使用辅助索引进行查找时，需要先查找到主键值，然后再到主索引中进行查找。

### 2. 哈希索引

哈希索引能以 O(1) 时间进行查找，但是失去了有序性：

- 无法用于排序与分组；
- 只支持精确查找，无法用于部分查找和范围查找。

InnoDB 存储引擎有一个特殊的功能叫“自适应哈希索引”，当某个索引值被使用的非常频繁时，会在 B+Tree 索引之上再创建一个哈希索引，这样就让 B+Tree 索引具有哈希索引的一些优点，比如快速的哈希查找。

### 3. 全文索引

MyISAM 存储引擎支持全文索引，用于查找文本中的关键词，而不是直接比较是否相等。

查找条件使用 MATCH AGAINST，而不是普通的 WHERE。

全文索引使用倒排索引实现，它记录着关键词到其所在文档的映射。

InnoDB 存储引擎在 MySQL 5.6.4 版本中也开始支持全文索引。

### 4. 空间数据索引

MyISAM 存储引擎支持空间数据索引（R-Tree），可以用于地理数据存储。空间数据索引会从所有维度来索引数据，可以有效地使用任意维度来进行组合查询。

必须使用 GIS 相关的函数来维护数据。

## 索引优化

### 1. 建立单列索引

创建索引简单，但是在哪些列上创建索引则需要好好思考。可以考虑在where字句中出现列或者join字句中出现的列上建索引

### 2. 建立联合索引

在需要使用多个列作为条件进行查询时，使用多列索引比使用多个单列索引性能更好。例如下面的语句中，最好把 actor_id 和 film_id 设置为多列索引。

```sql
SELECT film_id, actor_ id FROM sakila.film_actor
WHERE actor_id = 1 AND film_id = 1;
```

### 3. 联合索引的顺序

让选择性最强的索引列放在前面。

索引的选择性是指：不重复的索引值和记录总数的比值。最大值为 1，此时每个记录都有唯一的索引与其对应。选择性越高，每个记录的区分度越高，查询效率也越高。

例如下面显示的结果中 customer_id 的选择性比 staff_id 更高，因此最好把 customer_id 列放在多列索引的前面。

```sql
SELECT COUNT(DISTINCT staff_id)/COUNT(*) AS staff_id_selectivity,
COUNT(DISTINCT customer_id)/COUNT(*) AS customer_id_selectivity,
COUNT(*)
FROM payment;
```

```html
   staff_id_selectivity: 0.0001
customer_id_selectivity: 0.0373
               COUNT(*): 16049
```

### 4. 前缀索引

对于 BLOB、TEXT 和 VARCHAR 类型的列，必须使用前缀索引，只索引开始的部分字符。

前缀长度的选取需要根据索引选择性来确定。

### 5. 覆盖索引

索引包含所有需要查询的字段的值。

具有以下优点：

- 索引通常远小于数据行的大小，只读取索引能大大减少数据访问量。
- 一些存储引擎（例如 MyISAM）在内存中只缓存索引，而数据依赖于操作系统来缓存。因此，只访问索引可以不使用系统调用（通常比较费时）。
- 对于 InnoDB 引擎，若辅助索引能够覆盖查询，则无需访问主索引。

### 6. 避免索引失效

## 索引失效

1. 如果条件中有or，即使其中有条件带索引也不会使用(这也是为什么尽量少用or的原因)
2. 对于多列索引，不是使用的第一部分，则不会使用索引
3. like查询是以%开头
4. 如果列类型是字符串，那一定要在条件中将数据使用引号引用起来,否则不使用索引
5. 如果mysql估计使用全表扫描要比使用索引快,则不使用索引

## 索引的优点

- 大大减少了服务器需要扫描的数据行数。
- 帮助服务器避免进行排序和分组，以及避免创建临时表（B+Tree 索引是有序的，可以用于 ORDER BY 和 GROUP BY 操作。临时表主要是在排序和分组过程中创建，不需要排序和分组，也就不需要创建临时表）。
- 将随机 I/O 变为顺序 I/O（B+Tree 索引是有序的，会将相邻的数据都存储在一起）。

## 索引的使用条件

- 对于非常小的表、大部分情况下简单的全表扫描比建立索引更高效；
- 对于中到大型的表，索引就非常有效；
- 但是对于特大型的表，建立和维护索引的代价将会随之增长。这种情况下，需要用到一种技术可以直接区分出需要查询的一组数据，而不是一条记录一条记录地匹配，例如可以使用分区技术。

# 事务

## 概念

事务指的是满足 ACID 特性的一组操作，可以通过 Commit 提交一个事务，也可以使用 Rollback 进行回滚。

## ACID

### 1. 原子性（Atomicity）

事务被视为不可分割的最小单元，事务的所有操作要么全部提交成功，要么全部失败回滚。

回滚可以用回滚日志来实现，回滚日志记录着事务所执行的修改操作，在回滚时反向执行这些修改操作即可。

### 2. 一致性（Consistency）

数据库在事务执行前后都保持一致性状态。在一致性状态下，所有事务对一个数据的读取结果都是相同的。

### 3. 隔离性（Isolation）

一个事务所做的修改在最终提交以前，对其它事务是不可见的。

### 4. 持久性（Durability）

一旦事务提交，则其所做的修改将会永远保存到数据库中。即使系统发生崩溃，事务执行的结果也不能丢失。

使用重做日志来保证持久性。

------

事务的 ACID 特性概念简单，但不是很好理解，主要是因为这几个特性不是一种平级关系：

- 只有满足一致性，事务的执行结果才是正确的。
- 在无并发的情况下，事务串行执行，隔离性一定能够满足。此时只要能满足原子性，就一定能满足一致性。
- 在并发的情况下，多个事务并行执行，事务不仅要满足原子性，还需要满足隔离性，才能满足一致性。
- 事务满足持久化是为了能应对数据库崩溃的情况。

![image](https://github.com/CyC2018/CS-Notes/raw/master/notes/pics/417bc315-4409-48c6-83e0-59e8d405429e.jpg)

## AUTOCOMMIT

MySQL 默认采用自动提交模式。也就是说，如果不显式使用`START TRANSACTION`语句来开始一个事务，那么每个查询都会被当做一个事务自动提交。

1.开启：set autocommit = 1；

2.关闭：set autocommit = 0 ;

3.查看：show variables like '%autocommit%'；

# 并发一致性问题

在并发环境下，事务的隔离性很难保证，因此会出现很多并发一致性问题。

## 丢失修改

T<sub>1</sub> 和 T<sub>2</sub> 两个事务都对一个数据进行修改，T<sub>1</sub> 先修改，T<sub>2</sub> 随后修改，T<sub>2</sub> 的修改覆盖了 T<sub>1</sub> 的修改。

## 读脏数据

T<sub>1</sub> 修改一个数据，T<sub>2</sub> 随后读取这个数据。如果 T<sub>1</sub> 撤销了这次修改，那么 T<sub>2</sub> 读取的数据是脏数据。

## 不可重复读

T<sub>2</sub> 读取一个数据，T<sub>1</sub> 对该数据做了修改。如果 T<sub>2</sub> 再次读取这个数据，此时读取的结果和第一次读取的结果不同。

## 幻影读

T<sub>1</sub> 读取某个范围的数据，T<sub>2</sub> 在这个范围内插入新的数据，T<sub>1</sub> 再次读取这个范围的数据，此时读取的结果和和第一次读取的结果不同。

------

产生并发不一致性问题主要原因是破坏了事务的隔离性，解决方法是通过并发控制来保证隔离性。并发控制可以通过封锁来实现，但是封锁操作需要用户自己控制，相当复杂。数据库管理系统提供了事务的隔离级别，让用户以一种更轻松的方式处理并发一致性问题。

# 隔离级别

## 未提交读（READ UNCOMMITTED）

事务中的修改，即使没有提交，对其它事务也是可见的。

## 提交读（READ COMMITTED）

一个事务只能读取已经提交的事务所做的修改。换句话说，一个事务所做的修改在提交之前对其它事务是不可见的。

## 可重复读（REPEATABLE READ）

保证在同一个事务中多次读取同样数据的结果是一样的。

## 可串行化（SERIALIZABLE）

强制事务串行执行。

需要加锁实现，而其它隔离级别通常不需要。

# 多版本并发控制

多版本并发控制（Multi-Version Concurrency Control, MVCC）是 MySQL 的 InnoDB 存储引擎实现隔离级别的一种具体方式，用于实现提交读和可重复读这两种隔离级别。而未提交读隔离级别总是读取最新的数据行，无需使用 MVCC。可串行化隔离级别需要对所有读取的行都加锁，单纯使用 MVCC 无法实现。

## 版本号

- 系统版本号：是一个递增的数字，每开始一个新的事务，系统版本号就会自动递增。
- 事务版本号：事务开始时的系统版本号。

## 隐藏的列

MVCC 在每行记录后面都保存着两个隐藏的列，用来存储两个版本号：

- 创建版本号：指示创建一个数据行的快照时的系统版本号；
- 删除版本号：如果该快照的删除版本号大于当前事务版本号表示该快照有效，否则表示该快照已经被删除了。

## Undo 日志

MVCC 使用到的快照存储在 Undo 日志中，该日志通过回滚指针把一个数据行（Record）的所有快照连接起来。

## 实现过程

以下实现过程针对可重复读隔离级别。

当开始一个事务时，该事务的版本号肯定大于当前所有数据行快照的创建版本号，理解这一点很关键。数据行快照的创建版本号是创建数据行快照时的系统版本号，系统版本号随着创建事务而递增，因此新创建一个事务时，这个事务的系统版本号比之前的系统版本号都大，也就是比所有数据行快照的创建版本号都大。

### 1. SELECT

多个事务必须读取到同一个数据行的快照，并且这个快照是距离现在最近的一个有效快照。但是也有例外，如果有一个事务正在修改该数据行，那么它可以读取事务本身所做的修改，而不用和其它事务的读取结果一致。

把没有对一个数据行做修改的事务称为 T，T 所要读取的数据行快照的创建版本号必须小于 T 的版本号，因为如果大于或者等于 T 的版本号，那么表示该数据行快照是其它事务的最新修改，因此不能去读取它。除此之外，T 所要读取的数据行快照的删除版本号必须大于 T 的版本号，因为如果小于等于 T 的版本号，那么表示该数据行快照是已经被删除的，不应该去读取它。

### 2. INSERT

将当前系统版本号作为数据行快照的创建版本号。

### 3. DELETE

将当前系统版本号作为数据行快照的删除版本号。

### 4. UPDATE

将当前系统版本号作为更新前的数据行快照的删除版本号，并将当前系统版本号作为更新后的数据行快照的创建版本号。可以理解为先执行 DELETE 后执行 INSERT。

## 快照读与当前读

### 1. 快照读

使用 MVCC 读取的是快照中的数据，这样可以减少加锁所带来的开销。

```sql
select * from table ...;
```

### 2. 当前读

读取的是最新的数据，需要加锁。以下第一个语句需要加 S 锁，其它都需要加 X 锁。

```sql
select * from table where ? lock in share mode;
select * from table where ? for update;
insert;
update;
delete;
```

# 查询性能优化

[一通骚操作，我把SQL执行效率提高了10000000倍](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247485281&idx=1&sn=2fbe43885baaf75f3027ebdaa9a85e7c&chksm=fba6ef62ccd16674004f843fd0926b3040cbb49329af81e907284255fdfc90498139794860de&mpshare=1&scene=1&srcid=05288ZaCH5LK0IUHvfPaJyHT#rd)

## 1. 开启慢查询

## 2. 使用 Explain 进行分析

Explain 用来分析 SELECT 查询语句，开发人员可以通过分析 Explain 结果来优化查询语句。

比较重要的字段有：

- select_type : 查询类型，有简单查询、联合查询、子查询等
- key : 使用的索引
- rows : 扫描的行数

## 3. 优化数据访问

### 1. 减少请求的数据量

- 只返回必要的列：最好不要使用 SELECT * 语句。
- 只返回必要的行：使用 LIMIT 语句来限制返回的数据。
- 缓存重复查询的数据：使用缓存可以避免在数据库中进行查询，特别在要查询的数据经常被重复查询时，缓存带来的查询性能提升将会是非常明显的。

### 2. 减少服务器端扫描的行数（索引优化）

最有效的方式是使用索引来覆盖查询。

## 4. 重构查询方式

### 1. 切分大查询

一个大查询如果一次性执行的话，可能一次锁住很多数据、占满整个事务日志、耗尽系统资源、阻塞很多小的但重要的查询。

```sql
DELETE FROM messages WHERE create < DATE_SUB(NOW(), INTERVAL 3 MONTH);
```

```sql
rows_affected = 0
do {
    rows_affected = do_query(
    "DELETE FROM messages WHERE create  < DATE_SUB(NOW(), INTERVAL 3 MONTH) LIMIT 10000")
} while rows_affected > 0

```

### 2. 分解大连接查询

将一个大连接查询分解成对每一个表进行一次单表查询，然后在应用程序中进行关联，这样做的好处有：

- 让缓存更高效。对于连接查询，如果其中一个表发生变化，那么整个查询缓存就无法使用。而分解后的多个查询，即使其中一个表发生变化，对其它表的查询缓存依然可以使用。
- 分解成多个单表查询，这些单表查询的缓存结果更可能被其它查询使用到，从而减少冗余记录的查询。
- 减少锁竞争；
- 在应用层进行连接，可以更容易对数据库进行拆分，从而更容易做到高性能和可伸缩。
- 查询本身效率也可能会有所提升。例如下面的例子中，使用 IN() 代替连接查询，可以让 MySQL 按照 ID 顺序进行查询，这可能比随机的连接要更高效。

```sql
SELECT * FROM tab
JOIN tag_post ON tag_post.tag_id=tag.id
JOIN post ON tag_post.post_id=post.id
WHERE tag.tag='mysql';

```

```sql
SELECT * FROM tag WHERE tag='mysql';
SELECT * FROM tag_post WHERE tag_id=1234;
SELECT * FROM post WHERE post.id IN (123,456,567,9098,8904);

```

# 封锁

## 封锁粒度

MySQL 中提供了两种封锁粒度：行级锁以及表级锁。

应该尽量只锁定需要修改的那部分数据，而不是所有的资源。锁定的数据量越少，发生锁争用的可能就越小，系统的并发程度就越高。

但是加锁需要消耗资源，锁的各种操作（包括获取锁、释放锁、以及检查锁状态）都会增加系统开销。因此封锁粒度越小，系统开销就越大。

在选择封锁粒度时，需要在锁开销和并发程度之间做一个权衡。

## 封锁类型

### 1. 读写锁

- 排它锁（Exclusive），简写为 X 锁，又称写锁。
- 共享锁（Shared），简写为 S 锁，又称读锁。

有以下两个规定：

- 一个事务对数据对象 A 加了 X 锁，就可以对 A 进行读取和更新。加锁期间其它事务不能对 A 加任何锁。
- 一个事务对数据对象 A 加了 S 锁，可以对 A 进行读取操作，但是不能进行更新操作。加锁期间其它事务能对 A 加 S 锁，但是不能加 X 锁。

### 2. 意向锁

使用意向锁（Intention Locks）可以更容易地支持多粒度封锁。

在存在行级锁和表级锁的情况下，事务 T 想要对表 A 加 X 锁，就需要先检测是否有其它事务对表 A 或者表 A 中的任意一行加了锁，那么就需要对表 A 的每一行都检测一次，这是非常耗时的。

意向锁在原来的 X/S 锁之上引入了 IX/IS，IX/IS 都是表锁，用来表示一个事务想要在表中的某个数据行上加 X 锁或 S 锁。有以下两个规定：

- 一个事务在获得某个数据行对象的 S 锁之前，必须先获得表的 IS 锁或者更强的锁；
- 一个事务在获得某个数据行对象的 X 锁之前，必须先获得表的 IX 锁。

通过引入意向锁，事务 T 想要对表 A 加 X 锁，只需要先检测是否有其它事务对表 A 加了 X/IX/S/IS 锁，如果加了就表示有其它事务正在使用这个表或者表中某一行的锁，因此事务 T 加 X 锁失败。

### 3. 乐观锁VS悲观锁

https://www.cnblogs.com/xuyuanjia/p/6027414.html

悲观锁：

```
顾名思义，就是很悲观，每次去拿数据的时候都认为别人会修改，所以每次在拿数据的时候都会上锁，这样别人想拿这个数据就会block
直到它拿到锁但如果经常产生冲突，上层应用会不断的进行retry，这样乐观锁反倒是降低了性能，所以这种情况下用悲观锁就比较合适。

```

```
select * from account where name=”Erica” for update
这条 sql 语句锁定了 account 表中所有符合检索条件（ name=”Erica” ）的记录。

```

乐观锁：

```
每次去拿数据的时候都认为别人不会修改，所以不会上锁，但是在更新的时候会判断一下在此期间别人有没有去更新这个数据，可以使
用版本号等机制。乐观锁适用于多读写比较少的应用类型，这样可以提高吞吐量

```

```
	UPDATE tab1 SET col1=1,version=version+1 WHERE version=#version#

```

## 行锁优化

### 两阶段锁

1、获取锁。2、事务提交释放锁

如果你的事务中需要锁多个行，要把最可能造成锁冲突、 最可能影响并发度的锁的申请时机尽量往后放

### 死锁处理方式

1、超时时间：时间难以控制 2、死锁检测：消耗太大

### 分段锁的思想

减少死锁的主要方向：就是控制访问相同资源的并发事务量将一行改成逻辑上的多行来减少锁冲突

## Next-Key Locks

Next-Key Locks 是 MySQL 的 InnoDB 存储引擎的一种锁实现。

MVCC 不能解决幻影读问题，Next-Key Locks 就是为了解决这个问题而存在的。在可重复读（REPEATABLE READ）隔离级别下，使用 MVCC + Next-Key Locks 可以解决幻读问题。

### Record Locks

锁定一个记录上的索引，而不是记录本身。

如果表没有设置索引，InnoDB 会自动在主键上创建隐藏的聚簇索引，因此 Record Locks 依然可以使用。

### Gap Locks

锁定索引之间的间隙，但是不包含索引本身。例如当一个事务执行以下语句，其它事务就不能在 t.c 中插入 15。

```sql
SELECT c FROM t WHERE c BETWEEN 10 and 20 FOR UPDATE;

```

### Next-Key Locks

它是 Record Locks 和 Gap Locks 的结合，不仅锁定一个记录上的索引，也锁定索引之间的间隙。例如一个索引包含以下值：10, 11, 13, and 20，那么就需要锁定以下区间：

```sql
(-∞, 10]
(10, 11]
(11, 13]
(13, 20]
(20, +∞)

```

# 存储引擎

## InnoDB

**事务+行级锁+外键**

**是 MySQL 默认的事务型存储引擎，只有在需要它不支持的特性时，才考虑使用其它存储引擎。**

实现了四个标准的**隔离级别**，默认级别是可重复读（REPEATABLE READ）。在可重复读隔离级别下，通过多版本并发控制（MVCC）+ 间隙锁（Next-Key Locking）防止幻影读。

**主索引是聚簇索引**，在索引中保存了数据，从而避免直接读取磁盘，因此对查询性能有很大的提升。

内部做了很多优化，包括从磁盘读取数据时采用的可预测性读、能够加快读操作并且自动创建的自适应哈希索引、能够加速插入操作的插入缓冲区等。

支持真正的在线热备份（redo log）。其它存储引擎不支持在线热备份，要获取一致性视图需要停止对所有表的写入，而在读写混合场景中，停止写入可能也意味着停止读取。

## MyISAM

**不支持事务。不支持行级锁，读的效率高，可以作为从库的引擎**

**设计简单，数据以紧密格式存储。对于只读数据，或者表比较小、可以容忍修复操作，则依然可以使用它。**

提供了大量的特性，包括压缩表、空间数据索引等。

**不支持事务。**

**不支持行级锁，**只能对整张表加锁，读取时会对需要读到的所有表加共享锁，写入时则对表加排它锁。但在表有读取操作的同时，也可以往表中插入新的记录，这被称为并发插入（CONCURRENT INSERT）。

可以手工或者自动执行检查和修复操作，但是和事务恢复以及崩溃恢复不同，可能导致一些数据丢失，而且修复操作是非常慢的。

如果指定了 DELAY_KEY_WRITE 选项，在每次修改执行完成时，不会立即将修改的索引数据写入磁盘，而是会写到内存中的键缓冲区，只有在清理键缓冲区或者关闭表的时候才会将对应的索引块写入磁盘。这种方式可以极大的提升写入性能，但是在数据库或者主机崩溃时会造成索引损坏，需要执行修复操作。

## 比较

- 事务：InnoDB 是事务型的，可以使用 Commit 和 Rollback 语句。
- 并发：MyISAM 只支持表级锁，而 InnoDB 还支持行级锁。
- 外键：InnoDB 支持外键。
- 备份：InnoDB 支持在线热备份。
- 崩溃恢复：MyISAM 崩溃后发生损坏的概率比 InnoDB 高很多，而且恢复的速度也更慢。
- 其它特性：MyISAM 支持压缩表和空间数据索引。

# 数据类型

## 整型

TINYINT, SMALLINT, MEDIUMINT, INT, BIGINT 分别使用 8, 16, 24, 32, 64 位存储空间，一般情况下越小的列越好。

INT(11) 中的数字只是规定了交互工具显示字符的个数，对于存储和计算来说是没有意义的。

## 浮点数

FLOAT 和 DOUBLE 为浮点类型，DECIMAL 为高精度小数类型。CPU 原生支持浮点运算，但是不支持 DECIMAl 类型的计算，因此 DECIMAL 的计算比浮点类型需要更高的代价。

FLOAT、DOUBLE 和 DECIMAL 都可以指定列宽，例如 DECIMAL(18, 9) 表示总共 18 位，取 9 位存储小数部分，剩下 9 位存储整数部分。

## 字符串

主要有 CHAR 和 VARCHAR 两种类型，一种是定长的，一种是变长的。

VARCHAR 这种变长类型能够节省空间，因为只需要存储必要的内容。但是在执行 UPDATE 时可能会使行变得比原来长，当超出一个页所能容纳的大小时，就要执行额外的操作。MyISAM 会将行拆成不同的片段存储，而 InnoDB 则需要分裂页来使行放进页内。

在进行存储和检索时，会保留 VARCHAR 末尾的空格，而会删除 CHAR 末尾的空格。

## TEXT 与 BLOB

一般在保存少量字符串的时候，我们会选择 CHAR 或者 VARCHAR；而在保存较大文本时，通常会选择使用 TEXT 或者 BLOB，二者之间的主要差别是 BLOB 能用来保存二进制数据，比如照片；而 TEXT 只能保存字符数据，比如一篇文章或者日记

BLOB 和 TEXT 值会引起一些性能问题，特别是在执行了大量的删除操作时。删除操作会在数据表中留下很大的“空洞”，以后填入这些“空洞”的记录在插入的性能上会有影响。为了提高性能，建议定期使用 OPTIMIZE TABLE 功能对这类表进行碎片整理，避免因为“空洞”导致性能问题。

## 时间和日期

MySQL 提供了两种相似的日期时间类型：DATETIME 和 TIMESTAMP。

### 1. DATETIME

能够保存从 1000 年到 9999 年的日期和时间，精度为秒，使用 8 字节的存储空间。

它与时区无关。

默认情况下，MySQL 以一种可排序的、无歧义的格式显示 DATETIME 值，例如“2008-01-16 22<span>:</span>37<span>:</span>08”，这是 ANSI 标准定义的日期和时间表示方法。

### 2. TIMESTAMP

和 UNIX 时间戳相同，保存从 1970 年 1 月 1 日午夜（格林威治时间）以来的秒数，使用 4 个字节，只能表示从 1970 年到 2038 年。

它和时区有关，也就是说一个时间戳在不同的时区所代表的具体时间是不同的。

MySQL 提供了 FROM_UNIXTIME() 函数把 UNIX 时间戳转换为日期，并提供了 UNIX_TIMESTAMP() 函数把日期转换为 UNIX 时间戳。

默认情况下，如果插入时没有指定 TIMESTAMP 列的值，会将这个值设置为当前时间。

应该尽量使用 TIMESTAMP，因为它比 DATETIME 空间效率更高。

# 分区分表

https://www.cnblogs.com/phpshen/p/6198375.html
https://blog.csdn.net/qq_21873747/article/details/80668939
https://www.cnblogs.com/phpper/p/6937896.html

## 分区

就是把一张表的数据分成N个区块，在逻辑上看最终只是一张表，但底层是由N个物理区块组成的

## 分表

逻辑上不是一张表，物理上也不是一张表

### 水平切分

水平切分又称为 Sharding，它是将同一个表中的记录拆分到多个结构相同的表中。

当一个表的数据不断增多时，Sharding 是必然的选择，它可以将数据分布到集群的不同节点上，从而缓存单个数据库的压力。

### 垂直切分

垂直切分是将一张表按列切分成多个表，通常是按照列的关系密集程度进行切分，也可以利用垂直切分将经常被使用的列和不经常被使用的列切分到不同的表中。

在数据库的层面使用垂直切分将按数据库中表的密集程度部署到不同的库中，例如将原来的电商数据库垂直切分成商品数据库、用户数据库等。

## Sharding 策略

- 哈希取模：hash(key) % N；
- 范围：可以是 ID 范围也可以是时间范围；
- 映射表：使用单独的一个数据库来存储映射关系。

## Sharding 存在的问题

### 1. 事务问题

使用分布式事务来解决，比如 XA 接口。

### 2. 连接

可以将原来的连接分解成多个单表查询，然后在用户程序中进行连接。

### 3. ID 唯一性

- 使用全局唯一 ID（GUID）
- 为每个分片指定一个 ID 范围
- 分布式 ID 生成器 (如 Twitter 的 Snowflake 算法)

# 集群

## 主从复制：同步问题

主要涉及三个线程：binlog 线程、I/O 线程和 SQL 线程。

- **binlog 线程** ：负责将主服务器上的数据更改写入二进制日志（Binary log）中。
- **I/O 线程** ：负责从主服务器上读取二进制日志，并写入从服务器的中继日志（Relay log）。
- **SQL 线程** ：负责读取中继日志，解析出主服务器已经执行的数据更改并在从服务器中重放（Replay）。

![](https://github.com/CyC2018/CS-Notes/raw/master/notes/pics/master-slave.png)

## 读写分离

1、what 读写分离

读写分离，基本的原理是让主数据库处理事务性增、改、删操作（INSERT、UPDATE、DELETE），而从数据库处理SELECT查询操作。数据库复制被用来把事务性操作导致的变更同步到集群中的从数据库。

2、why 那么为什么要读写分离呢？

因为数据库的“写”（写10000条数据到oracle可能要3分钟）操作是比较耗时的。
但是数据库的“读”（从oracle读10000条数据可能只要5秒钟）。
所以读写分离，解决的是，数据库的写入，影响了查询的效率。

3、when 什么时候要读写分离？

数据库不一定要读写分离，如果程序使用数据库较多时，而更新少，查询多的情况下会考虑使用，利用数据库 主从同步 。可以减少数据库压力，提高性能。当然，数据库也有其它优化方案。memcache 或是 表折分，或是搜索引擎。都是解决方法。

读写分离常用代理方式来实现，代理服务器接收应用层传来的读写请求，然后决定转发到哪个服务器。

## 高可用

https://baijiahao.baidu.com/s?id=1597294744568311877&wfr=spider&for=pc
https://www.cnblogs.com/stateis0/p/9062133.html

1. 主备选举

Paxos,RAFT算法：基于投票机制的选举算法

2. 主备切换

切换引擎，要进行主从复制

# 范式

[数据库设计第三范式---一二三范式介绍](https://blog.csdn.net/h330531987/article/details/71194540)

高级别范式的依赖于低级别的范式，1NF 是最低级别的范式。

## 1. 第一范式 (1NF)

属性不可分。

## 2. 第二范式 (2NF)

数据库表中不存在非关键字段对任一候选关键字段的部分函数依赖

## 3. 第三范式 (3NF)

数据表中如果不存在非关键字段对任一候选关键字段的传递函数依赖

# count(*)优化

### count(*)原理

MyISAM 引擎把一个表的总行数存在了磁盘上，因此执行 count(*) 的时候会直接返回 这个数，效率很高；

而 InnoDB 引擎就麻烦了，它执行 count(*) 的时候，需要把数据一行一行地从引擎里面 读出来，然后累积计数。（由于MVCC）

### 用缓存系统保存计数

包括两个步骤：更新缓存，写数据库

会出现的问题：

1、丢失更新：还没写入redis，redis宕机了

2、数据不一致：由于更新缓存和写数据库没有放到一个事务里去，当有另外的一个事务先查询出有缓存更新了，但是数据库没有更新，就会出现不一致的问题

### 在数据库保存计数

1、解决了丢失更新

2、解决了数据不一致：两个表的操作可以都放入同一个事务执行

### 不同的 count 用法

原则：count()里面有什么就需要返回什么，只有count(*)做过优化

1、对于 **count(主键 id)** 来说，

InnoDB 引擎会遍历整张表，把每一行的 id 值都取出来，返 回给 server 层。server 层拿到 id 后，判断是不可能为空的，就按行累加。

2、对于 **count(1)** 来说，

InnoDB 引擎遍历整张表，但不取值。server 层对于返回的每一 行，放一个数字“1”进去，判断是不可能为空的，按行累加。

单看这两个用法的差别的话，你能对比出来，count(1) 执行得要比 count(主键 id) 快。因 为从引擎返回 id 会涉及到解析数据行，以及拷贝字段值的操作。

3、对于 **count(字段)** 来说：

如果这个“字段”是定义为 not null 的话，一行行地从记录里面读出这个字段，判断不 能为 null，按行累加；
如果这个“字段”定义允许为 null，那么执行的时候，判断到有可能是 null，还要把值 取出来再判断一下，不是 null 才累加。
3、**count(*)**

并不会把全部字段取出来，而是专门做了优化，不取值。 count(*) 肯定不是 null，按行累加。

按照效率排序的话，count(字段)<count(主键 id)<count(1)≈count(*) ，所 以我建议你，尽量使用 count(*)

# 分析工具

## show profiles

[link](https://blog.csdn.net/gaoshan12345678910/article/details/78840158)

执行的SQL语句都将记录其资源开销，诸如IO，上下文切换，CPU，Memory

```
show profile memory for query 2 ;  
show profile block io,cpu for query 2;

```

## explain

https://www.cnblogs.com/yycc/p/7338894.html

explain显示了mysql如何使用索引来处理select语句以及连接表。可以帮助选择更好的索引和写出更优化的查询语句。

**key：真正使用到的索引**

**rows：MYSQL认为必须检查的用来返回请求数据的行数**

extra：

```
Using filesort: 看到这个的时候，查询就需要优化了。MYSQL需要进行额外的步骤来发现如何对返回的行排序。它根据连接类型
以及存储排序键值和匹配条件的全部行的行指针来排序全部行

Using temporary 看到这个的时候，查询需要优化了。这里，MYSQL需要创建一个临时表来存储结果，这通常发生在对不同的列集
进行ORDER BY上，而不是GROUP BY上

```

## 慢查询

https://www.cnblogs.com/saneri/p/6656161.html

# 日志系统

https://blog.csdn.net/wanbin6470398/article/details/81941586

## 一条SQL查询语句是如何执行的

MySQL 可以分为 Server 层和存储引擎层两部分

**Server 层包括连接器、查询缓存、分析器、优化器、执行器**等，涵盖 MySQL 的大多数核 心服务功能，以及所有的内置函数（如日期、时间、数学和加密函数等），所有跨存储引 擎的功能都在这一层实现，比如存储过程、触发器、视图等。

**而存储引擎层负责数据的存储和提取**。其架构模式是插件式的，支持 InnoDB、 MyISAM、Memory 等多个存储引擎。

**不同的存储引擎共用一个Server 层，也就是从连接器到执行器的部分**

## redo

Write-Ahead Logging，它的关键点就是先写日志，再写磁盘有了 redo log，InnoDB 就可以保证即使数据库发生异常重启，之前提交的记录都不会丢 失，这个能力称为crash-safe。

## binlog

binlog记录了对MySQL数据库执行更改的所有操作

redo log 是 InnoDB 引擎特有的日志，而 Server 层也有自己的日志，称为 binlog（归档日志）

### mysql的两阶段提交协议

MySQL通过两阶段提交解决了服务层binlog与引擎层Innodb的redo log的一致性与协同问题。

第一阶段：事务写redo-log

第二阶段：事务写Binlog

事务提交

## undo

https://m.2cto.com/database/201806/754458.html

为了满足事务的原子性，在操作任何数据之前，首先将数据备份到一个地方(这个存储数据备份的地方称为Undo Log)。然后进行数据的修改。如果出现了错误或者用户执行了ROLLBACK语句，系统可以利用Undo Log中的备份将数据恢复到事务开始之前的状态。

快照的存放地方

## 从innodb事务执行流程感受日志系统

https://www.linuxidc.com/Linux/2018-04/152080.htm

update he set name='liuwenhe' where id=5;

1）事务开始

2）对id=5这条数据上排他锁，并且给5两边的临近范围加gap锁，防止别的事务insert新数据；

3）将需要修改的数据页PIN到innodb_buffer_cache中；

4）记录id=5的数据到undo log.

5）记录修改id=5的信息到redo log.

6）修改id=5的name='liuwenhe'.

7）刷新innodb_buffer_cache中脏数据到底层磁盘，这个过程和commit无关；

8）commit，触发page cleaner线程把redo从redo buffer cache中刷新到底层磁盘，并且刷新innodb_buffer_cache中脏数据到底层磁盘也会触发对redo的刷新；

9）记录binlog （记录到binlog_buffer_cache中）

10）事务结束；

# 参考资料

[极客时间-mysql实战](http://note.youdao.com/noteshare?id=f3d7d7dc81654fae3b955a2891b51eec&sub=552A87F5FF7442CF95500CC258BC6E80)