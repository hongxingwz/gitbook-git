# Git自动换行符

## 回车和换行

回车\(Carriage Return\)和换行\(Line Feed\)概念：

* 回车CR:将光标移到到当前行开头
* 换行LF:将光标"垂直"移动到下一行，并不改变光标水平位置

以上的概念中适用于打字机，现代计算机没用的时候主要使用的是_**回到行首**_和_**换行+加到行首的功能。**_看下面的例子：

1.在Windows下应用程序输出\n到文件，会被自动转换成\r\n



## 不同系统下的换行符：

* Windows/DOS系统：采用CR/LF表示下一行
* Unix/Linux系统：采用LF表示下一行
* Mac OS系统：采用CR表示下一行
* Mac OS X系统：采用LF表示下一行\(Mac OS X已经改成Unix/Linux一样使用LF\)

CR使用的符号是'\r',十进制ASCII代表是13，十六进制代码为ox0D;LF使用'\n'符号表示，ASCII代码是10,十六进制为0x0A。所以Windows平台上换行在文本文件中是使用0d 0a两个字节表示，而UNIX和苹果平台上换行则是使用0a或0d一个字节表示。

Unix/Linux/Mac系统下的文件在Windows里打开的话\(使用Windows自带记事本\)，会出现换行丢失，所有文件会变成一行，整个文件会乱成一团。Window系统下的文件在Unix/Linux/Mac里打开的话，在每行的结尾可能会多出一个^M符号。

目前大部分的编辑器和IDE都支持这几种换行符\(除了notepad\),但是跨平台协作项目源码到底保存为哪种风格的换行符呢？输出的文本需要保存为哪种风格的换行符呢?Git提供了一个解决方案--在跨平台协作场景时，会提供一个“换行符自动转换”的功能。

## Git CRLF

Git默认在提交时将Windows换行符\(CRLF\)转换为LF，在拉取时将UNIX换行符\(LF\)替换成CRLF。我们可以设置autocrlf和safecrlf来设置具体的操作

### autocrlf and saftcrlf

1.autocrlf

```
// 提交时转换为LF，检出时转换为CRLF
git config --global core.autocrlf true

//提交时转换为LF，检出时不转换
git config --global core.autocrlf input

//提交检出是均不转换
git config --global core.autocrlf fase
```

2.safecrlf

```
//拒绝提交包含混合换行符的文件 
git config --global core.safecrlf true

//允许提交包含混合换行符的文件
git config --global core.safecrlf false

//提交包含混合换行符的文件时给出警告
git config --global core.safecrlf warn
```

### .gitattributes

.gitattributes文件能够设置每个仓库的换行符配置，摘取Link中的设置为例：

```
###############################################################################
# Set default behavior to automatically normalize line endings.
###############################################################################
* text=auto

###############################################################################
# Set the merge driver for project and solution files
#
# Merging from the command prompt will add diff markers to the files if there
# are conflicts (Merging from VS is not affected by the settings below, in VS
# the diff markers are never inserted). Diff markers may cause the following 
# file extensions to fail to load in VS. An alternative would be to treat
# these files as binary and thus will always conflict and require user
# intervention with every merge. To do so, just uncomment the entries below
###############################################################################
#*.sln       merge=binary
#*.vcxproj   merge=binary

###############################################################################
# behavior for image files
#
# image files are treated as binary by default.
###############################################################################
#*.jpg   binary
#*.png   binary
#*.gif   binary

###############################################################################
# diff behavior for common document formats
# 
# Convert binary document formats to text before diffing them. This feature
# is only available from the command line. Turn it on by uncommenting the 
# entries below.
###############################################################################
#*.doc   diff=astextplain
#*.DOC   diff=astextplain
#*.docx  diff=astextplain
#*.DOCX  diff=astextplain
#*.dot   diff=astextplain
#*.DOT   diff=astextplain
#*.pdf   diff=astextplain
#*.PDF   diff=astextplain
#*.rtf   diff=astextplain
#*.RTF   diff=astextplain

作者：小熊猜猜我有几颗糖
链接：http://www.jianshu.com/p/f13ef9e538e0
來源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

1. text=auto：采用git认为最好的方式来处理文件，未在.gitattributes中设置的项默认按照这种方式处理；
2. text eol=crlf/lf:在checkout时，转换Line Ending为crlf/lf;
3. binary：告诉git该文件为二进制，防止git修改该文件。

注意.gitattributes文件必须要提交之后才能生效。

> 注：由于目前Jenkins推送到打包服务器上的代码默认采用LF结尾，所以建议仓库内创建.gitattributes文件并设置。

## 项目实施一

### 设置原则

本地仓库完全一致，适合单一平台编程。

### 团队设置

一个团队需要使用使用同一的换行符标准\(UNIX标准或者Windows标准\)，然后配置自己的代码编辑器和IDE，达到两项要求：

* 在新建文件时默认使用团队统一的换行符标准
* 在打开文件时保持现有换行符格式不变\(不要做自动转换\)。

关闭换行符自动转换功能

```
//提交检出均不转换
git config --global core.autocrlf false
```

开启换行符检查功能\(按照需要设置\)

```
git config --global core.safecrlf true
git config --global core.safecrlf fase
git config --global core.safecrlf warn
```

### 留意每次提交

如果提交的时候变更行数过多\(超过自己修改\)，或者增减行数相同，很有可能是整个文件的换行符被修改了，这个时候就注意检查了。



## 项目实施二

---

### 设置原则

保证仓库永远换行符永远采用UNIX标准\(LF\)，在Windows工作空间设置为Windows标准\(CRLF\)，在Mac/Linux工作空间设置为Unix标准\(LF\)，适合跨平台编程。

### 团队设置

统一不同平台下的换行符标准，按照上面设置原则的标准，配置自己代码编辑器和IDE，达到两项要求：

* 在新建文件时默认使用团队统一的换行符标准
* 在打开文件时保持现有换行符格式不变\(不要做自动转换\)



1.设置换选符自动转换功能

```
#Configure Git on OS X or Linux to properly handle line endings
git config --global core.autocrlf input

#Configure Git on Windows to properly handle line endings
git config --global core.autocrlf true
```

2.设置换行符检查功能

```
#提交包含混合换行符的文件时给出警告
git config --global core.safecrlf warn
```

### 留意每次提交

1. 留意每次提交的更改行数。
2. 留意提交时的挑选符警告。



