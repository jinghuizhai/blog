---
layout: default
title: angularjs的简单实现
---
#angularjs的简单实现
很多人喜欢google的angularjs，它真正实现了前后端的分离，后端人员再也不用再html页面里填充杂乱的标签。
angular对搜索引擎不友好，非常适合于后端的单页面应用。在使用angulajs以前，我们想把数据插入到div中，只能通过拼接字符串的方式，
这对前端和后端都是噩梦。
我们可以借用angularjs的思想做一些东西，比如动态组装一个div，如果一个页面中这样的需求很少，
而去引用一个angularjs文件的话是很不划算的。那就自己实现一个:
##javascipt:
<pre><code>function model(el,data){
	    var objs = el.match(/[{]{2}\s*([^{}]+)\s*[}}]{2}/g),
	        ret = [];
	    if(objs){
	        objs.forEach(function(ele){
	            var m = ele.match(/[^{}\s]+/);
	            if(m) ret.push(m[0]);
	        });
	    }
	    if(ret){
	        var html = "";
	        data.forEach(function(ele){
	            var htm = el.slice(0);
	            ret.forEach(function(re,index){
	                htm = htm.replace(objs[index],ele[re]);
	            });
	            html = html+"\n"+htm;
	        });
	        return html;
	    }else{
	        return '';
	    }
	}
</code></pre>
##div:
	<ul id="list">
	    <li>
	        {{ name }}
	    </li>
	</ul>
##调用：
	var html = model(document.getElementById('list').innerHTML,[{name:'Tom'},{name:'Jack'},{name:'Jerry'}]);
	document.getElementById('list').innerHTML = html;
##结果：
	<ul id="list">
	    <li>
	        Tom
	    </li>
	    <li>
	        Jack
	    </li>
	    <li>
	        Jerry
	    </li>
	</ul>
_______________
实际上，model函数与angularjs的实现原理是不同的，但在紧要关头，却能解决特殊的问题。函数要用在生产环境中需要改进。