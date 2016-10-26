title: 本站搭建小结
date: 2015-09-09
categories: Tool
toc: true
tags: 
- hexo 
- GitHub
description: 记录搭建的过程。老师说： ”好记性不如烂笔头“。
---
本小站采用 [hexo](http://hexo.io/) 结合[githubpage]搭建,hexo资料：
+ [文档](http://hexo.io/docs/) 
+ [troubleshooting](http://hexo.io/docs/troubleshooting.html) 
+ [GitHub](https://github.com/hexojs/hexo/issues)
<!-- more -->
约定当前路径：项目所在根目录

## 安装hexo
前置条件

+ [Node.js](https://nodejs.org/)
+ [Git](http://git-scm.com/)

安装hexo

``` bash
$ npm install hexo --no-optional
```

## 常用hexo 命令

``` bash
$ hexo init [path] 			# 初始化一个项目
$ hexo new "My New Post" 	# 新建一篇博文
$ hexo server 				# 本地调试
$ hexo generate				# 生成HTML
$ hexo deploy 				# 部署到远程服务器
```
======
. 代表初始化项目的根目录
项目的全局配置文件 ./_config.yml
主题的配置文件 ./theme/(themename)/_config.yml
## 全局配置
``` ruby
# Hexo Configuration
## Docs: https://hexo.io/docs/configuration.html
## Source: https://github.com/hexojs/hexo/

# Site
title: Puzzlefun
subtitle: stay hungry stay foolish
description: 学习iOS笔记，分享自己的学习路程，记录脚下的每一个脚印
author: invokefear
language: zh-CN
timezone: 

# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: puzzlefun.github.io
root: /
permalink: :year/:month/:day/:title/
permalink_defaults:

# Directory
source_dir: source
public_dir: public
tag_dir: tags
archive_dir: archives
category_dir: categories
code_dir: downloads/code
i18n_dir: :lang
skip_render:

# Writing
new_post_name: :title.md # File name of new posts
default_layout: post
titlecase: false # Transform title into titlecase
external_link: true # Open external links in new tab
filename_case: 0
render_drafts: false
post_asset_folder: false
relative_link: false
future: true
highlight:
  enable: true
  line_number: true
  auto_detect: false
  tab_replace:

# Category & Tag
default_category: uncategorized
category_map:
tag_map:

# Date / Time format
## Hexo uses Moment.js to parse and display date
## You can customize the date format as defined in
## http://momentjs.com/docs/#/displaying/format/
date_format: YYYY-MM-DD
time_format: HH:mm:ss

# Pagination
## Set per_page to 0 to disable pagination
per_page: 10
pagination_dir: page

# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: freemind

# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: https://github.com/puzzlefun/puzzlefun.github.io.git
  
feed:
  type: atom
  path: atom.xml
  limit: 20
  hub:

## https://github.com/PaicHyperionDev/hexo-generator-search
search:
  path: search.xml
  field: post
  
```
### 配置主题 

下载主题
e.g [freemind](https://github.com/wzpan/hexo-theme-freemind.git)
 
``` bash
cd theme/
$ git clone https://github.com/wzpan/hexo-theme-freemind.git themes/freemind
$ npm install hexo-tag-bootstrap --save
```
在全局配置文件_config.yml 中Extension节中设置
``` json
theme: freemind
```
hexo [theme](http://hexo.io/themes/)提供了多种主题
## 主题配置
本站采用的主题为 freemind
``` ruby

slogan: "好好学习 天天向上"

theme: false
inverse: false

menu:
  - title: Archives
    url: archives
    intro: "All the articles."
    icon: "fa fa-archive"
  - title: Categories
    url: categories
    intro: "All the categories."
    icon: "fa fa-folder"
  - title: Tags
    url: tags
    intro: "All the tags."
    icon: "fa fa-tags"
  - title: About
    url: about
    intro: "About me."
    icon: "fa fa-user"

links:
  - title: "Puzzle4fun"
    url: https://github.com/puzzlefun
    intro: "My Github account."
    icon: "fa fa-github"
  - title: "My LinkedIn"
    url: https://cn.linkedin.com/in/carl-liu-337796a2
    intro: "My Linkin account."
    icon: "fa fa-linkedin"

widgets:
- search
- category
- tagcloud
- recent_posts  
- links

rss: atom.xml
fancybox: true
favicon: favicon.png
duoshuo_shortname: puzzlefun

# Analytics
google_analytics:
  enable: false
  siteid:
baidu_tongji:
  enable: true
  siteid: e358945bd22b2347e568dd59e2f62845

# search
# swiftype_key: ZP2ZSuHgipSZfRyU8uTR

# share widgets
bdshare: true
jiathis: false

```
### 添加 网站统计
e.g [百度统计](http://tongji.baidu.com/)创建一个网站统计id

``` json
baidu_tongji:
  enable: true
  siteid: [your baidu tongji id]
```
 该配置会在主题的layout中增加统计的代码，根据自己的需要可以适当的
 
 ### 添加 多说评论
 

## 引用
+ http://baoxiehao.com/2014/05/17/Hexo%E5%8D%9A%E5%AE%A2%E4%BC%98%E5%8C%96/
+ http://hexo.io/docs/deployment.html
