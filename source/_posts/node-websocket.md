---
title: Nodejs搭建简单的websocket服务
date: 2021-03-10 08:20:18
tags: 
- Nodejs
- 后端入门
categories: Nodejs
---
### 简单的后台服务搭建流程
- 创建一个文件夹 `websocket-server`
- 终端执行`cd`命令进入到`websocket-server`文件夹
- 执行`yarn add nodejs-websocket`或`npm install nodejs-websocket`,用以安装nodejs的`websocket`模块
- 待模块安装完成后，在当前目录新建 app.js 文件
- 简单代码如下
![](https://upload-images.jianshu.io/upload_images/25023219-cef1a8ce059bd338.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



- 创建服务的过程和使用`http`模块创建服务的过程类似，终端执行`node app.js`,可以看到终端打印出，监听了端口3000，这样一个简单的websocket后台服务就创建完了。

### 前端与websocket服务建立连接
- 在当前目录下创建index.html文件
- 在`body`标签中写入代码
![](https://upload-images.jianshu.io/upload_images/25023219-18a3c680c7bcbb36.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- 在`script`标签中写入如下代码获取dom元素
![](https://upload-images.jianshu.io/upload_images/25023219-e17df728d86970cb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- 如下为websocket的事件API
![](https://upload-images.jianshu.io/upload_images/25023219-68ecb89b99371d49.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- 前端创建一个websocket连接，并监听websocket的open事件
![](https://upload-images.jianshu.io/upload_images/25023219-ac5b84b9adbfd2c9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
> 这里的地址不是http协议，而是websocket
- 用vscode的live server 打开index.html文件，看到浏览器如下

![](https://upload-images.jianshu.io/upload_images/25023219-a88852498c7df11d.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
这标志着我们与后端的websocket服务成功建立了连接，这时打开开发人员工具
可以在图示位置看到我们与后端websocket建立的连接
![](https://upload-images.jianshu.io/upload_images/25023219-605c7b9ede7fac86.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在往下进行之前，要先对后端的代码进行一些异常处理，不然我们每次页面一刷新，后端会直接报错并停掉服务。
在app.js文件中添加如下代码
![](https://upload-images.jianshu.io/upload_images/25023219-0170d8e546e7e86b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
这两段代码分别是对连接关闭时和异常的事件进行处理，对两个事件进行处理之后，我们前端进行访问才不会报错

### 前后端数据交互
- 在`button`上监听一个点击事件，调用websocket的`send()`方法向后端发送input的内容
![](https://upload-images.jianshu.io/upload_images/25023219-72a3bd14e7bccb9b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- 点击按钮，打开控制台，可以看到我们发送的数据

![](https://upload-images.jianshu.io/upload_images/25023219-1818be301af94ec0.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 后端接收数据处理，并返回给前端
![](https://upload-images.jianshu.io/upload_images/25023219-dd4404ee4e623d71.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- 接受到前端发送的数据后，将字母转为大写返回给前端
>前端代码添加如下逻辑
![](https://upload-images.jianshu.io/upload_images/25023219-65c5e160eaa20004.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) 

- input输入内容，点击按钮，效果如下图
![](https://upload-images.jianshu.io/upload_images/25023219-a072044b20815db0.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
>红色内容为后端返回的内容，绿色内容为我们发送给后端的内容。  

至此，一个简单的websocket服务和前后端交互逻辑就完成了。

>前端完整代码
![](https://upload-images.jianshu.io/upload_images/25023219-b0e1c9f41bfcd56e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>后端完整代码
![](https://upload-images.jianshu.io/upload_images/25023219-066fe795dbb971be.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)