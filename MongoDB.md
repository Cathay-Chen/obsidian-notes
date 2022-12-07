
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

我们通过 use admin 指令切换到 admin 数据库，再通过 db.auth("用户名"，"用户密码") 验证用户登录权限。如果返回 1 表示验证成功；如果返回 0 表示验证失败。具体的命令如下：

```shell
## 创建管理员账户。
use admin

db.createUser({user:"${MONGO_ADMIN_USERNAME}",pwd:"${MONGO_ADMIN_PASSWORD}",roles:["root"]})  

db.auth("${MONGO_ADMIN_USERNAME}", "${MONGO_ADMIN_PASSWORD}")

## 添加 Datebase 管理员
use iam_analytics 

db.createUser({user:"${MONGO_USERNAME}",pwd:"${MONGO_PASSWORD}",roles:["dbOwner"]})  

db.auth("${MONGO_USERNAME}", "${MONGO_PASSWORD}")
```