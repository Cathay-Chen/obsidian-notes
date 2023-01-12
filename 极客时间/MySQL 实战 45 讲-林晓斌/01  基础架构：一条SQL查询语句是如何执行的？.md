

## MySQL 的逻辑架构

逻辑架构图:

![[Pasted image 20230112223415.png]]


MySQL 可以分为 Server 层和存储引擎层两部分。

- Server 层：包括连接器、查询缓存、分析器、优化器、执行器等，涵盖 MySQL 的大多数核心服务功能，以及所有的内置函数（如日期、时间、数学和加密函数等），所有跨存储引擎的功能都在这一层实现，比如存储过程、触发器、视图等。
- 存储引擎层：负责数据的存储和提取。其架构模式是插件式的，支持 InnoDB、MyISAM、Memory 等多个存储引擎。现在最常用的存储引擎是 InnoDB，它从 MySQL 5.5.5 版本开始成为了默认存储引擎。

> 不同的存储引擎共用一个Server 层，也就是从连接器到执行器的部分。

### 连接器

连接器负责跟客户端建立连接、获取权限、维持和管理连接。连接命令一般是这么写的：

```bash
mysql -h$ip -P$port -u$user -p
```

一个用户成功建立连接后，即使你用管理员账号对这个用户的权限做了修改，也不会影响已经存在连接的权限。修改完成后，只有再新建的连接才会使用新的权限设置。

可以使用 `show processlist`  命令查看所有的连接一些信息。

![[Pasted image 20230112224425.png]]

可以使用 `wait_timeout` 参数控制连接器闲置自动断开时间。默认是 8 小时。修改方法如下：

```bash
mysql> set global wait_timeout = 280000;
Query OK, 0 rows affected (0.00 sec)

mysql>
```

如果想让MySQL无论从哪种客户端都能让 `wait_timeout` 一致，那就要同时设置 `global wait_timeout` 和 `global interactive_timeout`了。例如:

```bash
mysql> set global wait_timeout = 280000;
Query OK, 0 rows affected (0.00 sec)

mysql> set global interactive_timeout = 280000;
Query OK, 0 rows affected (0.00 sec)

mysql>
```

> 也可以通过 my.conf 设置

大量使用长连接可能会有些时候 MySQL 占用内存涨得特别快，这是因为 MySQL 在执行过程中临时使用的内存是管理在连接对象里面的。这些资源会在连接断开的时候才释放。所以如果长连接累积下来，可能导致内存占用太大，被系统强行杀掉（OOM），从现象看就是 MySQL 异常重启了。

怎么解决这个问题呢？你可以考虑以下两种方案。
1. 定期断开长连接。使用一段时间，或者程序里面判断执行过一个占用内存的大查询后，
断开连接，之后要查询再重连。
2. 如果你用的是 MySQL 5.7 或更新版本，可以在每次执行一个比较大的操作后，通过执行
mysql_reset_connection 来重新初始化连接资源。这个过程不需要重连和重新做权限验
证，但是会将连接恢复到刚刚创建完时的状态。