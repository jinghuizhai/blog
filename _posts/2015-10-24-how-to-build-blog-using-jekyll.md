---
layout: default
title: python的__name__和__doc__属性
---
<h1>python的__name__和__doc__属性</h1>
<p>
    每个模块都有一个__name__属性，用于判断当前模块是不是程序入口。如果是,__name__ == &#39;__main__&#39;。<br/>
</p>
<p>
    每个模块（module）,类（class）和函数（method包括类方法）都有一个__doc__属性，这个属性就是在类或函数声明之后，紧接着的一段字段串，注意不是注释而是字符串。
</p>
<p>
    比如：
</p>
<pre class="brush:python;toolbar:false"><code>class Dog(object):
    &quot;this class is dog&quot;
    def run(self):
        &#39;I can run&#39;
        pass</code></pre>
<p>
    调用：
</p>
<pre class="brush:python;toolbar:false"><code>print Dog.__doc__ #this class is dog
dog = Dog()
print dog.run.__doc__ #I can run</code></pre>
<p>
    是的，__doc__属性就是类或方法的说明。<br/>
</p>
<p>
    那么，自然知道模块的__doc__属性怎样写了：
</p>
<pre class="brush:python;toolbar:false"><code>test.py:
&quot;this is module test used testing&quot;
test2.py:
import test
print test.__test__# this is module test used testing</code></pre>
<p>
    <br/>
</p>

