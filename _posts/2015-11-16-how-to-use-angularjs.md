---
layout: default
title: 'angularjs的基本功能'
---
#angularjs的基本功能
<h2>service</h2>
service方法里写的是业务逻辑，像是后端mvc中的M层功能。定义好一个对象，并且定义好对象的各种方法，
最后返回。
<h2>controller</h2>
controller将service返回的数据和view关联起来，与后端mvc的controller功能类似。
<h2>directive</h2>
指令。暂时我还没完全悟透，我在项目中常用来执行重复的动作。
<h2>例子：</h2>
一个页面中会有很多controller，每个controller负责一个模块的视图，现在有一个视图要展示所有的用户(users)，先初始化：
<pre><code>
myapp = angular('my-app');
</code></pre>
业务逻辑：
<pre><code>
myapp.service('userService',function(){
	var obj = {
		get:function(http,fn){
			http.get('http://localhost/user.php',{params:{}}).success(function(r){
				if(typeof fn == 'function'){
					fn(r);
				}
			});
		},
		getProvince:function(http,fn){
			http.get('http://localhost/province.php',{params:{}}).success(function(){
				if(typeof fn == 'function'){
					fn(r);
				}
			});
		}
	};
	return obj;
});
</code></pre>
关联视图:
<pre><code>
myapp.contoller('userCtrl',function($scope,$http,userService){
	userService.get($http,function(data){
		$scope.users = data;
	});
});
</code></pre>
好了，现在有一个select，我们希望懒加载，获取焦点的时候才加载下拉列表,比如要加载所有的省份:
<pre><code>
&lt;select request-province&gt;
&lt;option ng-model="p in provinces" value="{{ p.province_id }}" &gt; {{ p.name }} &lt;/option&gt;
&lt;/select&gt;
</code></pre>
这样的下拉列表也许很多，我们就写成一个指令，在多个地方调用：
<pre><code>
myapp.directive('requestProvince',function(userService){
	return {
		restrict:'A',
		link:function(scope,ele,attrs){
			ele.bind('focus',function(){
				userService.getProvince(function(data){
					scope.provinces = data;
				});
			});
		}
	};
});
</code></pre>
or:
<pre><code>
myapp.directive('requestProvince',function($http){
	return {
		restrict:'A',
		link:function(scope,ele,attrs){
			ele.bind('focus',function(){
				http.get('http://localhost/province.php',{params:{}}).success(function(r){
					scope.provinces = r;
				});
			});
		}
	};
});
</code></pre>
<hr/>
完。
