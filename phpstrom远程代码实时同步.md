---
title: phpstrom远程代码实时同步
date: 2018-07-13 00:22:00
tags: 
 - 工具使用
---
## 前言

开发的时候一般的平台都是Windows，但是Windows对开发极其不友好，一般都会在本地Windows主机安装虚拟机，安装Linux环境进行项目的部署和测试。下面介绍一种Windows主机与Linux虚拟机（包括阿里云的服务器）代码同步的方法。这个方法使用jetbrains公司的很多产品包括idea、webstrom等等。

## 前置条件

在Windows与Linux中都有同一份代码。

## 配置步骤

1、打开Windows主机上的phpstrom，另外打开用phpstrom打开项目代码。选择tools->deployment->brower remote host。

2、点击右上方有三个点的一个按键，新建一个连接。

~~~shell
连接类型：sftp
依次填写虚拟机信息
root path项选中Linux虚拟机中的项目位置
打开mapping面板
选择deployment path为根路径/
确定保存
~~~

3、选择tools->deployment->auto upload开启自动上传代码。

此时，在Windows主机对项目所做的任何修改一旦被保存都会被实时推送到虚拟机中。一旦在Linux虚拟机中项目功能验证通过，开始推送到git远程仓库中。

## 注意

该方法可以避免由于Windows系统所带来的一些麻烦，同时能利用Windows图形化优势。当然，有钱的话直接买mac更合适。

该方法同样适用于远程服务器，并且所有的jetbrains家族的开发工具都支持该操作。

本博客就是通过phpstorm设置远程代码同步推送来加快部署。

