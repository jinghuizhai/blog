---
layout: default
title: '在windows下配置c语言环境'
---
#在windows下配置c语言环境
<h2>安装MinGW</h2>
mingw是c和c++的编译器，也是一个开发windows应用的工具包。
可以去source forge 下载，注意下载的文件很小，安装时它会从
source forge下载相应的安装包，所以总体下来有400M左右。
<br/>
安装后需要配置环境变量。如D:\dev\MinGW\bin.
<h2>选择编辑器</h2>
这里以notepad为例。
写好c文件后，点击运行，输入以下编译命令，保存，设置快捷键。
<pre><code>
cmd /k g++.exe -g -W -Wall -o $(CURRENT_DIRECTORY)/$(NAME_PART).exe "$(FULL_CURRENT_PATH)" & PAUSE & EXIT
</code></pre>
运行的快捷键是：
<pre><code>
cmd /k $(CURRENT_DIRECTORY)/$(NAME_PART).exe "$(FULL_CURRENT_PATH)" & PAUSE & EXIT
</code></pre>
<hr/>
完。