# git 获取远程分支

git获取别人刚提交到服务器上的远程分支

```
git fetch origin 远程分支名x: 本地分支名x
```

使用该方式会在本地新建分支x,但是不会自动切换到该本地分支x，需要手动checkout

```
video-management git:(management-monitor) ✗ git fetch origin management-check
➜  video-management git:(management-monitor) ✗ git branch -r
  origin/HEAD -> origin/master
  origin/data-support
  origin/fileupload
  origin/management
  origin/management-check
  origin/management-monitor
  origin/master
  origin/master-es
  origin/research
  origin/wechat
  origin/yingla

```

如上图已经把远程分支拉取到本地

