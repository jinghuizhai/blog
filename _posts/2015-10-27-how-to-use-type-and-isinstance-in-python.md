---
layout: default
title: 如何使用python的type和isinstance
---
#如何使用python的type和isinstance  
type函数和isinstance函数都是用来判断变量的所属类型，区别如下：  
<ul>
<li>type通过用来判断基本类型，也可以判断函数或类（像javascript中的typeof）</li>
<li>isintance通常用来判断类，也可以判断基本类型 （像javascript中的instanceof）  </li>
</ul>
<h2>type的用法</h2>
<pre><code>
	print type(1) #<class 'int'>  
	print type('str') #<class 'str'>  
	print type(None) #<type(None) 'NoneType'>  
</code></pre>
type()返回的是一个类，所以`type(1) == int`的结果是`True`  
type()也可以用来判断函数和对象
<pre><code>
	type(abs) #<class 'builtin_function_or_method'>
	type(a) #<class '__main__.Animal'>
</code></pre>
判断一个对象是否是函数的时候需要引入types
<pre><code>
	import types
	def test():
		pass
	print type(test) == types.FunctionType # True
	print type(abs) == types.BuiltinFunctionType #True
	print type(lambda x: x) == types.LambdaType #True
	print type((x for x in range(10))) == types.GeneratorType #True
</code></pre>
<h2>isinstance的用法：</h2>
<pre><code>
	class Dog():
		pass
	class Husky(Dog):
		pass

	tom = Husky()
	print isinstance(tom,Husky) #True
	print isinstance(tom,Dog) #True
</code></pre>
出现这样的结果是因为Husky和Dog是继承关系，所以isinstance()判断的是一个对象是否是该类型本身，或者位于该类型的父继承链上。
<h2>isinstance也可以像type一样判断基本类型：</h2>
<code>
	print isinstance(1,int) #True
</code>
<hr/>
使用type判断对象是比较麻烦的，用isinstance判断基本类型虽然是可以，但不够符合直觉。