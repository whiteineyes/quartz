---
title: 用网盘方式在不同电脑同步Hexo
date: 2016-11-24 13:54:48
tags: [hexo]
thumbnail: http://whiteeyes.qiniudn.com/yunfuwu.jpg
---

如果我们有两台电脑，一台在家里，一台在办公室，想同时对Hexo进行更新怎么办？  

我在这里举一下例子，我在家里创建了Hexo，并且进行了部署，然后我想在办公室的电脑上也可以更新这个Hexo博客，那么可以试着安装我的做法来做一下。

<!--more-->  

条件：家里的电脑已经部署好，现在在办公室的电脑上部署Hexo，用网盘同步的方式来部署。

注意，我这里说的是网盘，不是同步盘，同步盘我会另外写一篇文章来说明，链接在末尾。

### 1 同步内容

hexo博客文件夹中的_config.yml，theme/，source/，scaffolds/，package.json，.gitignore这几个文件。
或者你上传整个Hexo文件夹到网盘上，但下载到本地时，只下载我上面说的这几个。

#### 注意！千万不要下载node_modules/这个文件夹！！！
### 里面套路太深，同步盘或云盘不支持路径名称大于256的文件！
#### 就算网盘支持，同步到本地时windows也不支持！！！
### 我就吃了这个亏，上了这个当！

### 2 安装git

### 3 部署SSH-keys

### 4 安装node.js

### 5 在办公室电脑上找个合适位置，新建一个hexo博客文件夹内，在这个文件夹内用git bash安装hexo

`npm install hexo-cli -g`

### 6 把你从网盘下载下来的hexo文件夹中的这几个文件拷贝到博客文件夹内

	_config.yml
	
	theme/
	
	source/
	
	scaffolds/
	
	package.json
	
	.gitignore

### 7 进行模块安装

`npm install`
`npm install hexo-deployer-git`
	    *（注意，不需要hexo init这条指令）*

### ８　安装你需要的插件（常用的几个）

（1）为了使用hexo d来部署到git上，需要安装
`npm install hexo-deployer-git --save`

（2）为了建立RSS订阅，需要安装
`npm install hexo-generator-feed --save`

（3）为了建立本地搜索，需要安装
`npm install hexo-generator-search --save`

### 9 进行你想要的操作，比如写文章
	
### 10 发布到git

`hexo clean`
`hexo g -d` 
到这里，我们就已经把跟家里电脑上的Hexo一模一样的Hexo部署好了。

### 8 日后使用

如果你在别的电脑上没有更新过Hexo,那么什么都不要管，直接写文章，然后
`hexo clean`
`hexo g -d` 
就好了

如果你在别的电脑上更新过Hexo,那么每次都要把我说的那几个文件覆盖到本地来，然后
`hexo clean`
`hexo g -d` 

### 9 弊端
每次切换电脑操作都得上传文件，然后又得下载文件，很麻烦。

### 10 其他方法

1使用同步盘的方法，可以避免手动上传下载。

2使用git push 到版本库，然后git clone , git pull 。



