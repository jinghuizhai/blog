---
layout: default
title: '如何安装git并连接到github'
---
#如何安装git并连接到github
<h2>下载msysgit</h2>
(http://msysgit.github.io/)[github]
如果不能下载，可以在很多地方搜索到。
<h2>install</h2>
安装的时候一路下一步，不要安装到C盘，因为权限会受限制
<h2>设置账号密码</h2>
<pre><code>
$ git config --global user.name 'yourname' //enter
$ git config --global user.email 'email@example.com'//enter
</code></pre>
<h2>设置github SSH key</h2>
获取key
<pre><code>
git bash:
$ ssh-keygen -t rsa -C 'email@example.com'
</code></pre>
将id_rsa.pub文件(在桌面的文件夹找)中的内容复制到github的sshkey textarea中。
这样就可以使用<code>git push origin [master]</code>命令提交代码了。
<p>notice：本机的账号密码设置与github没有关系。<strong>邀请别人加入组织时，被邀请人访问组织页面才能看到请求</strong></p>
<hr/>
完。
