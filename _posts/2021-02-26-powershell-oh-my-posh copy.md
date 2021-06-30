---
layout: post
title: "将 PowerShell Oh-My-Zsh 化"
subtitle: "美化和支持git快捷键"
thumbnail-img: ../assets/img/202102/20210226181309-powershell-beauty-cover.png
comments: true
tags: [powershell, git]
---

windows下可以比较好的兼容到vscode的终端就是powershell了, 但是powershell win95的配色实在是难受, 而且对于git flow based开发者来说不能使用zsh里面的git简写实在是噩梦.

我本来使用windows terminal的wsl, 在linux下安装zsh用的挺好, 但是不小心升级到了wsl2, 一下子文件系统不通用了, 而且比较糟糕的是linux的虚拟机环境不能用我的梯子, 因此github速度很慢而且一些插件下载不下来.

那么既然两边都不好用, 好歹搞定一头, 本着这样的思想, 我开始美化power shell

> 准备插件

1. oh-my-posh
2. https://github.com/gluons/powershell-git-aliases

> 开始安装

### oh-my-posh
oh-my-posh的安装教程很多, 按部就班的过程中还是遇到一些小问题记录下来:

1.运行`Import-Module oh-my-posh` 后没有反应. 其实已经生效了, 但是没有设置主题,导致看起来好像没有安装成功.

2.`$profile`文件不存在, 这其实只要在对应的目录下新建一个文件即可, 很简单.

3.设置主题: `set-theme`的时候报错:


```
Hi there!

It seems you're using an oh-my-posh V2 cmdlet while running V3.    
To migrate your current setup to V3, have a look the documentation.

https://ohmyposh.dev/docs/upgrading
```

提示`oh-my-posh`版本不正确, 并建议upgrade config 到 ver3, 但是实际上恰恰相反, 正是因为版本已经是ver3了而我们还在用v2的命令导致不兼容.
解决办法就是采用新版本命令: `set-poshpromt -theme`, 我的文件配置如下:

```
Import-Module posh-git
Import-Module oh-my-posh
Set-PoshPrompt -Theme robbyrussel

Import-Module git-aliases -DisableNameChecking
```

4.主题乱码问题. 我在配置一些主题后发现一些字符乱码, 和网友的效果图不一样, 于是设置了一个很朴素的主题, 绕过了这个问题. 主题名见上面的配置.

### git alias
这个没啥问题只需要按照`readme`配置就完事儿了. 最后还是参考上面的配置文件, 将git加入到配置中就可以实现随终端启动了.