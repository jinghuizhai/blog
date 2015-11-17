---
layout: default
title: '常用git命令'
---
#常用git命令
<p>初始化</p>
<pre><code>
git init
</code></pre>
<p>添加一个修改</p>
<pre><code>
git add .
git add -A
</code></pre>
<p>提交</p>
<pre><code>
git commit -m 'add a file'
</code></pre>
<p>删除文件</p>
<pre><code>
git rm readme.md
并提交
git commit -m 'remove a file'
</code></pre>
<p>创建分支</p>
<pre><code>
git branch dev
</code></pre>
<p>切换分支</p>
<pre><code>
git checkout dev
</code></pre>
<p>查看当前分支</p>
<pre><code>
git branch
</code></pre>
<p>合并分支</p>
<pre><code>
在master分支上操作
git merge dev
</code></pre>
<p>删除分支</p>
<pre><code>
git branch -d dev
可以看出来
删除分支用关键字 -d(means delete)
而删除文件用关键字rm(means remove)
个中差别，慢慢体会
</code></pre>
合并时会有冲突，需要在合并文件中修复，消除冲突，最后提交已经解除冲突的文件。



