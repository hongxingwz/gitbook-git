git log  --pretty=oneline 具体的文件，如：

```
git log --pretty=oneline src/main/java/com/yunlook/service/WechatMessageTaskBuildService.java
035f80ae491cb8139980cfe65333aabb43a88f52 replace CRLF to LF
5d9baac4fad59ab6f3a699f5eec51cf4904b950e web-3920 微信增加推送种类
c41c0c674e8473eeafe8fb427d43c5e0324238f4 bug 微信推送不出去信息bug comment
e5f882d2afd2526d05b164c923a8ce18fa5a2cf3 bug 微信推送不出消息
3f694e057c221d1fc6f9d304bd4fddf7aabe3051 微信消息推送优化
1e2085c4bd8a1a6801d914a726b5c5c856e9ac04 漏提
14cae28d364c26a5146e81d3dd1dd124ea2271a9 漏提
c9781110e3146a52e23ff35f6ec80b90b4c3c5c5 微信推送-非空较难，bug修复
8a4211b2235ecd02fc30ded13c958fa0c535ec95 微信推送
```

然后,显示此次提交与上一次的不同

```
git show c41c0c674e8473eeafe8fb427d43c5e0324238f4
```



