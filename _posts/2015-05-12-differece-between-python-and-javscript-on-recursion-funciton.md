---
layout: default
title: 用在dom上的递归和python有什么不同
---
#用在dom上的递归和python有什么不同
##javascript:
将dom元素（element）都加上某个类（class）：
<pre><code>function addClass(ele,class){
	if(ele instanceof Array){
		for(var i = 0,len = ele.length;i<len;i++){
			addClass(el,class);
		}
	}else{
		ele.className = ele.className+" "+class;
	}
}
</code></pre>
在这个上述例子中，使用递归式非常方便的，关键是，这种情况可以使用递归，函数addClass的功能类似python中的map函数
##python:
求一个list的和：
<pre><code>def getSum(list):
	sum = 0
	for key in list:
		sum = sum+key
	return sum

list = range(101)
print getSum(list)
</code></pre>
***

