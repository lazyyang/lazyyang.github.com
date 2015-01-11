---
layout: post
title: "在Octopress上搭建一个github博客"
date: 2014-05-24 00:06:41 +0800
comments: true
categories: 
---

##安装
----
1. 首先我们得先配置ruby、git环境，这里就不讲了。
2. 先cd到一个好的目录，比如Desktop,然后开始下载Octopress  
`$ git clone https://github.com/imathis/octopress.git`  
`$ cd octopress`
3. 安装一些东西  
`$ gem install bundler`  
`$ rbenv rehash`  
`$ bundle install`  

这样就装好Octopress了，我们可以`rake preview`在本地查看，如果`rake preview`报错的话，如下，
> You have already activated rake 10.1.1, but your Gemfile requires rake 0.9.2.2. Prepending `bundle exec` to your command may solve this. 

可能是因为你的rake版本过高，这时候就需要你在`rake preview`的前面加上`bundle exec`
<!--more-->

##发布
---
1. 在github上创建一个名为`username.github.com`的repository
2. 在Octopress目录里设定资料  
`$ rake setup_github_pages`
3. 生成HTML  
`$ rake generate`
4. 发布  
`$rake deploy`

**这样等几分钟，你就可以在你的网页,例如<http://lazyyang.github.com>上浏览你的博客了**

##配置博客
---
**我们需要在github上另外创建一个source分支，这个分支专门用来博客相关属性、写博客以及主题等**
###配置博客相关属性
* 配置博客，相关配置文件在_config.yml文件里
`$ vi  _config.yml`  
![](https://raw.githubusercontent.com/lazyyang/lazyyang.github.com/source/source/images/img/octopress_1.png)
**其中url是必填项，为你的博客地址**

###写博客
* 写博客  
`$ cd source`  
`$ cd _posts`  
`$ rake new_post["博客名字"]`  
**这样就创建了一个名为markdown的文件，然后在markdown里面写博客了**  
* 同步github  
`$ git add .`  
`$ git commit -m "a new blog"`  
`$ git pull orgin source`   
`$ git push origin source`  
* 发布文章  
`$ rake generate`  
`$ rake deploy`  
**这样文章就成功同步到blog上去了**

#:##多台电脑管理博客
---
**目前github上已经部署了我们的博客了，现在需要在另外一台电脑上继续写博客，该怎么处理**   
**Octopress的git仓库(repository)有两个分支，分别是`master`和`source`。`master`存储的事博客网站本身,而`source`存储的是生成博客的源文件。`master`的内容放在根目录的`_deploy`**

* 将source分支clone到本地  
`$ git clone -b source git@github.com:username/username.github.com.git octopress`

* 然后将master的clone到octopress的_deploy文件夹内  
`$ cd octopress`      
`$ git clone git@github.com:username/username.github.com.git  _deploy`  

* 然后安装博客，即bundler和需要的rubygem     
`$ gem install bundler`   
`$ rbenv rehash`    
`$ bundle install`     
`$ rake setup_github_pages`        

