---
layout: default
title: '使用angularjs的较佳实践'
---
#使用angularjs的较佳实践
一开始不太明白为什么angular没有处理模块依赖的问题，后来才发现，
只要ng写的简洁，一个文件处理所有的业务逻辑，其实是最好的，加上压缩处理后，其实
文件并不大。极其复杂，需要很多模块的系统不在上述结论之列。
<h2>如何使用路由</h2>
ng处理路由，是借助html5的新特性实现的。url加上#号后，后面的字符串再多，依然是当前页面，
不会跳转。ng监听url的变化加载不同的模板，这样就实现了无刷新的单页面应用。例子:
<pre><code>
var myapp = angular.module('myapp',['ngRoute']);
myapp.config(['$routeProvider',function($routeProvider){
	$routeProvider
	.when('/',{
		templateUrl:'static/dashboard.html',
		controller:'dashboardCtrl'
	})
	.when('list',{
		templateUrl:'static/user.html',
		controller:'userCtrl'
	});
html:（伪代码）
a href="#/" 控制台 /a
a href="#/user" 用户 /a
</code></pre>
notice:ng里已经声明的controller不需要在页面中重复声明，意思是,在<code>/static/user.html</code>里：
<pre><code>
<div ng-controller="userCtrl">
	//some html codes
</div>
</code></pre>
ng-contrller声明是不必要的，这会造成http重复请求。
<h2>如何处理业务逻辑</h2>
ng的service层包干了后端MVC之model层的业务。所以前端的curl可以这样写：
<pre><code>
myapp.service('userService',function($http){
	var obj = {
		get:function(params,fn){
			$http({
			    method: 'POST',
			    url:'user/find',
			    data: $.param(params),
			    headers: {'Content-Type': 'application/x-www-form-urlencoded'}
			}).success(function(r){
				//请求的数据绑定到userService上
				obj.data = r;
				if(tpyeof fn == 'undefined') fn(r);
			});
		},
		add:function(){
			//pass
		},
		update:function(){
			//pass
		},
		delete:function(){
			//pass
		}
	};
	return obj;
});
</code></pre>
以上就是对user模型的增删改查。如果只看里面的函数，还以为是用nodejs写的后端代码。
<h2>如何处理视图</h2>
<pre><code>
myapp.controller('userCtrl',function($scope,userService){
	
	//请求指定用户
	var params = {
		phone:'150XXXXXXXX',
		email:'XXX@16.com'
	};
	userService.get(params,function(r){
		$scope.users = userService.data;
	});
});
</code></pre>
<h2>html怎么写</h2>
<pre><code>
伪代码：
ul
	li ng-repeat="u in users" {{ u.name }} /li
ul
</code></pre>
<h2>事件绑定怎么写</h2>
<pre><code>
html:
button ng-click="add($event.target)" 添加 /button
//$evant.target是button这个dom对象
angularjs:
$scope.add = function(othis){
	othis.disabled = true;
	userService.add($scope.name,function(){
		othis.disabled = false;
		console.log('已经添加');
	});
};
</code></pre>
<h2>指令怎么用</h2>
凡是指令可以实现的，不使用它也可以实现。然而很多时候使用指令时更方便的。
比如有的模块非常标准化，那就可以写成指令，方便随时调用。
<pre><code>
//把请求的省份拼成html放在select里，这个请求省份的模块我们经常使用，因此我们写成指令。
myapp.directive('requestProvice',function($http){
	restrict: 'A',
	link:function(scope,ele,attrs){
		ele.bind('focus',function(){
			$http({
			    method: 'POST',
			    url:'province/find',
			    data: {},
			    headers: {'Content-Type': 'application/x-www-form-urlencoded'}
			}).success(function(r){
				ele.html(r);
			});
		});
	}
});
html:（伪代码）
select request-province
/select
notice:注意指令在html中怎么写。
</code></pre>
将这些模块拼装起来，就成为丰富的单页面应用。但这不是最佳实践。
<hr/>
完。
