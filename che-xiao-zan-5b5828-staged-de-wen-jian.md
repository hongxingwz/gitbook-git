# 撤销暂存\(staged\)的文件

## 情况一：新添加的文件取消暂存
(use "git rm --cached <file>..." to unstage)

```
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        src/

nothing added to commit but untracked files present (use "git add" to track)

```

**把未追踪的文件夹src/添加至暂存区**

```
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git add src/
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   src/.DS_Store
        new file:   src/main/.DS_Store
        new file:   src/main/java/com/jianglei/config/JiangLeiProperties.java
        ...

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .DS_Store
        .idea/
        README
        pom.xml
        simplegit.rb
        springjpatest01.iml

jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git add src/
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   src/.DS_Store
        new file:   src/main/.DS_Store
        new file:   src/main/java/com/jianglei/config/JiangLeiProperties.java
       ...
```

**移除新添加至暂存区的src/目录**

```
jiangxuedeMacBook-Pro:springjpatest01 jianglei$ git rm --cached -r src/
rm 'src/.DS_Store'
rm 'src/main/.DS_Store'
rm 'src/main/java/com/jianglei/config/JiangLeiProperties.java'
```

## 撤销已经追踪修改的文件





