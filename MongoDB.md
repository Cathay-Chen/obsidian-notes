#mongodb

# #  MongoDB 中的一些符号
| 符号 | 含义     |
| ---- | -------- |
| $gt  | 大于     |
| $gte | 大于等于 |
| $lt  | 小于     |
| $lte | 小于等于 |
| $ne  | 不等于   |
| $in  | IN       |
| $nin | NOT IN   |
| $mod | 取余     |
| $NOT | 非       |
| $OR  | 或       |
 
## 开启外网访问

```shell
sudo -S sed -i '/bindIp/{s/127.0.0.1/0.0.0.0/}' /etc/mongod.conf  
sudo -S sed -i '/^#security/a\security:\n  authorization: enabled' /etc/mongod.conf
```

## 添加用户及赋权限

我们通过 use admin 指令切换到 admin 数据库，再通过 db.auth("用户名"，"用户密码") 验证用户登录权限。如果返回 1 表示验证成功；如果返回 0 表示验证失败。

如果想删除用户，可以使用 db.dropUser("用户名") 命令。

db.createUser 用到了以下 3 个参数。
- user: 用户名。
- pwd: 用户密码。
- roles: 用来设置用户的权限，比如读、读写、写等。

因为 admin 用户具有 MongoDB 的 Root 权限，权限过大安全性会降低。为了提高安全性，我们还需要创建一个 iam 普通用户来连接和操作 MongoDB。

```MongoDB
## 创建管理员账户。
use admin

db.createUser({user:"${MONGO_ADMIN_USERNAME}",pwd:"${MONGO_ADMIN_PASSWORD}",roles:["root"]})  

db.auth("${MONGO_ADMIN_USERNAME}", "${MONGO_ADMIN_PASSWORD}")

## 添加 Datebase 管理员
use iam_analytics 

db.createUser({user:"${MONGO_USERNAME}",pwd:"${MONGO_PASSWORD}",roles:["dbOwner"]})  

db.auth("${MONGO_USERNAME}", "${MONGO_PASSWORD}")

## 查看所有用户
show users
```