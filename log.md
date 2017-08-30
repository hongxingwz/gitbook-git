### 显示补丁

`git log -p`

### 统计字数

`git log --stat`

### 调整显示格式

使用"git log --pretty=format"命令，可以将提交历史显示成你想要的格式。这里format的可选项包括

* oneline
* short
* medium
* full
* fuller
* email
* raw

### 分支拓扑图

`git log --graph`

### 提交查询过滤器

git log 命令后如果跟--before 和 --after选项，就会显示两个日期之间的提交条目。日期格式也有不同的可选格式。例如，我想看1月26号之后，2个星期之前的提交内容，可以运行：

```
$ git log --before="2 weeks age" --after="2009-01-26" --pretty=oneline
```

#### 贡献者过滤器

git还可以通过贡献者过滤器来查看某个作者发起的提交。在commit对象中实际上存在两个人的记录

* 一个是作者\(author\)，也就是原始提交的人。
* 第二个人名是提交者\(committer\),就是提交到仓库中的人。

在这里找不到合适的翻译，所以把二者统称为贡献者。一般情况下，所指的都是同一个，但是某些情况就不是了。譬如，有一个作者将他写的东西emial给项目持有人，这个项目持有人就是提交者\(committer\),项目持有人将作者提交的东西提交到git仓库中。

大多数情况下搜索的是作者，当然你可以通过--author或者--committer加名字的方式来搜索相应的提交条目。下面这个例子我们是执行命令来查找作者名\(author\)为jianglei的提交记录

```bash
$ git log --author=jianglei
```

你可以指定完整人名或email地址来搜索，你也可以使用这些值的部分内容来查询，譬如，搜索jianglei作者的提交内容，可以执行下面的任意一条语句

```bash
$ git log --author=jianglei
$ git log --author=745300440@qq.com
```

#### 查找提交信息

如果你对“提交信息”更感兴趣，你可以通过提交信息里面的某个字符串来查找相应的提交。例如，下面是搜索在提交信息中含有’c90‘的

```bash
$ git log --grep='c90'
```

#### 文件或目录的历史

**文件历史**

```bash
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git log --pretty=oneline -- README
e9f7b2792d0f15295d4602faedb898906fd70ba5 hei hei hei
cb2d8bd76f0caacb420aaeaab9fc3b281ebfdd72 conflict
cf8b44eee7cc3222bacedec21d7354aed4ebdee9 master change the dev
8831aceb745b8b483a8b10140d60d376bc1e2dad change the dev
d9c34dcddf6b71d1d4e3391ea9e2dcf638b477a2 add author's wife
08620ae813382e26b6489e86866969bfeb536a3c modify the file README
d89360c0ab13abd612e335b84bbd88be739b4962 second commit
```

**目录历史**

```bash
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git log --pretty=oneline -- src/
ac1bc4be5db217ed6b6fbe64a704595fa134450a first commit
```

**文件历史和目录历史综合查询**

```bash
$ git log --pretty=online -- README src/
```

#### 其他选项

很多时候想查看未合并的提交历史记录，所以你可以加上"--no-merges"选项

```bash
$ git log --pretty=oneline --no-merges
```

还可以在查看日志命令最后加上-N来查看满足条件的最近的N条历史记录：

```bash
$ git log --pretty=oneline -5
14fc4c1f8a1a3992affdda9aa98b2ed57fb026de Merge branch 'dev'
37426682a73a784383b56a95b3ce035faf27276b dev second comit
e9f7b2792d0f15295d4602faedb898906fd70ba5 hei hei hei
cb2d8bd76f0caacb420aaeaab9fc3b281ebfdd72 conflict
cf8b44eee7cc3222bacedec21d7354aed4ebdee9 master change the dev
```

如果我们只希望看到提交信息为"dev second comit"之前“conflict”之后的提交记录

```bash
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git log --pretty=oneline 37426682a73a784383b56a95b3ce035faf27276b...cb2d8bd76f0caacb420aaeaab9fc3b281ebfdd72
37426682a73a784383b56a95b3ce035faf27276b dev second comit
cb2d8bd76f0caacb420aaeaab9fc3b281ebfdd72 conflict
cf8b44eee7cc3222bacedec21d7354aed4ebdee9 master change the dev
```

如果你在查找一个分支上的提交时，这样做非常管用。譬如，你目前在’master‘分支上，并且想查看’dev‘分支上还没有合并的提交记录的话，可以这样

```bash
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git log master...dev2
commit 99635d6ce84f77157942f9e16a3be617f4a3cbe2
Author: jianglei <745300440@qq.com>
Date:   Wed Aug 30 10:59:32 2017 +0800

    u2

commit d0d5a740a548d3e81d71b31f24d3ed8eb15146d5
Author: jianglei <745300440@qq.com>
Date:   Wed Aug 30 10:58:06 2017 +0800

    u
```

这就告诉你，如果现在合并的话，那么所列出的这些提交都被合并。你可以不写某一端的分支名，git会决断你目前正在哪个分支上，所以，如果你在master分支上的话，下面的命令执行结果和上面的一样：

```bash
$ git log ..dev2 --pretty=oneline
```

如果你在dev2分支上，也想看到相同的信息，即还没有合并到master的提交，可以运行：

```bash
$ git log master.. --pretty=oneline
```



