
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

```s
mongosh --quiet "mongodb://${MONGO_HOST}:${MONGO_PORT}" << EOF  
use admin  
db.createUser({user:"${MONGO_ADMIN_USERNAME}",pwd:"${MONGO_ADMIN_PASSWORD}",roles:["root"]})  
db.auth("${MONGO_ADMIN_USERNAME}", "${MONGO_ADMIN_PASSWORD}")  
EOF
```