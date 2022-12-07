#mysql

## 创建用户

```mysql
grant all on iam.* TO iam@127.0.0.1 identified by 'iam59!z$';

flush privileges;
```

## 执行sql文件

```mysql
source configs/iam.sql;
```

