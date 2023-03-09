## 一、安装 vim-go

[[Linux]] 安装命令如下

```shell
$ rm -f $HOME/.vim; mkdir -p ~/.vim/pack/plugins/start/
$ git clone --depth=1 https://github.com/fatih/vim-go.git ~/.vim/pack/plugins/start/vim-go
```

## 二、Go 工具安装

vim-go 会用到一些 Go 工具，比如在函数跳转时会用到 guru、godef 工具，在格式化时会用到 goimports，所以你也需要安装这些工具。安装方式如下：执行 vi /tmp/test.go，然后输入 :GoInstallBinaries 安装 vim-go 需要的工具。

## 三、使用说明

![[Pasted image 20221202173126.png]]