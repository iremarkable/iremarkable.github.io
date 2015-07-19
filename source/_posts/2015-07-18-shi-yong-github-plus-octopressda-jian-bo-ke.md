---
layout: post
title: "使用Github+Octopress搭建博客"
date: 2015-07-18 16:58:03 +0800
comments: true
categories:  Github
---




##折腾一天半终于把Mac环境的Git+Octopress搭建好了，现在简要的说下在Mac上搭建步骤.

`提示：配置环境的时候，由于被强的原因，有的软件下载不下来，请使用VPN`




###(1) 环境配置

###1.1 安装Git 
安装Git很简单，下载完成后安装即可 [下载地址](http://git-scm.com/)

### 1.2 安装Ruby 
 
 安装Ruby不像Git那么简单，需要借助[HomeBrew](http://brew.sh/index_zh-cn.html)来安装
 	
* 首先安装HomeBrew 	

	1. ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"  
	2. brew doctor  //这个是用来诊断的，当出现Your system is ready to brew.就表示OK了。
	
	
* 安装Ruby

		curl -L https://get.rvm.io | bash -s stable --ruby
		
		或者安装指定的稳定版本：
		rvm install 2.0.0
		rvm use 2.0.0	
		rvm rubygems latest
	
		以上二者选一
				
			

###(2) 安装Octopress

* 2.1 安装octopress<br/>

> 首先在建立一个文件夹存放octopress，我的目录是 ~/Dev/Github.

  执行命令：
 
		1. cd Dev/Github  //进入存放octopress的目录
		2. git clone git://github.com/imathis/octopress.git octopress
		3. cd octopress   //进入octopress的目录，以后的所有操作都是基于进入该目录后的操作，请注意

* 2.2 安装Bundler<br/>
>	这一步会出现网络问题，可以多试试几次，如果不行，请使用VPN.
	
	执行命令：
	 	
		1. gem install bundler
		2. bundle install
		
* 2.3 预览安装效果
		
	执行命令：
	
		rake preview
			
	然后在浏览器中打开：http://localhost:4000 就可看到效果了	



###(3) 发布新文章
	
  * 执行命令：
  
		cd octopress
		rake new_post["你的文章标题"]
   
   然后会在`octopress/source/_posts`的目录下生成你命名的 markdown文件，使用 markdown编辑器编辑你要写的文章就可了
	
* 及时预览

   执行命令：
		
		rake generate   //将你编写markdown文件转化为HTML
		rake preview    
		 
		 
		
		
		
###(4) 文件提到到Git/部署
* 4.1 创建Github帐号

	打开[Github](http://github.com)

* 4.2 创建repository 

	命名： [your_username].github.io ,创建成功过后出现SSH地址：git@github.com:[your_username]/[your_username].github.io.git
	
	`注意不要命名成为youname.github.com的形式，这是Github之前使用的格式，现在推荐的是yourname.github.io`
	
* 4.3 将本地的octopress发不到Github pages

   执行命令：
		
		cd octopress
		rake setup_github_pages
		
		该步骤会提醒您输入SSH地址，就把您创建您的repository的SSH地址粘贴进入就可了	   	
* 4.4 提交更新到Github
   
   执行命令：
   
		git add .
		git commit -m '您的提交备注'
		git push origin source
		
		每次有变动都要执行该3个命令做数据同步

* 4.5 部署
   
   执行命令：
		
		rake generate
		rake deploy
		
		   
   		   	
  ___小技巧：rake gen_deploy 等同于 rake generate 和 rake deploy, 是不是很方便呢—___
	



###如果出现权限的问题，请在命令前加上sudo



###参考:
1. [http://shengmingzhiqing.com/blog/setup-octopress-with-github-pages.html/](http://shengmingzhiqing.com/blog/setup-octopress-with-github-pages.html/)
1. [http://williamherry.com/blog/2012/07/20/octopress-setup/](http://williamherry.com/blog/2012/07/20/octopress-setup/)