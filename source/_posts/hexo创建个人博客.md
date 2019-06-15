---
title: hexo创建个人博客
date: 2019-06-13 11:15:57
tags:
---
#### 什么是Hexo

Hexo是一个基于Node.js的静态博客程序，可以方便的生成静态网页托管在Github和Heroku上。并且有很多人为其制作了很多优秀的主题（theme），你可以根据自己的喜好进行设置。主题的设置将在后面的章节中介绍。

---
#### 怎么在Github上搭建一个hexo博客

创建比较简单
#### 安装Git
前往Git官网下载Windows版本压缩包，下载完成后解压安装。

#### 安装Node.js
前往Node.js官方下载网站，下载Node.js官方安装包，下载完成后同样解压安装。

#### 安装Hexo
安装Hexo所需要的环境已将安装完成，下一步只需要安装Hexo便可以了
npm install -g hexo-cli
hexo 便安装完成了

### 创建Hexo文件夹
在当前文件夹下面初始化
hexo init
成功后直接启动
hexo server 

### 提交部署到Github上
登录自己的GitHub账号
创建一个新的仓库

    特别注意仓库名称要和Github用户名保持一致----这样才能通过仓库名直接访问（例如:仓库名.github.io）
在项目更目录下面

    hexo deploy 或者  hexo d 进行项目的部署到Github上面
通过设置的  “仓库名.github.io”  进行访问自己的博客
如果访问不到404 查看自己的仓库名称是否和Github 的账户保持一致
这样大功告成  博客创建-部署

### 更换主题为yilia
git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia

