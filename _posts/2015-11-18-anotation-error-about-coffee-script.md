---
layout: default
title: 'coffee script中会出现的缩进错误'
---
#coffee script中会出现的缩进错误
<code>coffee script</code>语法简洁，像<code>Python/Ruby</code>，但是在注释方面处理有些坑。例子：
<pre><code>
add = (x,y) ->　
#
this is a function realize additive operation
#
	x+y
</code></pre>
会发现出现<code>unexpected indentation error</code>，看来是注释的错误，我们现在修改下
<pre><code>
add = (x,y) ->
#
	this is a function realize additive operation
#
	x+y
</code></pre>
一样会出现错误，看来光缩进注释内容太天真啊：
<pre><code>
add = (x,y) ->
	#
	this is a ……
	#
	x+y
</code></pre>
编译成功了，终于看到编译后的js代码了:
<pre><code>
(function(){
	var add;
	add = function(x,y){
		/*
		this is a ...
		*/
		return x+y;
	};
}).call(this);
</code></pre>
那能不能嵌套注释呢？
<pre><code>
#
add (x,y) -> 
	#
	test
	#
	x+y
#
</code></pre>
仍然出错。可见：
<strong>coffee script 在编译coffee的时候，强行要求缩进，而且现在还没有实现嵌套注释，在这种情况下，要使用类似于<code>python</code>的注释，尽量写的简洁：</strong>
<pre><code>
def add(x,y):
	'''
	this is a add function
	'''
	return x+y
</code></pre>
<hr/>
完。