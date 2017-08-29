# 配置文件git config介绍

git有一个工具被称为git confi,它允许你获得和设置配置变量：这些变量可以控制git的外观和操作的各个方面。

## 配置文件的存储位置

这些变量可以被存储在三个不同的位置：

1. /etc/gticonfig文件：包含了适用于系统所有用户和所库的值。如果你传递参数选项"--system"给git config，它将明确的读和写这个文件
2. ~/.gitconfig文件：具体到你的用户。你可通过传递--global选项使Git读或写这个特定的文件。
3. 位于git目录的config文件\(也就是.git/config\)：无论你当前在用的库是什么，特定指定该单一的库。

每个级别重写前一个级别的值。因此在.git/config中的值覆盖了在/etc/gitconfig中的同一个值。



## 配置你的用户名和邮箱

当你安装Git后首先要做的事情是设置你用户名称和e-mail地址。这是非常重要的，因为每次Git提交都会使用该信息。它被永远的嵌入到了你的提交中：

```
$ git config --global user.name "dengyi"
$ git config --global user.email "745400440@qq.com"
```

## 配置你的编辑器

你的标识已经设置，你可以配置你的缺省文件编辑器，Git在需要你输入一些消息时会使用该文件编辑器。缺少情况下，Git使用你的系统的缺省编译器，这通常可能是vi或者vim。如果你想使用一个不同的文件编译器，例如Emace,你可以做如下操作：

```
$ git config --global core.editor emacs
```

## 配置你的比较工具

另外一个你可能需要配置的有用的选项是缺少的比较工具它用来解决合并时的冲突。例如，你想使用vimdiff:

```
$ git config --global merge.too vimdiff
```



## 检查你的配置

如果你想检查你的设置，你可以使用git config --list 命令来列出Git可以在该处找到的所有的位置：

```
$ git config --list
  user.name=dengyi
  user.email=745300440@qq.com
```

你可能会看到一个关键字出现了多次，这是因为Git从不同的文件\(例如:/etc/gitconfig以及~/.gitconfig\)读取相同的关键字。在这种情况下，对每个唯一的关键字，Git使用最后的那个值。

你可以查看Git认为的一个特定的关键字目前的值，使用如下命令git config {key}:

```
$ git config user.name
dengyi
```



## 获取帮助

如果当你在使用Git时需要帮助，有三种方法可以获得任何git命令的手册面{manpage}帮助信息

```
$ git help <verb>
$ git <verb> --help
$ man git -<verb>
```

例如，你可运行如下命令获取对config命令的手册帮助：

```
$ git help config
```



