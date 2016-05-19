---
layout: default
title: avalon引入模板
---
# avalon引入模板
通常我们需要在当前界面进行弹窗操作的时候，经常会使用模板。
<br/>
引入的方式有两种，一种是写在当前页面的script里，另外一种是通过ajax加载，前一种方式适用于简单操作，表单并不复杂，后一种方式多是为了完成复杂操作，就有必要写在一个独立的文件中。
<br/>
下面介绍方式
<br/>
1 script
<br/>
<pre><code>
<div ms-controller="test">
    <p>{{xxx}}</p>
    <div ms-include="'tpl'"></div>
</div>
</code></pre>
<pre><code>
<script type="avalon" id="tpl">
    here, {{ 3 + 6 * 5 }}
</script>
</code></pre>
2 ajax
<br/>
<pre><code>
<div  ms-include-src="'tmpl.html'"></div>
</code></pre>
这需要服务器的支持。
<br/>
> 1 如果大家想在模板加载后，加工一下模板，可以使用 data-include-loaded 来指定回调的名字。
> 2 如果大家想在模板扫描后，隐藏loading什么的，可以使用 data-include-rendered 来指定回调的名字。
以上两句话，我只用过2,data-include-rendered后面的回调函数是在文档加载完之后触发的，这个时候如果需要jquery操作dom节点，就可以操作了。
