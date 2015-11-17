---
layout: default
title: 'nodejs写的分段工具'
---
#nodejs写的分段工具
在写blog时，习惯先在sublime里写。有时候看到一些文章转载时，直接粘贴会没有分段。
于是写了一个分段的小工具，记录在这里，方便下次使用。
<pre><code>
var fs = require('fs');

fs.readFile('test.md','utf8',function(err,data){
	if(err) throw err;
	var result = data.match(/<div>(.*)<\/div>/);
	if(result[1]){
		result = result[1];
		var arr = result.split('。');
		var newarr = [];
		fs.writeFile('test2.txt',arr.join('\n'),function(err){
			if(err) throw err;
			console.log('done');
		});
	}
});
</code></pre>
<hr/>
完。