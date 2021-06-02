---
title: vscode迁移到webstorm
date: 2021-05-25 12:52:39
tags:
---
### vscode低成本迁移到webstorm
#### 下载安装webstorm
#### 安装如下插件

  - Atom material icons - 项目的图标
  - CodeGlance - 代码编辑区右侧的概览条
  - gitToolBox - git 变更记录
  - Rainbow brackets - 彩色括号
  - vscode keymap - vscode 键盘映射
  <!-- - 我喜欢的主题 solaxxxx -->
 > 安装完vscode keymap 之后，进入到设置里
 在左侧菜单中搜索 keymap 
 点击搜索到的 keymap 选项
 将键盘映射设置为刚刚下载的 vscode 然后点击保存，重启

    为什么用 webstorm
1. 例如在编写 vue 项目的时候，直接在 html 部分引入组件可以自动import 并且在components里注册，而vscode的vetur虽然可以，但是有时候组件插入会出错，导致还要手动引入

2. html 的内联样式提示，组件的 prop 值，emit 的时间监听，以及行内样式，在 webstorm 中都有提示

安装完成后就可以愉快的写自己的前端项目了

 