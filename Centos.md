#linux/centos 

## 关闭 SElinux

```shell
$ sudo setenforce 0
$ sudo sed -i 's/^SELINUX=.*$/SELINUX=disabled/' /etc/selinux/config # 永久关闭 SELINUX
```

