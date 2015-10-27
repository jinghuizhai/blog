---
layout: default
title: 如何实现javascript子元素选择器
---
#如何实现javascript子元素选择器
使用类库选择dom元素的子元素是非常方便的，是jQuery中，可以这样：<code>$('#ele').find(1)</code>选择id为ele的第二个子元素
那么我们自己去写一个子元素的选择器，应该怎么做呢？
在原生的javascript中，选择子元素有firstChild,lastChild,childNodes等属性，但是，因为浏览器的差异性，
在lt IE8中以上三个属均是忽略空白的Text元素的，但是现代浏览器不忽略，本来想着ele.firstChild,ele.childNodes[0]搞定，但其实，根本不行。
没事，有办法，定义一个id选择器先：
<code>function $(id){return document.getElementById(id);}</code>
以及打印结果的函数：
<code>function l(arg){console.log(arguments);}</code>
<h2>首先我们可以利用dom元素的firstChild和nextSibling属性：</h2>
<pre><code>
	function first(ele){
		var firstChild = ele.firstChild;
		while(firstChild.nodeType === 3) firstChild = firstChild.nextSibling;
		if(!firstChild || firstChild.nodeType !== 1) return null;
		return firstChild;
	}
</code></pre>
<h2>然后利用childNodes属性：</h2>
<pre><code>
	function first2(ele){
		var children = ele.childNodes;
		for(var i = 0,len = children.length;i<len;i++){
			var el = children[i];
			if(el.nodeType === 1){
				return el;
			}
		}
	}
</code></pre>
<h3>最后利用非标准却在包括IE（IE7/8 also include）的各大浏览器中早已实现的属性：children</h3>
这个属性竟然过滤（或者没有选择）空的Text节点，这真是太好了。代码格外简单：
<pre><code>
	function first3(ele){
		return ele.children(0);
	}
</code></pre>
<h2>测试，每个选择器都连续选择1w次</h2>
<pre><code>
	var then = new Date().getTime();
	l('first start');
	for(var i = 0;i<100000;i++){
		var el = first(test);
	}
	var middle = new Date().getTime();
	l(middle-then);
	then = middle;
	l('first2 start');
	for(var i = 0;i<100000;i++){
		var el = first2(test);
	}
	middle = new Date().getTime();
	l(middle-then);
	middle = then;
	l('raw start');
	for(var i = 0;i<100000;i++){
		var el = first3(ele);
	}
	l(new Date().getTime()-then);
	l('end');
</code></pre>
<h2>结果：</h2>
<pre><code>
	["first start"]
	[37]
	["first2 start"]
	[48]
	["raw start"]
	[90]
	["end"]
</code></pre>
<hr/>
<code>first</code>最快，<code>first2</code>次之，原生的<code>children</code>最慢，然而chilren最方便。
