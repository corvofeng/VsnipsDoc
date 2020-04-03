
Vsnips 使用时, 会尽可能兼容 Vim 中 Ultisnips 插件. 对于非 Vim 用户, 如果你只是想创建一些片段,
可以不必做太多考虑, 但是若与其他用户分享代码片段, 请尽量在 Vim 与 VSCode 中都确保运行成功.

## 最简单片段

此种片段不需要与任何变量交互, 因此兼容性最佳.

```
snippet dbg "Use IPython to debug"
# ---------- XXX: Can't GIT add [START] ---------- #
import IPython
IPython.embed(using=False)
# ---------- XXX: Can't GIT add  [END]  ---------- #
endsnippe
```

## 与 Vim 变量, 函数的交互

Vsnips 提供了对于 vimrc 中定义变量的查找, 在解析代码片段时, 会将vim中的变量进行替换, 以下方的代码片段为例.

```
snippet title "Hexo post header" b
---
layout: post
title: `!p snip.rv = get_markdown_title(snip)`
date: `!v strftime("%Y-%m-%d %H:%M:%S")`
author: `!v g:snips_author`
tags: 
description: ${3}
categories: Docs
photos:  
toc: true

---

${0}
endsnippet
```

使用`!v`开头的表示需要由 Vim 来解析, 上面的片段中`!v strftime("%Y-%m-%d %H:%M:%S")`, `!v g:snips_author`有两个 Vim 变量.
`strftime`为时间的处理, `g:snips_author`表示引用在vimrc中定义的变量(`let g:snips_author="corvo"`).

## 与自定义函数的交互

### 解析时替换

在 Vim 中使用 UltiSnips 时, 可以使用`!p snip.rv`表示此占位符由 Python 解析, 以下方代码为例:

```snippet
snippet ifmain "ifmain" b
if __name__ == `!p snip.rv = get_quoting_style(snip)`__main__`!p snip.rv = get_quoting_style(snip)`:
	${1:${VISUAL:main()}}
endsnippe
```

代码中有`!p snip.rv = get_quoting_style(snip)`这个函数, 这些函数先前均是由 Python 编写, 虽然我将插件功能移植到 VSCode,
但直接解析 Python 函数是有难度的, 所以在 Vsnips 中, 需要我们针对这些函数重写一份 JavaScript 代码,

* 原始 Python 代码

```python
def get_quoting_style(snip):
	style = snip.opt("g:ultisnips_python_quoting_style", "double")
	if style == 'single':
		return SINGLE_QUOTES
	return DOUBLE_QUOTE
```

* 重写后的 JavaScript 代码

```javascript
function get_quoting_style() {
  let style = VIM_VARS_MAP.get("ultisnips_python_quoting_style") || "double";
  if (style === "single") {
    return SINGLE_QUOTES;
  }

  return DOUBLE_QUOTES;
}
```

### 需要依靠代码的具体位置确定

上方的自定义函数可以在解析 snippet 代码片段时直接替换, 但是有一些函数, 例如我们想要获取当前文件的文件名,
就需要动态的处理这个函数. Vsnips 中的具体实现请查看[repush函数][1], 我们会在补全操作时调用`get_snip_body`
函数, 如果片段中存在js模板函数, 我们将会根据上下文信息进行替换.

Vsnips中, 自定义了一类函数, `!js {func_name}`的形式替换进模板. 仍然以这个标题为例

```
snippet title "Hexo post header" b
---
layout: post
title: `!p snip.rv = get_markdown_title(snip)`
date: `!v strftime("%Y-%m-%d %H:%M:%S")`
author: `!v g:snips_author`
tags: 
description: ${3}
categories: Docs
photos:  
toc: true

---

${0}
endsnippet
```

`get_markdown_title`是需要根据当前位置的上下文片段来确定的, 所以我们在处理代码片段中的这部分时, 返回了一个js函数,
详细信息请查看[script_tpl.ts][2].

```javascript
function get_markdown_title() {
  return jsFuncDecorator("js_markdown_title");  // `!js js_markdown_title`
}
```
而`js_markdown_title`也对应了一个函数:

```javascript
function js_markdown_title(vsContext: VSnipContext) {
  let fn = vsContext.document.fileName;
  return path.basename(fn, path.extname(fn));
}
```

VsnipContext 是对 VSCode api 的一层封装, 的具体定义请查看 [vsnip_context][3].

[1]: https://github.com/corvofeng/Vsnips/blob/master/src/generate.ts
[2]: https://github.com/corvofeng/Vsnips/blob/master/src/script_tpl.ts
[3]: https://github.com/corvofeng/Vsnips/blob/master/src/vsnip_context.ts
