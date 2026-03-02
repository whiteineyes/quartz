---
title: 用git方式在不同电脑同步Hexo
date: 2017-10-03 15:29:19
tags: [git,hexo]
thumbnail: http://whiteeyes.qiniudn.com/typing.gif
---

***
推荐一个我自己用的方式，可以自由的在各个电脑之间更新博客，不用携带U盘或者使用网盘，只要有git就可以了。
不要太依赖本文中的代码，因为随着Hexo版本的更新，有些代码或者插件会失效，所以请把注意力放在流程上。
***
<!--more-->  
你需要弄明白在Hexo中，`hexo d`也就是`hexo deploy`所代表的意思.
`hexo d`这个命令会对我们利用`hexo g`生成的静态网页进行部署，而不是整个Hexo，所以我们可以利用git的分支来做文章：

|分支          ||用途     |命令 |设置位置|
|:------------:|--|:------:|:------:|:---:|
|[master分支]    ||   存放整个Hexo的文件  | `git push`|   .git文件夹中config|
|[gh-pages分支]  ||   部署所生成的静态网页 | `hexo d`|  _config.yml|


那么我们可以在使用完Hexo后，也就是将静态网页部署后`hexo d`，对整个Hexo仓库进行版本上传`git push`,那么所有的文件就都上传到git的远程仓库了，然后如果你换了另外一台电脑来更新博客，只要在新电脑上`git pull`将远程仓库更新到本地来就可以了。

接下来说说详细的步骤,假设有A和B两台电脑。
***

### 电脑A：

#### 安装Hexo
请参照[Hexo博客安装教程](/2016/11/23/hexo-install/)。

#### 对Hexo进行版本上传
在`hexo d`后，我们将本地的hexo博客文件整个Push到远程仓库。
`git add .`
`git commit -m "写你想写的"`
`git push`或者`git push master`
这个部分是将整个Hexo博客的文件上传到远程仓库的master分支。




#### 不更换电脑更新博客
如果你没有更换电脑，而是继续在A电脑上更新博客，那么在你`hexo d`之后，仍旧对其进行版本上传好了，或者你可以在最后一次博客更新后进行版本上传。



### 电脑B：
重点的来了，B电脑是一台新电脑，想要使用并更新Hexo博客，那么需要以下步骤：

#### git clone
对远程仓库中的Hexo博客进行`git clone`，不需要像电脑A一样另外新建一个Hexo项目。
但是clone下来的文件是无法直接进行博客更新操作的，因为没有Hexo来驱动，所以我们需要先安装Hexo。

#### 进入Blog文件夹安装hexo

`npm install hexo-cli -g`


#### 进行模块安装

`npm install`
	    *（注意，不需要hexo init这条指令）*

#### 安装插件（根据需求来，第一个必装，其余的你可以有选择性地安装）

（1）为了使用hexo d来部署到git上，需要安装
`npm install hexo-deployer-git --save`

（2）为了建立RSS订阅，需要安装
`npm install hexo-generator-feed --save`

（3）为了建立本地搜索，需要安装
`npm install hexo-generator-search --save`

（3）为了建立谷歌sitemap，需要安装
`npm install hexo-generator-sitemap --save`

（3）为了建立百度sitemap，需要安装
`npm install hexo-generator-baidu-sitemap --save`

上述步骤完了以后，那么恭喜你，B电脑已全部设置完成，可以用来更新博客了。

#### 更新博客
进行你想要的操作，比如写一篇新的文章，然后：
`hexo clean`
`hexo g` `hexo d`或者`hexo g -d`
这样你就把新生成的静态网页部署到远程仓库的gh-pages分支上了。

#### 对Hexo进行版本上传
`git add .`
`git commit -m "写你想写的"`
`git push`或者`git push master`
那么这样我们就再次将整个Hexo博客的文件Push到远程仓库的master分支了。

***
***

### 不同电脑之间电脑更新Hexo

#### 如果在别的电脑上没有更新过Hexo：

直接写文章

再更新博客：
`hexo clean`
`hexo g -d`

然后把Hexo文件push到远程仓库：
`git add .`
`git commit -m ""`
`git push`或者`git push master`

#### 如果在别的电脑上更新过Hexo：

那么使用`git pull`，这个命令会将远程仓库的更改合并到本地来。

比如你在B电脑更新了博客，也push了Hexo文件到远程仓库，那么当你换到A电脑来操作的时候，先使用`git pull`将远程仓库里的文件合并到本地，之后你就可以进行博客的更新操作了，比如写文章。

然后生成静态网页并部署：
`hexo clean`
`hexo g -d`

最后push博客文件到远程仓库：
`git add .`
`git commit -m ""`
`git push`或者`git push master`
