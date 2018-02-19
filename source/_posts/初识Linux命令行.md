---
title: 初识Linux命令行
date: 2018-02-20 06:07:01
categories:
- Linux
tags:
- 命令行
---
# 我的认知
##### 昨天简单学习了一下git bash,git bash是Windows操作系统中Git的命令行工具，如图

![image.png](http://upload-images.jianshu.io/upload_images/4929420-d1d29dcab358f681.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
##### 它和Windows自带的cmd命令行工具差不多，如图

![image.png](http://upload-images.jianshu.io/upload_images/4929420-35bc3791b9560ffc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
##### 那何谓[命令行](https://zh.wikipedia.org/wiki/%E5%91%BD%E4%BB%A4%E8%A1%8C%E7%95%8C%E9%9D%A2)呢?
> 一般说的“命令行”是指linux[命令](http://baike.baidu.com/item/%E5%91%BD%E4%BB%A4)，linux命令是对Linux系统进行管理的命令。对于Linux系统来说，无论是中央处理器、内存、磁盘驱动器、键盘、鼠标，还是用户等都是文件，Linux[系统管理](http://baike.baidu.com/item/%E7%B3%BB%E7%BB%9F%E7%AE%A1%E7%90%86)的[命令](http://baike.baidu.com/item/%E5%91%BD%E4%BB%A4)是它正常运行的核心，与之前的DOS命令类似。[linux](http://baike.baidu.com/item/linux)[命令](http://baike.baidu.com/item/%E5%91%BD%E4%BB%A4)在系统中有两种类型：内置Shell（外壳）命令和Linux命令。

# 常用命令行
## 1.cd命令
cd|打开目录|
-----|------|
cd ~|打开/c/Users/Administrtor/目录|
cd  /root/Docements|切换到目录/root/Docements|
cd  ./path | 切换到当前目录下的path目录中，“.”表示当前目录|
cd  ../path| 切换到上层目录中的path目录中，“..”表示上一层目录|
cd - |回到刚才的目录（返回）|
**注意**|上面只能打开目录、文件夹（**directory**），不能打开文件（**file**)|
## 2.start命令
start|用图形界面（GUI)打开,    目录、文件夹和文件都可以打开|
---|---|
start ~|打开/c/Users/Administrtor/目录|
start  /root/Docements|切换到目录/root/Docements|
start  ./path | 切换到当前目录下的path目录中，“.”表示当前目录|
start  ../path| 切换到上层目录中的path目录中，“..”表示上一层目录|
## 3.pwd命令：显示当前目录
## 4.mkdir命令
mkdir|创建目录|
---|---|
mkdir dirctory目录名|创建directory目录|
mkdir -p 目录名|创建目录，"-p"表示路径|
## 5.echo命令
echo|创建文件并写入内容|
---|---|
echo 'content'>文件路径|在创建的文件中写入'content'|
echo 'content'>！文件路径|在创建的文件中写入'content'，重定向|
echo 'content'>>文件路径|在创建的文件中**追加**'content'|
## 6.touch命令
touch|创建文件|
---|---|
touch 文件名（test.txt等等）|创建文件(test.txt)|
**注意**|如果文件已存在，会更新文件创建时间。|
## 7.ls命令
ls|查看路径|
---|---|
ls -l （文件路径）|列出长数据串，包含文件的属性与权限数据等|
ls -a （文件路径） |列出全部的文件，连同隐藏文件（开头为.的文件）一起列出来（常用）|
ls -d （文件路径）|仅列出目录本身，而不是列出目录的文件数据|
ls -h （文件路径）|将文件容量以较易读的方式（GB，kB等）列出来|
ls -R （文件路径）|连同子目录的内容一起列出（递归列出），等于该目录下的所有文件都会显示出来|
## 8.cp命令
cp |复制文件、目录|
---|---|
cp 源路径 目标|复制文件|
cp -r 源路径 目标路径|复制目录|
## 9.mv命令
mv|移动节点
---|---
mv 源路径 目标路径|源路径移动到目标路径
mv -f |force强制的意思，如果目标文件已经存在，不会询问而直接覆盖
mv -i |若目标文件已经存在，就会询问是否覆盖
mv -u |若目标文件已经存在，且比目标文件新，才会更新
## 10.rm命令
rm|删除文件、目录
---|---
rm 文件路径|删除文件
rm -f  |就是force的意思，忽略不存在的文件，不会出现警告消息
rm -i |互动模式，在删除前会询问用户是否操作
rm -r |递归删除，最常用于目录删除，它是一个非常危险的参数
**注意**|永远不要运行 rm -rf /
## 11.find命令
find|查找文件
----|---
find . -name 'content'|查找文件名为content的文件

未完待续