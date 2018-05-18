# diff

相关链接：[https://blog.csdn.net/shirley\_john\_thomas/article/details/52548731](https://blog.csdn.net/shirley_john_thomas/article/details/52548731)

## 提交

**查看两次提交间的差异**

```
git diff 16fa736 5705593
```

**查看两次提交间的差异统计\(概况\)**

```
git diff 16fa736 5705593 --stat
```

## 文件

**查看指定文件某个版本与现在的差异**

```
git diff 16fa736 -- src/main/webapp/WEB-INF/jsp/manage/userAll.jsp
```

查看两个版本之间指定文件的差异

```
 git diff 16fa736 5705593 -- src/main/webapp/WEB-INF/jsp/manage/userAll.jsp
```



