> [[Linux]] 使用小记

## 创建新用户流程

### 1. 创建普通用户
```shell
# useradd username # 创建 username 用户，通过 username 用户登录开发机进行开发
# passwd username # 设置密码
Changing password for user going.
New password:
Retype new password:
passwd: all authentication tokens updated successfully.
```

###  2. 添加 sudoers，让添加用户可以使用 `sudo`
```shell
# sed -i '/^root.*ALL=(ALL).*ALL/a\going\tALL=(ALL) \tALL' /etc/sudoers
```




