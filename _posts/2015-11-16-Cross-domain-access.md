---
layout: default
title: 'javascript跨域访问'
---
#javascript跨域访问
这里的例子的是结合php
<h2>php的header</h2>
<pre><code>
header('Access-Control-Allow-Origin: *');//有人说只这条就行，但是我测试不work。
header("Access-Control-Allow-Headers: Origin, X-Requested-With, Content-Type, Accept");
header('Access-Control-Allow-Methods: GET, POST, PUT');
</code></pre>
这样就可以访问到了，但是最近在使用angularjs的时候，需要这样访问:
<pre><code>
var url = 'http://192.168.10.x/test.php';
$http({
    method: 'POST',
    url: url,
    data: $.param({fkey: "key"}),
    headers: {'Content-Type': 'application/x-www-form-urlencoded'}
}).success(function(r){
	console.log(r);
});
</code></pre>
如果是get方法呢：
<pre><code>
$http.get(url,{params:{name:'Tom'}}).success(function(r){
	console.log(r);
});//params是必须的
</code></pre>
<hr/>
完。