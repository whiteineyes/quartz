---
title: Hexo博客安装教程 
date: 2016-11-23 15:17:43
tags: [git,hexo]
thumbnail: http://whiteeyes.qiniudn.com/git+hexo.png
---


### 用hexo来搭建blog


此文章需要一定的基础，但是步骤已经够详细了，等我哪天有时间，写个更加详细的步骤和说明。
<!--more-->  


#### ssh密匙，省略 

#### 新建项目，省略 

#### hexo本地部署 

        在本地创建hexo的文件夹内，右键-git bash
        
    	npm install -g hexo 
    	#此命令将会在本地安装hexo(视网速和电脑配置情况，一分钟到三分钟不等,后面操作仍旧可能存在需要等待的地方，请大家自己耐心点）

![npm install -g hexo](http://whiteeyes.qiniudn.com/hexo-npminstall-ghexo.png)
    	
        hexo init 
    	#此命令hexo会在本地创建自身需要的文件和文件夹
		
![hexo init](http://whiteeyes.qiniudn.com/hexoinit.png)
	
	    npm install
	    #此命令会在本地安装hexo所需要的依赖包
		
![npm install](http://whiteeyes.qiniudn.com/hexo-npminstall.png)

    	hexo g 
    	#此操作将会生成Hexo静态页面，这个页面将会上传，也就是你在浏览器里将要看到的网页样子，用来展示你的Hexo网站。
		
![hexo g](http://whiteeyes.qiniudn.com/hexog.png)

    	hexo s
    	#此命令将会在你的本地4000端口部署Hexo网页演示，在本地部署是为了你能直接在本地查看，以确保页面生成没有问题。
		
![hexo s](http://whiteeyes.qiniudn.com/hexos.png)

	    然后在浏览器中查看http://localhost:4000/ ，这个时候你应该可以看到你的博客了
	
    	在git bash内按ctrl+c两个键停止演示

#### 如果你前面有过Hexo的博客，想把文章导入新创建的这个hexo，那就进行如下操作，如果没有，请跳过。

将你原来Hexo博客中的source文件夹替换到新建成的hexo的source文件夹
	
然后执行
				hexo g
                hexo s
		
查看http://localhost:4000/
看你的博客文章导过来没有
	
在git bash内按ctrl+c两个键停止演示


#### 修改_config.yml，这个文件中其他的我不介绍了，只介绍推送仓库的设置。

以我的举例，我是同时部署到github和coding两个上面的gh-pages，如果你只需要一个，那repo：后面就只填你需要的那个，以.git结尾的是你将部署的git地址，gh-pages是将要部署的分支，这两个都要记得修改成自己的。

        deploy:
	
        （前面一个tab）type: git

        （前面一个tab）repo: 

        （前面两个tab）github: git@github.com:whiteineyes/blog.git,gh-pages
	
        （前面两个tab）coding: git@git.coding.net:whiteeyes/blog.git,gh-pages
		
![config.yml](http://whiteeyes.qiniudn.com/hexo-config.png)

#### 部署

            git bash下输入
	   
	    	hexo g
		
	    	hexo d
		

#### 如果执行hexo d报错，错误显示为：

	    	ERROR deployer not found:git
		
	        那就先执行下面的命令，此命令只用执行一次，后面就不用执行了： 
	        npm install hexo-deployer-git --save
			
![npm install hexo-deployer-git](http://whiteeyes.qiniudn.com/hexo-npminstallhexo-deployer.png)
	        再执行 hexo d
	

### 完成
这样子你去上网页，应该能看到了。

#### 如果你需要一个readme.md，那把这个readme.md这个文件放在source文件夹下，然后修改全局config里面的skip-render: README.md 
#### github用来展示网站是会自动展示在这个地址：用户名.github.io/仓库名 ，如果你的仓库名直接就是： 用户名.github.io ，那么网站就会在这里展示。
![skip-render](http://whiteeyes.qiniudn.com/hexo-skiprender.png)