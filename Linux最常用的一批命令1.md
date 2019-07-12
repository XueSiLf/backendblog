---
title: Linux最常用的一批命令1
date: 2019-07-01 23:39:37
tags: Linux,Linux命令
---
[TOC]

内容：主要是Linux关于下面几个方面操作的命令：

* 目录操作
* 文本处理
* 压缩
* 日常运维
* 系统状态概览
* 工作常用

# 1.目录操作

主要是对目录和文件的操作。

## 1.1 基本操作(mv、rm、cp、mkdir)

* mkdir 创建目录（make dir）
* cp 拷贝（复制）文件（copy）
* mv 移动文件（move）
* rm 删除文件（remove）
* touch 新建文件

例子：

~~~bash
# 创建目录和父目录a,b,c,d
mkdir -p a/b/c/d
# 在当前文件夹中创建文件夹a
mkdir a

# 拷贝文件夹a到/tmp目录
cp -rvf a/ /tmp/
# 拷贝a文件夹下a1文件到b文件夹中并且重命名为b1
cp /a/a1 /b/b1

# 移动文件a到/tmp目录，并重命名为b
mv -vf a /tmp/b

# 删除tmp目录的所有文件
rm -rvf /tmp/   或者  rm -rf /tmp/
# 删除单个文件
rm 1.c

# 新建一个文件
touch 1.c
~~~

## 1.2 漫游

~~~bash
ls命令能够看到当前目录的所有内容。 ls -l能够看到更多信息。

pwd命令能够看到当前终端所在的目录。

cd命令能够切换到对的目录。

find命令通过筛选一些条件，能够找到已经被遗忘的文件。例如：find / -name "文件名.文件后缀"
~~~

# 2.文本处理

## 2.1 Vim技巧系列

## 2.2 Sed技巧系列

## 2.3 AWK技巧系列

# 3.查看文件

## 3.1 cat命令

查看文件最常用的就是cat命令了。但是如果文件很大的话，cat命令的输出结果会疯狂在终端上输出，可以多次按ctrl+c终止。

~~~bash
# 查看文件大小
du -h file
# 查看文件内容
cat file
~~~

## 3.2 less命令

针对比较大的文件，可以使用less命令打开某个文件。类似vim，less可以在输入/后进入查找模式，然后按n(N)向下（上）查找。有许多操作都和vim操作类似，可以类比看下。

## 3.3 tail命令

大多数做服务端开发的同学，都了解这个命令。比如，查看nginx的滚动日志。

~~~bash
tail -f access.log
~~~

tail 命令可以静态的查看某个文件的最后n行，与之对应的，head命令查看文件头n行。但head没有滚动功能。

~~~bash
tail -n100 access.log
head -n100 access.log
~~~

## 3.4 统计命令

sort和uniq经常配对使用。sort可以使用 -t 指定分隔符，使用 -k 指定要排序的列。

下面这个命令输出nginx日志的ip和每个ip的pv，pv最高的前10

~~~bash
# 2019-06-26T10:01:57+08:00|nginx001.server.ops.pro.dc|100.116.222.80|10.31.150.232:41021|0.014|0.011|0.000|200|200|273|-...
awk -F"|" '{print $3}' access.log | sort | uniq -c | sort -nk1 -r | head -n10
~~~

## 3.5 其他命令

# 4.压缩（tar、bzip2、unzip、unrar）

为了减小传输文件的大小，一般都开启压缩。Linux下常见的压缩文件有tar、bzip2、zip、rar等，7z这种用的相对较少。

* .tar 使用tar命令压缩或解压
* .bz2 使用bzip2命令操作
* .gz 使用gzip命令操作
* .zip 使用unzip命令解压
* .rar 使用unrar命令解压

最常用的就是.tar.gz文件格式了。其实是经过了tar打包后，再使用gzip压缩。

~~~bash
# 创建压缩文件
tar cvfz archive.tar.gz dir/
# 解压
tar -zxvf archive.tar.gz
~~~

