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

使用下面的代码查看b1的状态





