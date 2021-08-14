---
title: 写给前端工程师的Golang入门教程 —— 依赖管理
date: 2021-08-14 00:00:00
tags: Golang
---
## Node.js的依赖管理

在前端，我们通常使用npm管理依赖。

我们会使用`npm init`初始化一个项目，初始化完成会在当前目录下生成一个`package.json`的文件, 我们还会安装一些依赖，比如执行`npm install axios`安装`axios`http请求库，安装完成查看`package.json`

```json
{
  "name": "module",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "axios": "^0.21.1"
  }
}
```

`package.json`描述了整个项目的大致情况, 包括模块名字、模块版本号、模块描述、入口文件、模块脚本配置，作者、开源协议以及依赖情况。

项目下还存在一个`package-lock.json`文件, 它记录当前安装的每个依赖包的版本，

在运行`npm install`的时候，`npm`会使用这些确切的版本。

```json
  "dependencies": {
    "axios": {
      "version": "0.21.1",
      "resolved": "https://registry.npmjs.org/axios/-/axios-0.21.1.tgz",
      "integrity": "sha512-dKQiRHxGD9PPRIUNIWvZhPTPpl1rf/OxTYKsqKUDjBwYylTvV7SjSHJb9ratfyzM6wCdLCOYLzs73qpg5c4iGA==",
      "requires": {
        "follow-redirects": "^1.10.0"
      }
    },
    "follow-redirects": {
      "version": "1.14.1",
      "resolved": "https://registry.npmjs.org/follow-redirects/-/follow-redirects-1.14.1.tgz",
      "integrity": "sha512-HWqDgT7ZEkqRzBvc2s64vSZ/hfOceEol3ac/7tKwzuvEyWx3/4UegXh5oBOIotkGsObyk3xznnSRVADBgWSQVg=="
    }
  }
```

可以看到软件包的版本、下载地址、用于校验依赖包的sha512值和它的依赖，这里我们发现`axios`依赖了`follow-redirects`。

这些依赖安装到了项目下的`node_modules`目录。

![](https://gitee.com/noodanee/resource/raw/master/2021-8-14/1628908232918-image.png)

## Golang的依赖管理

Golang的依赖管理方案经历了一个曲折的过程。

GOPATH: 把所有的项目文件和依赖全部放在一个目录里，不同项目没办法使用不同版本的依赖，所以有了GOVENDOR。

GOVENDOR: 每个项目有自己的vendor目录，项目优先到vendor目录查找依赖，其次到GOPATH目录查找。

目前最新的Golang依赖管理是使用Go Modules。

使用`go mod init <module>`的方式初始化一个go mod项目

>`go mod init`相当于`npm init`

使用`go get <module>`的方式安装一个依赖包

>`go get`相当于`npm install`

```shell
$ go mod init github.com/noodanee/go-modules
go: creating new go.mod: module go-modules
$ go get github.com/go-resty/resty/v2
go get: added github.com/go-resty/resty/v2 v2.6.0
$ ls
go.mod  go.sum
```

我们初始化一个模块`github.com/noodanee/go-modules`

安装一个依赖`github.com/go-resty/resty/v2`

当前目录下产生两个文件`go.mod`和`go.sum`

```
module github.com/noodanee/go-modules

go 1.16

require github.com/go-resty/resty/v2 v2.6.0 // indirect

```

`go.mod`记录了当前模块名，当前项目使用的Golang版本以及依赖情况。

>`go.mod`相当于`package.json`

```
github.com/go-resty/resty/v2 v2.6.0 h1:joIR5PNLM2EFqqESUjCMGXrWmXNHEU9CEiK813oKYS4=
github.com/go-resty/resty/v2 v2.6.0/go.mod h1:PwvJS6hvaPkjtjNg9ph+VrSD92bi5Zq73w/BIH7cC3Q=
golang.org/x/net v0.0.0-20210405180319-a5a99cb37ef4 h1:4nGaVu0QrbjT/AK2PRLuQfQuh6DJve+pELhqTdAj3x0=
golang.org/x/net v0.0.0-20210405180319-a5a99cb37ef4/go.mod h1:p54w0d4576C0XHj96bSt6lcn1PtDYWL6XObtHCRCNQM=
golang.org/x/sys v0.0.0-20201119102817-f84b799fce68/go.mod h1:h1NjWce9XRLGQEsW7wpKNCjG9DtNlClVuFLEZdDNbEs=
golang.org/x/sys v0.0.0-20210330210617-4fbd30eecc44/go.mod h1:h1NjWce9XRLGQEsW7wpKNCjG9DtNlClVuFLEZdDNbEs=
golang.org/x/term v0.0.0-20201126162022-7de9c90e9dd1/go.mod h1:bj7SfCRtBDWHUb9snDiAeCFNEtKQo2Wmx5Cou7ajbmo=
golang.org/x/text v0.3.3/go.mod h1:5Zoc/QRtKVWzQhOtBMvqHzDpF6irO9z98xDceosuGiQ=
golang.org/x/tools v0.0.0-20180917221912-90fa682c2a6e/go.mod h1:n7NCudcB/nEzxVGmLbDWY5pfWTLqBcC2KZ6jyYvM4mQ=
```

`go.sum`记录了依赖的版本号，像`package-lock.json`一样也有依赖的依赖的版本号，还有校验依赖包的sha512值
>h1:开头的字符串，表示生成checksum的算法是第一版的hash算法，即sha256。

下载的依赖不像`Node.js`项目一样存放到当前`node_modules`目录，而是存放到`GOMODCACHE`目录，`GOMODCACHE`是一个go环境变量，通过`go env`可以查看`GOMODCACHE`的位置。

`cd`到`GOMODCACHE`指向的目录，我们发现它是按照模块名来组织依赖的。

```shell
$ ls
cache  github.com  golang.org  google.golang.org
```
`cd`到`github.com/go-resty/resty`
```shell
$ cd github.com/go-resty/resty
$ ls
v2@v2.6.0
```
好家伙！它是按版本来存放依赖的，以`@`符号作为版本分割符，这样就解决了多版本共存的问题。

## 总结

本文大致讲述了`Node.js`项目与`Golang`项目依赖管理的方式，对比了`Node.js`和`Golang`项目依赖管理的相同点和不同点。`Node.js`项目把依赖存放到项目的`node_modules`目录；`Golang`采用在项目下记录依赖，依赖文件实际存放到统一目录，这也是更通用的方式。

看到这里，我相信你对Golang的依赖管理已经有了一个深刻的认识。

欢迎关注我的公众号“**野生程序员的修炼**”，原创技术文章第一时间推送。

<center>
    <img src="https://gitee.com/noodanee/resource/raw/master/2021/08/13/1628787241618-a4cdaa95-d14e-4422-8851-f616c8f18f04.jpg" style="width: 100px;">
</center>
