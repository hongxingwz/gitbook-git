# 检出本地仓库中origin/master这样的分支



## 有时候我们要检出下图中名为remotes/origin/master的分支并命名为master

![](/assets/1515739320598.png)



```
git branch master origin/master
```

那检出并切换呢？

```
git checkout -b master origin/master
```



