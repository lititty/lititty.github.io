---
title: Athens代理或搭建go私服
date: 2019-04-16 23:26:27
tags: Go
---
`go1.11`以后就可以使用`GOPROXY`代理下载包依赖了<br>
使用`athens`可以很快的使用代理<br>
#### 两种方法 
(需`go1.11`以上)
#### 一、直接使用athens网站的代理

配置环境变量
```
export GOPROXY="https://athens.azurefd.net"
```
ps: 记得`source`
#### 二、安装athens
设置`GO111MODULE`变量

linux：
```
export GO111MODULE=on
```
windows:
```
$env:GO111MODULE = "on"
```
设置http、https代理(毕竟被墙)
```
export {http_proxy,https_proxy}=http://127.0.0.1:1087  (一般是1080端口，我的是1087)
```

然后用`git`把项目`clone`下来
```
$ git clone https://github.com/gomods/athens
$ cd athens/cmd/proxy
$ go install
$ proxy &   (后台进程方式启动，也可以使用screen等方式)
[1] 27892
INFO[0000] Exporter not specified. Traces won't be exported
INFO[0000] Starting application at http://127.0.0.1:3000
```
然后再配置`GOPROXY`

```
export GOPROXY=http://127.0.0.1:3000
```
配置完成之后使用
`go mod download`
或者
`go get`
之后，都会使用`GOPROXY`代理的地址来获取到依赖了
