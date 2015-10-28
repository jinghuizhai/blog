---
layout: default
title: 在php中mysql和mysqli的不同
---
#在php中mysql和mysqli的不同
mysql和mysqli是php操作数据库的扩展（extension）
<h2>php-mysql</h2>
mysql是最原始的扩展（extension），用法非常常见：
<pre><code>
<?php
	mysql_connect($host,$user,$pass);
	$result = mysql_query('select * from `user`');
	while($row = mysql_fetch_array($result,MYSQL_ASSOC)){
		echo $row['name'];
	}
	mysql_free_result($result);
?>
</code></pre>
以上连接数据库的方式是不能绑定参数(bind column)的，所以拼接参数的时候
非常容易sql注入(sql Injection),所以用<code>mysql_escape_string()</code>
和<code>mysql_real_escape_string()</code>转义字符（php5.3.0之后就弃用了）。
然而一旦字段多了以后就会这样：
<pre><code>
$query = sprintf('select * from `user` where user="%s" and pass = "%s"');
mysql_real_escape_string($user);
mysql_real_escape_string($pass);
muysql_query($query);
</code></pre>
<h2>php-mysqli</h2>
php-mysqli(php-mysql improve),是php-mysql的加强。支持：
<ul>
	<li>参数绑定（bind column）</li>
	<li>事务（transation）</li>
	<li>多参数（muti query）</li>
	<li>面向对象风格(Object oriented style)</li>
</ul>
看看用法吧：
<pre><code>
$mysqli = new mysqli($host,$user,$pass,$name);
$sql = 'insert into `user` set name=?';
$stmt = $mysqli->prepare($sql);
$stme=>bind_param($name);
$stmt->execute();
$stme->bind_result($name);
while($stmt->fetch()){
	echo $name;
}
$stmt->close();
$mysqli->close();
</code></pre>
<hr/>
这两样的区别就是这些了，最后的选择是pdo(php data object)，是官方推荐的扩展，需要php5.5及以上的环境。
这是我自己在项目中用的一个[lib](https://github.com/jinghuizhai/mysql-pdo)，欢迎clone及issue。