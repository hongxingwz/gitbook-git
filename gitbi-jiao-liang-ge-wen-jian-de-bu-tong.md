# Git差异对比

在“git日志”一课中，我们能过"git log -p"命令来显示每一次提交与其父节点提交内容之间快照的差异。这节课介绍的'diff'命令会实现类似的功能--用一种统一的格式来显示两个快照或文件之间的差异。这节课就向你展示如何使用diff命令

## 查看变更还未载入\(changed but unstaged\)的文件对比

最常见的一种情况是使用git diff 查看工作目录中某个还未载入\(stage\)的文件差异。

实验方案:

* 修改一下simplegit.rb, 添加一个方法
* 然后在README文件中添加一个作者
* 然后我们用“git add”命令把README文件载入\(stage\)
* 运行‘git status’会显示README载入，而simplegit.rb只是修改了还未载入

```
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   README

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   simplegit.rb

```

那么，我现在想看一下对simplegit.rb文件究竟做了什么改动？在我载入之前怎么查看这些改动的内容呢?答案是只需要运行不带任何参数的'git diff‘命令即可

```
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git diff
diff --git a/simplegit.rb b/simplegit.rb
index e69de29..de54089 100644
--- a/simplegit.rb
+++ b/simplegit.rb
@@ -0,0 +1 @@
+add a new line.
\ No newline at end of file

```

这样就可以看到我们添加到文件中的内容，现在我可以决定是不是要将其载入了。注意，README文件的修改并没有显示出来。

## 查看载入\(stage\)而并未提交\(commit\)的变更

为了查看载入\(staged\)而并未提交\(not commit\)的内容差异，可以使用“git diff -stage”命令\(在git 1.6之前的版本中，使用'--cached'\)

```
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git diff --cached
diff --git a/README b/README
index e69de29..e9e055c 100644
--- a/README
+++ b/README
@@ -0,0 +1 @@
+author:jianglei
\ No newline at end of file
```

适应情形：在运行git commit\(不带’-a‘\)之前，查看所有载入而未提交的变更内容。

## 查看在最后一次提交之后的所有变更

现在，如果你想查看最后一次之后工作目录中文件的变更，你可以在git diff之后加一个HEAD来进行对比:

```
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git diff HEAD
diff --git a/README b/README
index e69de29..e9e055c 100644
--- a/README
+++ b/README
@@ -0,0 +1 @@
+author:jianglei
\ No newline at end of file
diff --git a/simplegit.rb b/simplegit.rb
index e69de29..de54089 100644
--- a/simplegit.rb
+++ b/simplegit.rb
@@ -0,0 +1 @@
+add a new line.
\ No newline at end of file

```

适用情境：在运行“git commit -a”之前。显示所有载入的和未载入的变更。

在本教程的"intermediate"一课中会详细讲述HEAD在git中的含义。在这里要注意的一点是，HEAD含义跟SVN中的HEAD含义大不相同，在git中HEAD与你目前所处分支的最后一次提交相关。与每个用户的本地仓库相关，在不同分支间切换时它也会发生改变。

上面是使用“diff”时最常用的三条命令。

## 从一个特定点开始文件的修改情况

这也是最常见的一个问题。譬如，如何查看创建v1.6这个标签之后README文件所发生的修改呢，可以这样：

```bash
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git diff v1.6.0 -- README
diff --git a/README b/README
index e69de29..896eabf 100644
--- a/README
+++ b/README
@@ -0,0 +1,2 @@
+author:jianglei
+author's wife:dengyi
\ No newline at end of file
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ 
```

## 两次提交的差异比对

```bash
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git diff v1.6.0 v1.7.0
diff --git a/README b/README
index e69de29..896eabf 100644
--- a/README
+++ b/README
@@ -0,0 +1,2 @@
+author:jianglei
+author's wife:dengyi
\ No newline at end of file
diff --git a/simplegit.rb b/simplegit.rb
index e69de29..de54089 100644
--- a/simplegit.rb
+++ b/simplegit.rb
@@ -0,0 +1 @@
+add a new line.
\ No newline at end of file

```

如果两个版本分别在两个目录中的话，直接运行Unix的’diff‘工具进行比对也可以。

上节课在介绍log命令时讲过格式化参数，譬如--stat,在这里也可以对git diff命令加这样的参数，显示某些统计数，下面是显示v1.6.0与v1.7.0两个版本之间的差异的统计数字：

```
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git diff v1.6.0 v1.7.0 --stat
 README       | 2 ++
 simplegit.rb | 1 +
 2 files changed, 3 insertions(+)

```

还可以深入查看某个具体文件的变更对比

```
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git diff v1.6.0 v1.7.0 -- README
diff --git a/README b/README
index e69de29..896eabf 100644
--- a/README
+++ b/README
@@ -0,0 +1,2 @@
+author:jianglei
+author's wife:dengyi
\ No newline at end of file

```

执行后会显示README文件在v1.6.0和v1.7.0两个版本之间的对比结果

## 在合并某分支前查看变更内容

这个是比较奇怪的问题，困为如果你开始是工作在一个主分支上，而后生成了两个分支，如果直接对比快照的话，结果只会显示从一个状态到另一个状态的差异对比结果。

举例来说，如果你创建了一个'dev'分支，进入这个分支给REAMDE添加了一行，然后回到了'master'分支，删除了README文件的一行，然后运行：

```
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git diff master dev
diff --git a/README b/README
index 48d8b1b..e1bd5e2 100644
--- a/README
+++ b/README
@@ -1,3 +1,3 @@
 author:jianglei
 author's wife:dengyi
-master he hei hei
\ No newline at end of file
+hei hei hei hei
\ No newline at end of file

```

如果你想查看的实际上是在创建dev分支之后在这条分支上的差异对比，所以应该执行这样的命令：

```
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git diff master...dev
diff --git a/README b/README
index 896eabf..e1bd5e2 100644
--- a/README
+++ b/README
@@ -1,2 +1,3 @@
 author:jianglei
-author's wife:dengyi
\ No newline at end of file
+author's wife:dengyi
+hei hei hei hei
\ No newline at end of file

```

这就不会拿master分支上最后一个快照和dev分支上最后一个快照进行比对

而是用dev与master所父的那个分支点和现在的dev分支上最后一个快照进行比对。

如果你目前正在master分支上，你可以运行：

```
$ git diff ...dev
```

如果你想查看合并的某个分支会有什么样的变化，可以执行

```
git diff ...<branch>
```

将branch替换为你想要合并的分支名即可

