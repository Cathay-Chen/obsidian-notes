## Linux 安装 Go 1.18

```shell
$ tee -a $HOME/.bashrc <<'EOF'
# Go envs
export GOVERSION=go1.18.3 # Go 版本设置
export GO_INSTALL_DIR=$HOME/go # Go 安装目录
export GOROOT=$GO_INSTALL_DIR/$GOVERSION # GOROOT 设置
export GOPATH=$WORKSPACE/golang # GOPATH 设置
export PATH=$GOROOT/bin:$GOPATH/bin:$PATH # 将 Go 语言自带的和通过 go install 安装的二进制文件加入到 PATH 路径中
export GO111MODULE="on" # 开启 Go moudles 特性
export GOPROXY=https://goproxy.cn,direct # 安装 Go 模块时，代理服务器设置
export GOPRIVATE=
export GOSUMDB=off # 关闭校验 Go 依赖包的哈希值
EOF
```

因为 Go 以后会用 Go modules 来管理依赖，所以我建议你将 GO111MODULE 设置为 on。

在使用模块的时候，$GOPATH 是无意义的，不过它还是会把下载的依赖储存在 $GOPATH/pkg/mod 目录中，也会把 go install 的二进制文件存放在 $GOPATH/bin 目录中。

另外，我们还要将 `$GOPATH/bin`、`$GOROOT/bin` 加入到 Linux 可执行文件搜索路径中。这样一来，我们就可以直接在 bash shell 中执行 go 自带的命令，以及通过 go install 安装的命令。


![[Pasted image 20221202154216.png]]


go1.18.3 支持多模块工作区，所以这里也需要初始化工作区。

```shell
$ mkdir -p $GOPATH && cd $GOPATH
$ go work init
$ go env GOWORK # 执行此命令，查看 go.work 工作区文件路径
/home/going/workspace/golang/go.work
```



## ProtoBuf 编译环境安装
