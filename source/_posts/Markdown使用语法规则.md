---
title: Markdown使用规则
date: 2016-07-19 17:34:14
tags: 
	- Markdown 
---
### 说明
　　是一种轻量级标记语言，它的目标是实现易读易写。
### 标题 
　　如果一段文字被定义为标题，只要在这段文字前加#号即可。总共六级标题，使用几级标题在前面加多少个#号。（# 一级标题 ## 二级标题 ### 三级标题）。
### 列表 
　　列表有有序列表与无序列表的区别，在Markdown下，列表的显示只需要在文字前加上-或*即可变为无序列表，有序列表则直接在文字前加（1. 2. 3. ）符号要和文字之间加一个字符的空格。
### 引用 
　　如果需要引用一小段别处的内容只需要在文本前加入>（符号与内容之间有空格）这种尖括号。
### 显示阅读全文
　　在需要显示的地方添加`<!--more-->`那么就会在文中添加more的地方显示阅读全文。

<!--more-->

### 代码高亮
　　如果你只想高亮语句中的某个函数名或关键字，可以使用 \`函数名或关键字\` 实现。
	通常编辑器根据代码片段适配合适的高亮方法，但你也可以用\`\`\`代码块\`\`\`包裹一段代码，并指定一种语言。
![代码块](/uploads/daimagaoliang1.png)
　　支持的语言：actionscript, apache, bash, clojure, cmake, coffeescript, cpp, cs, css, d, delphi, django, erlang, go, haskell, html, http, ini, java, javascript, json, lisp, lua, markdown, matlab, nginx, objectivec, perl, php, python, r, ruby, scala, smalltalk, sql, tex, vbscript, xml等，可参考highlight.js `node_modules/highlight.js/lib`。
　　也可以使用 4 空格缩进，再贴上代码，实现相同的的效果。
![代码块](/uploads/daimagaoliang2.png)