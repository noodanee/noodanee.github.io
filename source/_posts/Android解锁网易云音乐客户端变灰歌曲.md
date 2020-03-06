---
title: Android解锁网易云音乐客户端变灰歌曲
date: 2019-05-02 11:26:32
tags:
---
### 发现
我在github上发现一个很有意思的项目，它可以解锁网易云音乐变灰歌曲[UnblockNeteaseMusic](https://github.com/nondanee/UnblockNeteaseMusic)，它的原理是通过代理替换变灰歌曲的链接来实现解锁。
### 思考
它是一个Node项目，需要部署在有Node环境的机器上，可以部署到自己的电脑在局域网使用，也可以部署到自己的服务器。那要是我没有自己的服务器呢？
我有一个大胆的想法，我要让它在我的Android上跑，<del>这样我就可以折(zhuang)腾(bi)了。</del>
### 实战
1. 首先下载一个Android Terminal Emulator
	[Termux](https://www.lanzous.com/i3vmj6b)是一个强大的终端模拟器，开箱即用，自带pkg包管理器。
2. 安装好Termux后打开依次运行以下命令
	```bash
	pkg install git 
	pkg install nodejs
	```
	安装git和nodejs，clone项目
	```bash
	git clone git@github.com:nondanee/UnblockNeteaseMusic.git
	```
	进入到UnblockNeteaseMusic目录
	```bash
	cd UnblockNeteaseMusic/
	```
	运行项目
	```bash
	node app.js
	```
3. 这一波操作不出意外的话Server启动成功
	```bash
	HTTP Server running @ http://0.0.0.0:8080
	```
4. 最后设置自动代理脚本地址
	WLAN > 修改网络 > 高级选项 > 代理 > 代理自动配置 > PAC网址
	```bash
	http://127.0.0.1:8080/proxy.pac
	```
	或者全局代理
	代理服务器主机名:localhost(127.0.0.1)
	代理服务器端口:8080
完成之后打开网易云音乐，就解锁灰色歌曲了。

![](/assets/20190502001.png)![](/assets/20190502002.png)![](/assets/20190502003.png)

<style type="text/css">
   img {
    		width: 30%;
        display: inline-block;
        text-align: center;
    }
</style>


