---
layout: default
title: 记录下我的sublimeText3设置
---
#记录下我的sublimeText3设置
setting default:
<pre><code>
{
	"always_show_minimap_viewport": true,
	"color_scheme": "Packages/User/Color Highlighter/themes/Monokai.tmTheme",
	"font_size": 11,
	"ignored_packages":
	[
		"Vintage"
	],
	"word_separators": "./\\()\"':,.;<>~!@#$%^&*|+=[]{}`~?",
	"word_wrap": false
}
</code></pre>
key binding:
<pre><code>
[ {"keys":["f5"],
"caption": "SublimeREPL: Python - RUN current file",
"command": "run_existing_window_command", "args":
{
"id": "repl_python_run",
"file": "config/Python/Main.sublime-menu"
}}
,{ "keys": ["ctrl+b"], "command": "toggle_side_bar" }
,{ "keys": ["ctrl+q"], "command": "reveal_in_side_bar" }
,{ "keys": ["ctrl+m"], "command": "exec", "args": {"kill": true}}
]
</code></pre>
我经常使用的插件：
<ul>
	<li>convertoutg-8</li>
	<li>htmlbeautiful</li>
	<li>jsformat</li>
	<li>package control</li>
	<li>sftp</li>
	<li>sublimecodeintel</li>
	<li>sublime repl</li>
</ul>
