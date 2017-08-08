# 删除远程分支和tag

## 删除远程分支

* 在Git v1.7.0之后，可以使用这种语法删除远程分支：

```
git push origin --delete <branchName>
```

* 否则，可以使用这种语法，推送一个空分支到远程分支，其实就相当于删除远程分支：

```
git push origin :<branchName>
```

## 删除远程tag

* 在Git v1.7.0之后，可以使用这种语法删除tag

```
git push origin --delete tag <tagName>
```

* 这是删除tag的方法，推送一个空tag到远程tag:

```
git tag -d <tagName>
git push origin :refs/tags/<tagName>
```

## 删除不存在对应远程分支的本地分支

假设这样一种情况:

1. 我创建了本地分支b1并push到远程分支origin/b1;
2. 其他人在本地使用fetch或pull创建了本地的b1分支；
3. 我删除了origin/b1远程分支；
4. 其他人再次执行fetch或者pull并不会删除这个他们本地的b1分支，运行git branch -a 也不能看出这个branch被删除了，如何处理？

使用下面的代码查看b1的状态:

![](/assets/import-08-08-01.png)这时候能够看到b1是stale的，使用以看命令 ，可以将其从本地版本库中去除。

```
git remote prune origin
```

更简单的方法是使用这个命令，它在fetch之后删除掉没有与远程分支对应的本地分支：

```
git fetch -p
```

### 重命名远程分支

在git中重命名远程分支，其实就是先删除远程分支，然后重命名本地分支，再重新提交一个远程分支。例如下面的例子，我需要把devel分支重命名为develop分支：

**首先删除远程分支：**

```bash
$git branch --delete origin devel
```

**重命名本地分支:**

```bash
$git branch -m devel develop
```

**推送本地分支到远程仓库：**

```bash
$git push origin develop
```



