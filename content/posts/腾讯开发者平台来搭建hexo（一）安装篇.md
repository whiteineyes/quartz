---
title: 腾讯开发者平台来搭建hexo（一）安装篇
date: 2018-10-28 14:50:31
tags:
thumbnail:
layout:
---
   
coding和腾讯云合作以后，推出的Cloud Studio真是很好用啊。  
好用之处就是，不用固定电脑了，直接浏览器打开Cloud Studio就能写博客，真的很方便！  
经过摸索，现在给大家来简单说一下在Cloud Studio下怎么安装和使用Hexo。  
***
<!--more--> 
  
# 1. 新建项目及分支
腾讯云开发者平台网址：`https://dev.tencent.com/user/`  
创建腾讯开发者账号后，右上角新建项目。  

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/1.png)  

填入项目名字、描述、启用README.md后，点击新建项目

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/2.png)  


新建分支，左侧分支管理，

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/3.png)  


右侧新建分支

填入分支名，coding-pages

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/4.png)  
  
![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/5.png) 


# 2. Cloud Studio部署  
## 2.1 配置环境
左侧，代码，代码浏览
![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/6.png)  

 


使用Cloud Studio编辑
![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/7.png)


右侧 运行环境 添加环境 选择Hexo 然后切换环境

  


![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/8.png)  


![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/9.png)  

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/10.png) 



## 2.2 配置hexo
然后我们开始配置hexo

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/11.png)  


 




在终端输入`hexo init 名字`名字就是你想给自己的博客工作区起的名字，我的是用`blog`  注意点

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/12.png)  


然后开始等待，大概4-5分钟，耐心

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/13.png)  


出现`Start blogging with Hexo!` 就是可以了

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/14.png)  


然后输入`cd blog` 进入到我们创建的文件夹，你们要改成自己的，也就是上面注意点1我们所说的名字

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/15.png)  



然后输入你的注册信息
```
git config --global user.email "你的邮箱"
git config --global user.name "你的用户名"
```
![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/16.png)  


输入 
`npm install hexo-deployer-git --save`

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/17.png)  

## 2.3 生成hexo博客

输入 `hexo g`来生成静态网页

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/18.png)  


输入`hexo s` 来生成预览网页

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/19.png)  

 

右侧 访问链接 把里面的端口号改成4000，然后创建链接

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/20.png)  


然后点击0.0.0.0:4000，就可以看到我们生成的hexo博客了

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/21.png)  

## 2.4 部署hexo静态网页
然后我们将hexo博客生成的静态网页部署到coding上去
先在终端按 Ctrl+C 来停止预览

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/22.png)  

然后我们设置一下部署的配置，先回到我们的coding网站或者腾讯云开发者平台


左侧，Pages服务

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/23.png)  

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/24.png)  


点击一键开启Coding Pages

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/25.png)  


将访问地址复制下来

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/26.png)  


回到Cloud Studio中，在左侧文件树中，双击_config.yml，在左侧的编辑区域，将url改成你刚刚复制的，root: 改成注意点1中你起的名字

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/27.png)  



然后回到Cloud Studio中，右侧，点击HTTPS旁的下拉按钮，更换为SSH

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/28.png)  


然后右侧复制` git@*** `的地址

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/29.png)  

回到Cloud Studio中，在左侧文件树中，双击_config.yml，拉到最后


按照截图填入信息，其中`gits@***.git `改成你自己刚刚复制的SSH地址，最后加上"coding-pages"
```
deploy:
  type: git
  repo:
    coding: git@git.dev.tencent.com:lqwhig/lwc.git,coding-pages
```
![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/30.png)  


然后在终端里输入`hexo clean`

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/31.png)  



`hexo g`

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/32.png)  



`hexo d`

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/33.png)  



回到腾讯开发者平台，点击Pages服务，然后右侧设置

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/34.png)  



在代码分支处，点下拉按钮，选择coding-pages

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/35.png)  


然后点部署

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/36.png)  


再点击访问地址

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/37.png)  


我们的hexo博客就搭建好了

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/38.png)  


## 2.5 写博文及再次生成部署
写文章的话，就回到我们的Cloud Studio  
输入`hexo new 文章名`

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/39.png)  


然后去左侧，路径为/blog/source/_posts/，双击.md文件，就会加载出来，在这里编辑好你要写的内容，格式为markdown

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/40.png)  



写好文章以后，在下面终端`hexo clean`、`hexo g`、`hexo d`，然后就可以看到网站更新了

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/41.png)  



# 3. 绑定域名
有自己域名的小伙伴，可以在DNS里，添加一条CNAME到访问地址`用户名.coding.me`，不用后面的`/blog`

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/42.png)  


然后去开发者平台Pages服务里，绑定新域名

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/43.png)  


再去Cloud Studio里面_config.yml里修改`url:`为你要绑定的域名地址，`root：`去掉后面的blog

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/44.png)  


惯例在下面终端`hexo clean`、`hexo g`、`hexo d`

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/45.png)  



# 4. 备份

到上面就可以了，但是为了保险，还是将hexo的主程序备份一下，将hexo推送到项目master分支
```
git add .
git commit -m "内容"
```
![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/46.png)  


`git push`

![Alt text](https://pic-1252861294.cos.ap-beijing.myqcloud.com/Cloud%20stuio%20hexo/install/47.png)  

***
# 5. 结尾
基本上就是这样了，除去修改主题或者插件，我们要进行的操作也就是  
写文章`hexo new 文章名`  
清楚老旧页面`hexo clean`  
生成静态页面`hexo g`  
部署到coding pages`hexo d`  
换电脑也一样，登陆Cloud Studio，就可以直接对博客进行更新维护了。  