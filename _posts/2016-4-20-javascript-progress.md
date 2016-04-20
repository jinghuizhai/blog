---
layout: default
title: 介绍一款简单的JavaScript进度条
---
# 介绍一款简单的JavaScript进度条
## How to use
```
var progress = $.simpleProgress({
	id:'progress',
	step:4,
	text:['first','second','third','forth'],
});
```
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
