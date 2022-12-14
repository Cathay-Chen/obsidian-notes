## 基本配置
```shell
$ git config --global user.name "cathay" # 用户名改成自己的
$ git config --global user.email "cathaycchen@gmail.com" # 邮箱改成自己的
$ git config --global credential.helper store # 设置 Git，保存用户名和密码
$ git config --global core.longpaths true # 解决 Git 中 'Filename too long' 的错误
```


在 Git 中，我们会把非 ASCII 字符叫做 Unusual 字符。这类字符在 Git 输出到终端的时候默认是用 8 进制转义字符输出的（以防乱码），但现在的终端多数都支持直接显示非 ASCII 字符，所以我们可以关闭掉这个特性，具体的命令如下：

```shell
$ git config --global core.quotepath off
```

GitHub 限制最大只能克隆 100M 的单个文件，为了能够克隆大于 100M 的文件，我们还需要安装 Git Large File Storage，安装方式如下：

```shell
$ git lfs install --skip-repo
```

## 修改最近一次 commit 的 message
git commit --amend：修改最近一次 commit 的 message

## 修改某次 commit 的 message

如果我们想修改的 Commit Message 不是最近一次的 Commit Message，可以通过 git rebase -i <父 commit ID>命令来修改。这个命令在实际开发中使用频率比较高，我们一定要掌握。具体来说，使用它主要分为 4 步。

1. 查看当前分支的日志记录。
	```
	$ git log --oneline
	1d6289f docs(docs): append test line 'update3' to README.md
	a38f808 docs(docs): append test line 'update$i' to README.md
	55892fa docs(docs): append test line 'update1' to README.md
	89651d4 docs(doc): add README.md
	```

1. 修改倒数第 3 次提交 commit 的 message。
2. 查看倒数第 3 次 commit 的 message 是否被更新。