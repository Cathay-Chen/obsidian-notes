- Redis 命令行连接
	`redis-cli -h host -p port -a password`
- 查看 Redis 版本等信息
	[INFO doc]( http://www.redis.cn/commands/info.html )
	`info [section]`

## Keys
### DEL key [key ...]  
[del 命令 -- Redis中国用户组（CRUG）](http://www.redis.cn/commands/del.html)

删除指定的一批 keys，如果删除中的某些 key 不存在，则直接忽略。
**返回值**
[integer-reply](http://www.redis.cn/topics/protocol.html#integer-reply) ： 被删除的 keys 的数量

```shell
redis> SET key1 "Hello"
OK
redis> SET key2 "World"
OK
redis> DEL key1 key2 key3
(integer) 2
redis> 
```