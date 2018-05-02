# 项目分支太多，克隆速度很慢怎么办

## 简介
随着项目越来越大，分支越来越多。克隆一个完整的代码库会变得很慢。而有的情况下，保需要克隆出一个分支的完整代码就可以了(比如在持续集成中)。

此问题困惑了我好久好久，今天终于找到了解决的办法

## 慢的原因
```
git clone  <url>
```
git会下载所有的分支下的所有提交历史

##解决办法


###只克隆一个分支
不是太旧版本的git的clone命令支持--single-branch参数，配合-b参数可以只获取单个分支

假如知道那个commit大概的深度，可以再加上--depth参数

**克隆仓库下management仓库下最近10个commit**

```
$ git clone --single-branch -b management --depth 10  http://jianglei@123.56.178.186:8080/r/video.git video-management
```

