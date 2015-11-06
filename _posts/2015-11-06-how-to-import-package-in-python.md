---
layout: default
title: python如何导入包
---
#python如何导入包
有三种情况
<p>假设有如下目录</p>
<pre><code>
root
	+model
		__init__.py
		animal.py
	+controller
		__init__.py
		dog.py
		controller.py
	index.py
</code></pre>
<h2>导入的文件与当前文件在同一个目录下</h2>
比如dog.py要导入controller.py:
<pre><code>
from controller import Controller
</code></pre>
notice：Controller是controller.py文件中的类
<h2>导入的文件在当前文件的平级目录下</h2>
比如index.py要导入controller下的dog.py
<pre><code>
from controller.dog import Dog
</code></pre>
<h2>导入的文件在当前文件的父目录下</h2>
比如在dog.py中导入animal.py
<pre><code>
import sys
sys.path.insert(0,'..')
from model.animal import Animal
</code></pre>
<hr/>
notice:一个文件夹（folder）对外要呈现为一个包(package),需要在文件夹中包含__init__.py文件，文件可为空。
<br/>
完。