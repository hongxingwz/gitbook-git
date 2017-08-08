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



