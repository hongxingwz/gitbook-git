# 研发团队GIT开发流程新人学习指南

## 前言

本文定位于为使用GIT标准分支开发流程的开发团队新人提供一份参考指南，其中的内容都是我们公司在研发团队初创时所遵循的一些开发流程标准，经过近一年的实践，虽说还有很多不足，但是随着团队经验的丰富和人员的扩张，我会适时地更新本文，分享我们在使用GIT开发流程中遇到的问题和解决方案。

## 分支流程说明

### 简介

![](/assets/1520839114393.png)

项目中长期存在的两个分支

* master: 主分支，负责记录上线版本的迭代，该分支代码与线上代码是完全一致的。
* develop: 开发分支，该分支记录相对稳定的版本，所有的feature分支和bugfix分支都从该分支创建。

其它分支为短期分支，其完成功能开发之后需要删除

* feature/\*：特性（功能）分支，用于开发新的功能，不同的功能创建不同的功能分支，功能分支开发守成并自测通过之后，需要合并到**develop**分支，之后删除该分支。
* bugfix/\*：bug修复分支，用于修复不紧急的bug，普通bug均需要创建bugfix分支，开发完成自测没问题后合并到**develop**分支后，删除该分支。
* release/\*：发布分支，用于代码上线准备，该分支从develop分支创建，创建之后由测试同学发布到测试环境进行测试，测试过程中发现bug需要开发人员在该release分支上进行bug修复，所有bug修复完后，在上线之前，需要合并该release分支到**master**分支和**develop**分支。
* hotfix/\*：紧急bug修复分支，该分支只有在紧急情况下使用，从**master**分支创建，用于紧急修复线上bug，修复完成后，需要合并该分支到**master**分支以便上线，同时需要再合并到**develop**分支。

## 分支命名规范

### 特性（功能）分支
功能分支的分支名称应该为能够准确描述该功能的英文简要表述


```
feature/分支名称
```
例如，开发的功能为 新增商品到物料库，则可以创建名称为 feature/material-add的分支。

### bug修复分支、紧急bug修复分支
bug修复分支的分支名称可以为Jira中bug代码或者是描述该bug的英文简称


```
bugfix/分支名称
hotfix/分支名称
```
比如，修复的bug在jira中代号为**MATERIAL-1**，则可以创建一个名为bugfix/MATERIAL-1的分支。

**release分支**
release分支为预发布分支，命名为本次发布的主要功能英文简称


```
release/分支名称
```
比如，本次上线物料库新增的功能，则分支名称可以为release/material-add。

## 常用操作使用简介

### 基本操作
基本命令这里就不多说了，基本跟以前一样，唯一的区别是注意分支是从哪里拉取的以及分支的命名规范。涉及到的命令主要包含以下，大家自己学习：


* git commit 
* git add [-all]
* git push 
* git pull
* git branch [-d]
* git merge
* git cherry-pick
* git checkout [-b] BRANCH_NAME
* git stash


## 总结
如果上面内容太多记不信，也没有关系，作为开发人员，刚开始的时候只要知道以下几点就足够了，其它的可以在碰到的时候再深入学习：
* 所有的新功能开发，bug修复（非紧急）都要人develop分支拉取新的分支进行开发，开发完成自测没有问题再合并到develop分支

* release分支发两点到测试环境，则开发人员创建release分支（需要测试人员提出需要）并发布到测试环境，如果测试过程中发现bug，需要开发人员track到该release分支修复bug，上线前需要测试人员提交merge request到master分支，准备上线，同时需要合并回develop分支

* 只有紧急情况下才允许从master上摘取hotfix分支，hotfix分支需要最终同时合并到develop和master分支（共两次merge操作）

* 除了master和develop分支，其它分支在开发完成后都要删除












