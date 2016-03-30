---
layout: default
title: 'javascript日期比较'
---
# javascript日期比较
今天遇到一个问题。
ng-if指令一直很好用。
但是今天比较日期的时候总是出错。
查了angularjs的源码，明明是可以写表达式的
<code>{{expression}}</code>
将变量换成了字面量还有会有问题，明明前几天没有出现啊。
后来,不经意的，在日期的day加了一个零，结果瞬间都正确了。
原来js中，如果直接用操作符比较日期的时候，需要考虑天的问题。
后来又经过测试，month也有这个问题。
原则上直接用字符串形式不借助函数比较日期的时候，要确定日期的位数
必须相同，不足补零，否则无法出现正确的结果。
<br/>
复习一下js的日期：
<pre><code>
var date = new Date(),
	year = date.getFullYear(),
	month = date.getMonth()+1,
	day = date.getDate(),
	week = date.getDay();

console.log("date now:",year,month,day,week);

date.setDate(day+5);

console.log('date after 5 days:',date);
</code></pre>
<hr/>
完。
