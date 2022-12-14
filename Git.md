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

可以看到倒数第 3 次提交的 Commit Message 是：docs(docs): append test line 'update\$i' to README.md，其中 update$i 正常应该是 update2。

2. 修改倒数第 3 次提交 commit 的 message。

在 Git 仓库下直接执行命令 git rebase -i 55892fa，然后会进入一个交互界面。在交互界面中，修改最近一次的 Commit Message。这里我们使用 reword 或者 r，保留倒数第 3 次的变更信息，但是修改其 message，如下图所示：

![[Pasted image 20221214161313.png]]

修改完成后执行:wq 保存，还会跳转到一个新的交互页面，如下图所示：

![[Pasted image 20221214161348.png]]

修改完成后执行:wq 保存，退出编辑器之后，会在命令行显示该 commit 的 message 的更新结果：

```
[detached HEAD 5a26aa2] docs(docs): append test line 'update2' to README.md
 Date: Fri Sep 18 13:45:54 2020 +0800
 1 file changed, 1 insertion(+)
Successfully rebased and updated refs/heads/master.
```

Successfully rebased and updated refs/heads/master.说明 rebase 成功，其实这里完成了两个步骤：更新 message，更新该 commit 的 HEAD 指针。

>注意：这里一定要传入想要变更 Commit Message 的父 commit ID：git rebase -i <父 commit ID>。

3. 查看倒数第 3 次 commit 的 message 是否被更新。

```
$ git log --oneline
7157e9e docs(docs): append test line 'update3' to README.md
5a26aa2 docs(docs): append test line 'update2' to README.md
55892fa docs(docs): append test line 'update1' to README.md
89651d4 docs(doc): add README.md
```

可以看到，倒数第 3 次 commit 的 message 成功被修改为期望的内容。

这里有两点需要你注意：

- Commit Message 是 commit 数据结构中的一个属性，如果 Commit Message 有变更，则 commit ID 一定会变，git commit --amend 只会变更最近一次的 commit ID，但是 git rebase -i 会变更父 commit ID 之后所有提交的 commit ID。
- 如果当前分支有未 commit 的代码，需要先执行 git stash 将工作状态进行暂存，当修改完成后再执行 git stash pop 恢复之前的工作状态。