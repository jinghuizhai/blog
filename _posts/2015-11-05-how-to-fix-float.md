---
layout: default
title: 如何清浮动
---
#如何清浮动
我们已经习惯了如何用<strong>伪类</strong>清浮动(清除浮动不良影响)
<pre><code>
.fix:after{
	display:table;
	content:'';
	clear:both;
}
</code></pre>
lt IE8 下是没有display:table属性的，而且也不支持伪类（love属性除外）
所以上述请浮动方法在lt IE8中是没有效果的。
那么如何清除lt IE8的浮动呢？
<h2>当我们在谈清浮动的时候，我们在谈些什么？</h2>
当一个块级元素的内容有浮动属性时，浮动元素和绝对定位元素一样脱离了正常的文档流，
于是造成div塌陷，换句话说就是外部元素失去了包裹性。所以最简直粗暴的方法是给外部div
加上height属性，这样，内部的浮动元素就无法逃出外部元素的手掌心了。但是，并不是在所有时候
外部元素都能确定具体height的，那怎么办呢？我们要关心的是问题的本质，我们可以找一些无伤大雅的属性
既不改变原有元素的表现，又具有包裹性，这样的特性有：
<ul>
	<li>overflow（hidden）</li>
	<li>zoom（1）</li>
</ul>
二者选一个，就能清除浮动了。
然而<strong>请注意：</strong>
zoom属性（将元素放大2倍）在chrome和opera中都有作用（虽然zoom：1相当于没有作用）
而overflow：hidden会使元素内部的绝对定位（position:absolute）元素超出部分被遮挡。
所以要避免以下坑：
<ul>
	<li>内部有绝对定位元素需要超出外部元素展示，比如菜单</li>
	<li>zoom最好利用下IE的hack，避免在所有浏览器下都发生作用（*zoom：1）</li>
</ul>
这里有一个口诀：7加6减都星星，意思是IE6：_zoom:1,IE7:+zoom:1,IE6&IE7:*zoom:1
<h2>如何综合处理，一次编写，到处清浮动呢？</h2>
<ul>
	<li>在确定内部没有超出外部元素的绝对定位元素情况下，外部元素加上一句overflow:hidden，就能解决一切问题</li>
	<li>在上述情况之外，就老老实实的用IE hack：
		<ul>
			<li>*zoom:1</li>
			<li>
				再为现代浏览器加上伪类：
				<pre><code>
.fix:after{
	display:table;
	content:''
	clear:both
}
				</code></pre>
			</li>
		</ul>
	</li>
</ul>
<h2>如何用inline-block实现列表布局</h2>
<img src="https://raw.githubusercontent.com/jinghuizhai/jekyll_demo/gh-pages/img/2015-11-05-code.png"/>
<br/>
如果是lt IE8，需要加上<code>display:inline;</code>,但是不要写在同一个代码块中。
<hr/>
其实，还有一个最好的清浮动办法：lt IE8禁止访问。如果所有的公司、网站都这样做，互联网会变得更好，用户的体验也是。
<p>
完。
</p>