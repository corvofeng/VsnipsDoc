

```
ext install corvofeng.Vsnips
```

![](/img/vsnips.gif)

> It is under development, although I can't guarantee that
> all ultisnips functions can be used in vscode, I will try my best.
> Please feel free to give an issue or pull requests.


## UltiSnips

For details of Ultisnips, please refer [here][1].

![ultisnips](../img/ultisnips.gif).

It's easy to write an UltiSnips sippets, for example, in `Python`,
I usually use `import IPython; IPython.embed()` for debugging.
And you could write snippts like this:

```snippets
# Atention, this code must be put in python.snippets for `Python` code.
snippet dbg "Use IPython to debug"
# ---------- XXX: Can't GIT add [START] ---------- #
import IPython
IPython.embed(using=False)
# ---------- XXX: Can't GIT add  [END]  ---------- #
endsnippet
```

The UltiSnips snippet bej  `snippet`, end with `endsnippets`

The whole snippst is surrounded with `snippet` and `endsnippets`,
while the `dbg` is the triger, and `"Use IPython to debug"` is
description for this snippet. At my vim:

![3][3]

## VScode snippets

In VScode, there is an origin [snippets syntax][4] to manage your own snippets. But I found it may not very easy to use:

1. If there is a multi-line snippet, `json` is not very well for storing.
2. It's hard for many PC sync the snippets. Because of this, there have been too many snippets extensions for different languages, like, [C/C++ Snippets][5], [Bootstrap 3 Snippets][6].

I do not mean that it's bad for different language having their own extension.
But you must admit that if you wanna add snippets for a language,
you need to learn how to write an extension and how to add snippets.
and what's most important is that if you are an Vimer, you had to
write snippets for these two editors, which bothers me.


## How to use Vsnips

> This plugin base on the [snippet api][8] in VScode, weather
> you have used UltiSnips or not, it's easy to start.
> I have adapted some UltiSnips snippets to VScode and used it by default.

If you have already use UltiSnips, and even have your own snippets,
you can add own snippets dir in settings, and use the variable in `VarFiles`
after set that.

```json
{
    "Vsnips.VarFiles": [
        "/home/corvo/.vimrc",
        "/home/corvo/.vim/common.vim",
    ],
    "Vsnips.SnipsDir": [
        "/home/corvo/.vim/UltiSnips"
    ]
}
```

When you give the variable like `let g:snips_author="corvo"`, you could
use it like snippets below.

```snippets
snippet full_title "Python title fully"
#!/usr/bin/env python
# -*- coding: utf-8 -*-
# vim: ts=4 sw=4 tw=99 et:

"""
@Date   : `!v strftime("%B %d, %Y")`
@Author : `!v g:snips_author`

"""

endsnippet
```

## Have done

* [x] Multi language completions support after installing
* [x] Allow user add their own Ultisnips.
    * [x] From Ultisnips to VScode snippets.
    * [x] Support strftime
    * [x] Allow user define variables
    * [x] Allow some functions(Rewrite by javascript)
* [x] Syntax highlight for snippets
* [x] Allow user define their own functions
* [x] Support autoDocstring(Python, TypeScript, Golang)
* [x] Support box command

## Doing

- [ ] Support extends and priority in Ultisnips
- [ ] Add support for golang function comments.

[1]: https://github.com/SirVer/ultisnips
[3]: https://user-images.githubusercontent.com/12025071/62412148-14cad280-b631-11e9-8d9c-01a65a2550ef.gif
[4]: https://code.visualstudio.com/docs/editor/userdefinedsnippets#_creating-your-own-snippets
[5]: https://marketplace.visualstudio.com/items?itemName=hars.CppSnippets
[6]: https://marketplace.visualstudio.com/items?itemName=wcwhitehead.bootstrap-3-snippets
[7]: https://user-images.githubusercontent.com/12025071/62412552-19928500-b637-11e9-8335-dfe3f0ca0688.gif
[8]: https://code.visualstudio.com/api/references/vscode-api#CompletionItemProvider
[9]: https://marketplace.visualstudio.com/items?itemName=njpwerner.autodocstring