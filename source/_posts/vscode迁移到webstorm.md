---
title: vscode迁移到webstorm
date: 2021-05-25 12:52:39
tags:
---
### vscode低成本迁移到webstorm
- 下载好webstorm之后
- 只需要安装几个插件就可以使用和vscode一样的功能了
  - Atom material icons 图标
  - CodeGlance 右侧代码条
  - gitToolBox git改动记录
  - Rainbow brackets 彩色括号
  - vscode keymap
 安装完vscode keymap 之后，进入到设置里，
 在左侧菜单中搜索keymap 
 点击搜索到的keymap选项
 将键盘映射设置为刚刚下载的vscode 然后点击保存，重启

 为什么用webstorm
 例如在编写vue项目的时候，直接在html部分引入组件可以自动import 并且在components里注册，而vscode的vetur虽然可以，但是有时候组件插入会出错，导致还要手动引入

 组件传值在标签中自动显示，也就是html的行内提示，父传子,子传父等等，以及行内样式的提示

 转为前端设计，不需要安装大量的插件，仅需超少量插件即可编写项目

 