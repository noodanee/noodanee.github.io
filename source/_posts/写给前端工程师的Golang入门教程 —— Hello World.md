---
title: 写给前端工程师的Golang入门教程 —— Hello World
date: 2021-08-12 00:00:00
tags: Golang
---
# 写给前端工程师的Golang入门教程 —— Hello World

> Go is an open source programming language that makes it easy to build simple, reliable, and efficient software.

## 环境搭建

我们在前端搭建环境时会先安装[Node.js](https://nodejs.org/)，安装Node.js有几种方法

1. 下载安装包或二进制文件
2. 使用系统包管理工具安装
3. 使用版本管理工具安装

对应我们也有这几种方法可以安装Golang

### 下载安装包或二进制文件

我们可以在[Golang下载页](https://golang.org/dl/)找到不同系统对应的安装包或二进制文件，这里不再赘述。
这个方案版本升级不太方便，需要手动下载最新版本覆盖旧版本，这里更推荐下面的方案。

### 使用系统包管理工具安装

在不同的系统都有自己的包管理工具，可以让我们很好的对应用进行管理

在Windows下，目前较好用的包管理工具是[Chocolatey](https://chocolatey.org/)，使用Chocolatey安装：

```powershell
choco install golang
```

在Mac下，最好用的包管理工具当然是[Homebrew](https://brew.sh/)，使用Homebrew安装：

```bash
brew install golang
```

安装命令执行完成后输入命令 `go version`  , 控制台打印golang版本号则代表安装成功。

### Golang版本管理工具

在Node.js中，有[nvm](https://github.com/nvm-sh/nvm), 对应在Golang社区也有[gvm](https://github.com/moovweb/gvm)

可以用 `gvm install` 命令显示可以下载和编译可用的 Golang 版本

安装特定的 go 版本只需运行 `gvm install <version>`命令，其中 `<version>` 是表示要安装的版本。假设你正在处理一个使用 go 1.16.7 版本的项目，你就可以使用 `gvm install go1.16.7` 命令来安装这个版本。

使用 `gvm use `  命令来切换到新安装的 go 1.16.7 版本。如果不想每次敲 gvm use 指令来切换版本，你可以加上 --default 参数来指定默认使用这个版本。

这里还要介绍另一款工具是[g](https://github.com/voidint/g), 它与Node.js的[n](https://github.com/tj/n)也是一样的用法

`g ls-remote `  查询可供安装的所有go版本

`g install <version>`  安装目标go版本

`g ls`  查询已安装的go版本

`g use <version>`  切换到另一个已安装的go版本

`g uninstall <version>`  卸载一个已安装的go版本

### 国内镜像配置

在使用npm安装项目依赖的时候，我们会设置npm的源来加快安装速度。

```bash
npm config set registry https://registry.npm.taobao.org
```

同样go的中央仓库也在国外，我们需要设置go的国内镜像，可以使用`goproxy.cn`  或 `goproxy.io` 

```bash
$ go env -w GO111MODULE=on
$ go env -w GOPROXY=https://goproxy.cn,direct
```
## Hello World

创建一个main.go文件

```golang
package main

import "fmt"

func main() {
	fmt.Println("hello world!")
}
```

控制台运行 `go run main.go` 

```bash
$ go run main.go
hello world!
```

至此，我们第一个Hello World程序就完成啦！是不是很简单呢？

欢迎关注我的公众号“**野生程序员的修炼**”，原创技术文章第一时间推送。

<center>
    <img src="https://gitee.com/noodanee/resource/raw/master/2021/08/13/1628787241618-a4cdaa95-d14e-4422-8851-f616c8f18f04.jpg" style="width: 100px;">
</center>
