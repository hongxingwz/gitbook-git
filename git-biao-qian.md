# Git标签

内容提要： 创建有签名，无签名，轻量级标签来永久的标记项目历史中的关键点

跟大多数的VCS工具一样，git也有在历史状态的关键点“贴标签”的功能 -- 一般人们用这个功能来标记发布点\(例如'v1.0'\)。这节课我们学习如何使用标签列表，创建新标签，以及在git中有哪些不同类型的标签。

## 列出git有现有的标签

要想列出git中现有的所有标签，输入'git tag'命令运行即可：

```
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git tag
v1.6.0
v1.7.0

```

这个列表是按照字母表顺序给出的，其实排名先后跟重要程序没有直接联系。

当然，你可以按照特定表达式搜索某些标签。假如在一个git仓库中有超过240个标签，而你只想得到1.6序列的标签，那么你可以：

```
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git tag -l v1.6*
v1.6.0

```

## 创建标签

在git中有两种最主要的标签

* 轻量级标签\(lightweight\)
* 带有注释的标签\(annotated\)

轻量级标签跟分支一样，不会改变，这就是针对某个特定提交的指针。

然而，带注释的标签是git仓库中的对象，它是一组校验和，包含标签名，email, 日期，标签信息，GPG签名和验证。

一般情况下，建议创建带注释的标签，这样就会保留这些信息，但是如果你只是需要临时性标签或某些原因你不想在标签中除带上面说的这些信息，lightweight更合适些。

### 带注释的标签

在git中创建带注释的标签非常简单，在运行'tag'命令时加上-a就可以了。

```
$git tag -a v1.8 -m "version 1.8"
$ git tag
v1.6.0
v1.7.0
v1.8

```

"-m"指明标签信息，跟标签一起存储。如果你不使用-m指明标签信息，git会自动启动文本编辑器让你输入。可以使用git show命令查看相应标签版本信息，并连同显示打标签时的提交对象。

```
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git show v1.8
tag v1.8
Tagger: jianglei <745300440@qq.com>
Date:   Wed Aug 30 09:43:27 2017 +0800

version v1.8

commit 14fc4c1f8a1a3992affdda9aa98b2ed57fb026de
Merge: e9f7b27 3742668
Author: jianglei <745300440@qq.com>
Date:   Wed Aug 30 09:23:33 2017 +0800

    Merge branch 'dev'


```

我们可以看到，在提交对象信息上面，列出了此标签的提交者和提交时间，以及相应的标签信息。

```
[master]$ git tag -s v1.5 -m 'my signed 1.5 tag'
You need a passphrase to unlock the secret key for
user: "Scott Chacon <schacon@gmail.com>"
1024-bit DSA key, ID F721C45A, created 2009-02-09
```

然后，如果你对某个标签运行’git show‘的话，你就会看到你的GPG前面附加上去了。

```
[master]$ git show v1.5
tag v1.5
Tagger: Scott Chacon <schacon@gmail.com>
Date:   Mon Feb 9 15:22:20 2009 -0800
my signed 1.5 tag
-----BEGIN PGP SIGNATURE-----
Version: GnuPG v1.4.8 (Darwin)
iEYEABECAAYFAkmQurIACgkQON3DxfchxFr5cACeIMN+ZxLKggJQf0QYiQBwgySN
Ki0An2JeAVUCAiJ7Ox6ZEtK+NvZAj82/
=WryJ
-----END PGP SIGNATURE-----
commit 15027957951b64cf874c3557a0f3547bd83b3ff6
Merge: 4a447f7... a6b4c97...
Author: Scott Chacon <schacon@gmail.com>
Date:   Sun Feb 8 19:02:46 2009 -0800
    Merge branch 'experiment'
```

### 带有轻量级的标签

轻量级标签实际上就是存在一个文件中的提交校验和-- 没有附加任何其他信息。创建轻量级标签的方法就是把上面’-a‘, '-s', '-m'这些选项都去掉。

```
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git tag v1.8.9
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git tag
v1.6.0
v1.7.0
v1.8
v1.8.9
```

如果现在对这个标签使用"git show"命令，不会看到像上面那种标签显示的那么多内容，仅仅显示这次提交的有关信息

```
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git show v1.8.9
commit 14fc4c1f8a1a3992affdda9aa98b2ed57fb026de
Merge: e9f7b27 3742668
Author: jianglei <745300440@qq.com>
Date:   Wed Aug 30 09:23:33 2017 +0800

    Merge branch 'dev'

jiangxuedeMacBook-Pro:springjpatest01 jianglei$ 

```

### 后期贴标签

这种情况是说想对以前的某次提交贴个标签，如果整个提交历史是这样的：

```
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git log --pretty=oneline 
14fc4c1f8a1a3992affdda9aa98b2ed57fb026de Merge branch 'dev'
37426682a73a784383b56a95b3ce035faf27276b dev second comit
e9f7b2792d0f15295d4602faedb898906fd70ba5 hei hei hei
cb2d8bd76f0caacb420aaeaab9fc3b281ebfdd72 conflict
cf8b44eee7cc3222bacedec21d7354aed4ebdee9 master change the dev
8831aceb745b8b483a8b10140d60d376bc1e2dad change the dev
d4b0757a8e414f3791d2169f7b604a75616b7fae simplegit
d9c34dcddf6b71d1d4e3391ea9e2dcf638b477a2 add author's wife
08620ae813382e26b6489e86866969bfeb536a3c modify the file README
d89360c0ab13abd612e335b84bbd88be739b4962 second commit
ac1bc4be5db217ed6b6fbe64a704595fa134450a first commit

```

忘记在那个提交信息为"first commit"的点贴上一个'v0.0.1'的标签了，我可以现在贴一个上去。你可以在执行创建标签的语句后面跟上那次提交的校验和\(或者部分校验\)

```
$ git tag v0.0.1 ac1bc4be5db217ed6b6fbe64a704595fa134450a
```

现在我们可以列出所有标签

```
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git tag
v0.0.1
v1.6.0
v1.7.0
v1.8
v1.8.9

```

### 共享标签

默认情况下，‘git push’命令不会将标签上传到远程服务器。为了共享这些标签。为了共享这些标签，你必须在'git push‘命令后明确添加--tags选项

```
git push --tags
```

现在，如果有人克隆或者在线同步你的git仓库的话，标签也会一并同步了。

