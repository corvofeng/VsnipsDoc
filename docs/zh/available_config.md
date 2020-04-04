这一部分主要介绍目前可用的 Vsnips 配置项.


## 存放代码片段的目录

> Vsnips.SnipsDir

用户可以添加自己的 UltiSnips 目录, 示例:

```
"Vsnips.SnipsDir": [
    "/home/corvo/.vim/UltiSnips"
],
```

## vimrc 文件位置

> Vsnips.VarFiles

vimrc 文件主要用户解析变量, 确保 VSCode 与 Vim 能够共用一套变量, 无其他任何作用, 示例:

```
"Vsnips.VarFiles": [
    "/home/corvo/.vimrc",
    "/home/corvo/.vim/common.vim",
],
```

## 在 VSCode 配置中增加自定义变量

> Vsnips.VScodeVars

用于在 VSCode 中单独设置一些变量, 此变量会覆盖 vimrc 中的变量, 示例:

```
"Vsnips.VScodeVars": {
    "project": "Vsnips",
},
```


## 是否启用自带的代码片段

> Vsnips.UseDefaultSnips

用户是否启用 Vsnips 使用自带的代码片段(默认为 true)

```
"Vsnips.UseDefaultSnips": true,
```

## 自定义的 JavaScript 函数位置

> Vsnips.UserScriptFiles

用户可能针对 Vsnips 创作了自己的 JavaScript 模板函数.

```
"Vsnips.UserScriptFiles": [
    "/home/corvo/.vim/UltiSnips/func.js"
],
```

## 日志级别

> Vsnips.LogLevel

用于调整 Vsnips 的日志级别(默认为 NO,不打印日志), 仅用于调试

可选参数有: "NO", "DEBUG", "INFO", "WARN", "ERROR"

## 是否支持 AutoTriger

> Vsnips.EnableAutoTrigger

是否在满足条件时立刻触发代码片段(默认为 false), 启用这一设置可能对 VSCode 性能有影响

```
"Vsnips.EnableAutoTrigger": false,
```

## 代码片段展示策略

> Vsnips.DisplayStrategy

展示当前可用的代码片段策略(默认为 ALL)

可选参数有: "ALL", "PREFIX"(表示根据前缀进行筛选)

## 代码片段触发键

> Vsnips.trigers

用户自定义的触发键

不推荐使用, 增加了触发键后, VSCode 原有的补全功能会失去
