---
title: github报错
date: 2021-05-27 17:57:10
tags:
---
####  fatal: unable to access 'https://github.com/kmq116/hexo-blog.git/': OpenSSL SSL_read: Connection was reset, errno 10054


打开Git命令页面，执行git命令脚本：修改设置，解除ssl验证
`git config --global http.sslVerify "false"`
链接：https://www.cnblogs.com/newAndHui/p/14741634.html