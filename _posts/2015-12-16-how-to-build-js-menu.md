---
layout: default
title: '如何构建一个js菜单'
---
#如何构建一个js菜单
<pre><code>
function buildTree(arr,fn){
	if(!arr || arr.toString() == "false"){
		return document.createElement('p');
	}
	var domSelect = '';
	function itdom(arr,fn){
		if(arr.length > 0){
			var args = arguments;
			var ul = document.createElement('ul');
			for(var i = 0,len = arr.length;i<len;i++){
				var obj = arr[i];
				var li = document.createElement('li');
				var span = document.createElement('span');
				if(obj.sub){
					span.innerHTML = "<i class='fa fa-folder-o'></i>"+obj.name;
				}else{
					span.innerHTML = obj.name;
				}
				(function(span,obj){
					span.onclick = function(){
						var kids = span.parentNode.children;
						if(kids[1]){
							if(kids[1].style.display == 'block'){
								span.children[0].className = "fa fa-folder-o";
								kids[1].style.display = 'none';
							}else{
								kids[1].style.display = 'block';
								span.children[0].className = "fa fa-folder-open-o";
								if(typeof fn == 'function'){
									fn(obj,span);
								}
							}
						}else{
							if(typeof fn == 'function'){
								fn(obj,span);
							}
						}
						if(domSelect){
							domSelect.style.backgroundColor = '#fff';
						}
						span.style.backgroundColor = '#efefef';
						domSelect = span;
					};
				})(span,obj);
				li.appendChild(span);
				if(obj.sub){
					li.appendChild(itdom(obj.sub,fn));
				}
				ul.appendChild(li);
			}
			return ul;
		}
	}
	return itdom(arr,fn);
}
</code></pre>
<h2>testing</h2>
<pre><code>
var arr = [{id:1,name:'总部',sub:[{id:2,name:'财务部'},{id:3,name:'行政部'}]}];

var html = buildTree(arr,function(obj,span){
	console.log(obj,span);
});

document.getElementById('tree').appendChild(html);
</code></pre>
notice:点击总部，查看效果。加入适量css，去掉list-type工更好，iconfont可以找一个文件夹。
<hr/>
完。