---
layout: default
title: 如何实现jQuery里的addClass，removeClass和hasClass方法
---
#如何实现jQuery里的addClass，removeClass和hasClass方法
<h2>按照惯例，先实现一个id选择器和打印方法</h2>
<pre><code>
function l(arg){
	console.log(arguments);
}
function $(id){
	return document.getElementById(id);
}
</code></pre>
<h2>addClass</h2>
addClass的本质其实就是在类名之后添加一个字符串，只是需要判断一下原来的类名，只要能处理好空格，就能写好这个方法：
<pre><code>
function addClass(ele,clazz){
	var className = ele.className.trim();
	if(className) ele.className = className+" "+clazz;
	else ele.className = clazz;
}
</code></pre>
<h2>removeClass</h2>
addClass的实现没有什么诀窍，但是removeClass就不同了，添加和减去一个类，本质就是对字符串进行操作，对字符串的操作方法有很多：
<ul>
	<li>split</li>
	<li>slice</li>
	<li>replace</li>
	<li>+</li>
</ul>
那么究竟哪种方法好呢？先考虑split方法，split可以将字符串按照分隔符分解并组装成一个数组（Array）,这样
就可以把对字符串的操作转化成对Array的操作，这会更简单：
<pre><code>
arr = ['a','b','c'];
retarr = new Array();
for(var i = 0,len = arr.length;i++){
	if(arr[i] != 'c') retarr.push(arr[i]);
}
var class_str = retarr.join(' ');
</code></pre>
对数组的操作直观些，一看就明白，但是有一个问题：
<pre><code>
var str = "   a   b    c   ";
console.log(str.split(' '));
</code></pre>
猜猜看上面代码的结果？
<pre><code>
Array[36]
</code></pre>
如果你已经先到这个结果了，证明对javascript的API还是比较熟悉的，split方法不会将非空字符中间的空格看成一个。
既然你能想到结果，那么你应该也能想到这个方法：
<pre><code>
str.split(/\s+/);
</code></pre>
将split的参数改成正则表达式，这样，不管你是几个空格，统统搞定，我们来看下lt IE8以及现代浏览器下的结果吧：
<pre><code>
g IE8 & modern:
['','a','b','c']
lt IE8:
['a','b','c']
</code></pre>
不吃惊，IE总是跟别人不一样，只是不知道不一样的什么，fantasy。
那么我们可以使用上面的代码，先正则，变成数组，再循环。既然总要使用正则，那只使用正则可以么？
<pre><code>
function removeClass(ele,clazz){
	if(hasClass(ele,clazz)){
		ele.className = (' '+ele.className+' ').replace(' '+clazz+' ','').trim();
	}
}
</code></pre>
反正都要用正则，不如只用一次。
你也看到了，removeClass依赖于hasClass:
<h2>hasClass</h2>
<pre><code>
function hasClass(ele,clazz){
	if((' '+ele.className+' ').match(' '+clazz+' ')) return true;
	return false;
}
</code></pre>
<hr/>
好了，可以把这些方法集成到一起，再添加一些方法，就成为自己的simple lib来替代厚重的jQuery，但是，上面的
代码有不够好的地方，就是没有考虑传入的dom元素是nodelist怎么办。不难实现，我们加一个递归就可以了：
<pre><code>
function addClass(ele,clazz){
	if(ele.length){
		for(var i = 0,len = ele.length;i<len;i++){
			addClass(ele[i],clazz);
		}
	}else{
		var className = ele.className.trim();
		if(className) ele.className = className+" "+clazz;
		else ele.className = clazz;
	}
}

function hasClass(ele,clazz){
	if(ele.length) ele = ele[0];
	if((' '+ele.className+' ').match(' '+clazz+' ')) return true;
	return false;
}

function removeClass(ele,clazz){
	if(ele.length){
		for(var i = 0,len = ele.length;i<len;i++){
			removeClass(ele[i],clazz);
		}
	}else{
		if(hasClass(ele,clazz)){
			ele.className = (' '+ele.className+' ').replace(' '+clazz+' ','').trim();
		}
	}
}
</code></pre>

