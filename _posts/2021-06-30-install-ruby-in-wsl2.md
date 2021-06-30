---
layout: post
title: "wsl2 安装bundle"
subtitle: ""
thumbnail-img:  ../assets/img/202103/20210310174652-8-queen-cover.jpg
comments: true
gh-repo: nigolarer/mine-blog
gh-badge: [star, follow]
tags: [ruby, bundle]
---

# 简介

今天心血来潮想要开始写文章了, 关于wsl2的踩坑记录, 但是开局就遇到另一个坑. 博客开始的时候我遇到过图片路径需要设置为绝对经否则图片找不到的问题, 后来接触typora后, 想要用typora在个人博客写点东西了, 毕竟markdown体验第一, 于是需要解决两个问题:
- 一是路径问题, 必须要让typora能加载图片, 
- 二是流程图问题, 不论如何还是想支持流程图, 靠贴图来写流程图实在是低效.

搜索一圈之后发现有一个插件(https://github.com/jeffreytse/jekyll-spaceship#installation)可以帮我来实现, 暂且不管github上是否可用, 因为github对插件的管理很严格,第三方的插件是会被自动禁用的. 但是我发现本地的bundle命令居然安装不上, 于是参考了这个老哥的文章: https://seankilleen.com/2020/07/building-my-jekyll-blog-with-ubuntu-on-wsl2/

考虑到万一老哥以后删掉了, 我还是把他的原文复制了一份: 

The shortcut, if you don’t want to do all of that back and forthPermalink
mkdir repos to create a directory for my repositories
cd repos

Pulled my repo: git clone https://github.com/SeanKilleen/seankilleen.github.io.git

Update package list: `sudo apt update`

For Ruby: `sudo apt-get install ruby-full`

For Bundler: `sudo gem install bundler`

Install dev dependencies that my gems need: `sudo apt-get install make gcc gpp build-essential zlib1g zlib1g-dev`

Run `bundle install` which prompts for my password when things need elevation

now it works.

Run `bundle exec jekyll serve`

Watch it build and run in Linux and watch my blog be available in Windows.

```marmid:
participant: a
participant: b
participant: c
```


TODO 支持本地插件的解决方案 
https://github.com/jeffreytse/jekyll-deploy-action