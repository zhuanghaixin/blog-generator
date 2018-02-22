---
title: 从URL输入到页面实现
date: 2018-02-22 20:45:49
categories:
- 前端
tags:
- HTML
- 网络
---
>当用户打开浏览器，输入 baidu.com，页面展示百度首页。整个过程发生了什么？
输入baidu.com，敲起回车，将域名baidu.com通过DNS域名解析成IP地址，然后向该IP地址的服务器发起请求，服务器响应并进行处理，往浏览器（客户端）发送HTML等等的文件，浏览器收到文件后进行解析处理，在通过浏览器渲染把页面呈现到我们的屏幕上。

![image.png](http://upload-images.jianshu.io/upload_images/4929420-4d8e562a2355b83a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
下面我们详细解释这一过程...
# 一.在浏览器输入URL
## 1.URL是什么？
谈到URL,不得不提一下URI(Uniform Resource Identifier),统一资源标识符，用于标识资源。URI是一种可以用于WWW之外的高效识别码，它被用于主页地址、电子邮件、电话号码等各种组合中，如下表示：
** http://www.rfc-editor.org/rfc/rfc4395.txt **
** http://www.ietf.org:80/index.html **
** http://localhost:631 **
这些例子属于一般主页网址，也被叫做URL（Uniform Resource Locator)。URL常被人们用来表示互联网中资源文件的具体位置。但是URI不局限标识互联网资源，它可以作为所有资源的识别码。现在，在有效的RFC文档中，已经不使用URL,转而在使用URI。相比URL狭义的概念，URI是一个广义的概念。因此，URI可以用于除了www之外的其他应用协议中。

URL组成：URL由协议，域名，端口，文件路径组成
例子：**https://github.com:8080/zhuanghaixin**
协议：传输的协议，比如http、https、ftp、file 协议
域名：github.com即为域名,一个URL中，也可以使用IP地址作为域名使用
端口：跟在域名后面的是端口，域名和端口之间使用“:”作为分隔符。端口不是一个URL必须的部分，如果省略端口部分，将采用默认端口
文件路径：/zhuanghaixin即为文件的路径
# 二.域名解析
## 1.域名是什么？
以一个常见的域名为例说明，baidu网址是由二部分组成，标号“baidu”是这个域名的主域名
体，而最后的标号“com”则是该域名的后缀，代表的这是一个com国际域名，是[顶级域名](https://baike.baidu.com/item/%E9%A1%B6%E7%BA%A7%E5%9F%9F%E5%90%8D)。而前面的www.是网络名， 为www的域名。

## 2. IP地址是什么？
IP地址是指互联网协议地址（[英语](https://baike.baidu.com/item/%E8%8B%B1%E8%AF%AD)：Internet Protocol Address，又译为网际协议地址），是IP Address的缩写。IP地址是[IP协议](https://baike.baidu.com/item/IP%E5%8D%8F%E8%AE%AE)提供的一种统一的地址格式，它为互联网上的每一个网络和每一台主机分配一个逻辑地址，以此来屏蔽物理地址的差异。目前还有些ip代理软件，但大部分都收费。
- 每个处于互联网中的设备都有IP 地址，形如 192.168.0.1
- 局域网 IP 和公网 IP 是有差别的
- 127.0.0.1代表本机的 IP

## 3.域名解析的流程
对于 http://www.baidu.com, 浏览器实际上不知道 www.baidu.com到底是什么东西，需要查找baidu.com网站所在服务器的IP地址，才能找到目标。
寻找过程：

- 浏览器缓存，浏览器会缓存DNS记录一段时间

![image.png](http://upload-images.jianshu.io/upload_images/4929420-1bf3b3ddc98783c1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


- 系统缓存 - 从 Hosts 文件查找是否有该域名和对应 IP

![image.png](http://upload-images.jianshu.io/upload_images/4929420-6ea05f7d6a48ca05.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 路由器缓存 – 一般路由器也会缓存域名信息
- ISP DNS 缓存 – 比如到电信的 DNS 上查找缓存

![image.png](http://upload-images.jianshu.io/upload_images/4929420-bcdfed50b030b8df.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](http://upload-images.jianshu.io/upload_images/4929420-6ec9d9325c4b884e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 如果都没有找到，则向根域名服务器查找域名对应 IP，根域名服务器把请求转发到下一级，直到找到 IP。
比如说浏览器想要查询www.baidu.com的IP地址，前面的方法都找不到，它就开始查询根服务器，找到com域名解析服务器，然后查询com解析服务器，找到baidu.com域名解析服务器，最好查询baidu.com域名解析服务器，获得www.baidu.com的IP地址。

![image.png](http://upload-images.jianshu.io/upload_images/4929420-b74055381888daab.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](http://upload-images.jianshu.io/upload_images/4929420-07df6d467068a0c8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 三.服务器处理
## 1.服务器是什么？
服务器是一台安装系统的机器，常见的系统如Linux、windows server 2012。系统里安装的处理请求的应用叫 Web server。常见的 web服务器有 Apache、Nginx、IIS、Lighttpd。
## 2.web服务器的作用？
浏览器把用户发起的HTTP请求发送给服务器后，Web server会进而在它做自己的存储空间中搜索所请求的文件（因为同一个服务器地址，有时候可能同时绑定了多个域名，此时需要配置web服务器将请求转给相应的端口）。当找到这文件时，这个服务器会读取它，按需处理它，并且把它传送回浏览器。Web server就相对于起到了内容分发的作用，为不同域名的用户请求展示其相应的内容,如下图。
![](http://ww1.sinaimg.cn/large/005AXjHngy1fhsly9i8f1j30fr07tdg4.jpg)

# 四.网站处理
这一步指的是网站后台处理数据反馈给浏览器之前的过程，常见的处理模型有MVC 模型(model)-视图(view)-控制器(controller)，控制器从数据模型中拿到数据，再从试图中拿到HTML，经过处理，返回html字符串给浏览器。
![](http://ww1.sinaimg.cn/large/005AXjHngy1fhsm36mlywj30el0f3jro.jpg)

# 五.浏览器处理
HTML字符串被浏览器接受后被一句句读取解析
解析到link 标签后重新发送请求获取css

解析到 script标签后发送请求获取 js，并执行代码

解析到img 标签后发送请求获取图片资源

# 六.绘制网页
浏览器根据 HTML 和 CSS 计算得到渲染树，绘制到屏幕上，并且js 会被执行