---
layout: default
title: 介绍一款简单的JavaScript进度条
---
# 介绍一款简单的JavaScript进度条
## How to use
<pre><code>
var progress = $.simpleProgress({
	id:'progress',
	step:4,
	text:['first','second','third','forth'],
});
</code></pre>
## API
<p>
  <ol>
    <li>next()</li>
    <li>getCurrent()</li>
    <li>getStep()</li>
  </ol>
</p>

## sample
```
progress.next();
console.log(progress.getCurrent());
console.log(progress.getStep());
```
<a href="https://github.com/jinghuizhai/simpleprogress">link</a>
