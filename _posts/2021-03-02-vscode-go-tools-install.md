---
layout: post
title: "vscode 安装 go 工具失败问题"
subtitle: "如 gopls, gopkg, golint 等"
thumbnail-img: ../assets/img/202103/20210302170520-golang-cover.png
comments: true
tags: [golang, vscode]
---

vscode 安装 go 插件的时候会报网络错误, 简单一搜基本上是因为墙. 大致看了下网上的解决方案基本是靠进入到 `$GOPATH` 下进行项目的 clone 和 install, 但是我通过按照教程执行之后却依然报错. 忘记保存报错日志, 看了下基本上是说没有发现指定的项目, 而且我确认是按照教程 clone 的.

鉴于以上, 很容易想到通过 `GOPROXY` 的方式来修复问题, 那么我们开始吧. 

> 设置 GOPROXY

通过修改 `go env` 中的 `GOPROXY` 可以实现走国内的代理, 从而解决网络问题: 
* goproxy.io
* goproxy.cn // (推荐)由国内的七牛云提供。

### windows 环境

```
go env -w GOPROXY=https://goproxy.cn,direct
```

### mac 或 linux 环境

```
export GOPROXY=https://goproxy.cn,direct
```

当然对于 IDE 而言, 不同的 IDE 都提供了相应的 Settings, 如 goland 中可以在: `Go modules(vgo)` 中配置proxy:
```
https://goproxy.cn,direct
```
设置好后, 还可以通过 `go env` 检查配置情况.


> 安装 go 工具

设置好 proxy 后就可以安装工具了, vscode 自动安装(install all)是无法正常安装的, 他走的自己配制的命令, 似乎没有使用到 proxy, 因此我们需要自己跑 `go get` 命令. 也很简单 ,vscode 右下角点击 `install all` 之后, 可以看到它的执行 log:
```
Error: Command failed: C:\Go\bin\go.exe get -v github.com/ramya-rao-a/go-outline
```
那么我们只要自己手动在 terminal 中执行如下命令即可:
```
go get -v github.com/ramya-rao-a/go-outline 
```

同理的, 根据报错信息将缺少的工具依次 `go get` 后 vscode 不再报错, enjoy!

