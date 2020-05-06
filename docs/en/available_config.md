# Available Configs

This section will introduce configuration items.

## The UltiSnips Dirs

> Vsnips.SnipsDir

Directories that user add their own UltiSnips. For example:

```
"Vsnips.SnipsDir": [
    "/home/corvo/.vim/UltiSnips"
],
```

## Vimrc File

> Vsnips.VarFiles

Vsnips use vimrc files to parse the variables which already defined in Vim config, which makes sure you can get the same value in VSCode. For example:

 示例:

```
"Vsnips.VarFiles": [
    "/home/corvo/.vimrc",
    "/home/corvo/.vim/common.vim",
],
```

## Variables In VSCode Config

> Vsnips.VScodeVars

Even if you provide vimrc files, Vsnips will use these variables, and these variables have higher priority. For example:

```
"Vsnips.VScodeVars": {
    "project": "Vsnips",
},
```

## Whether To Use Default Snips

> Vsnips.UseDefaultSnips

There are so many default snips, maybe someone only want to use his or her snips.
You can set this variable to false to disable the default snips.

```
"Vsnips.UseDefaultSnips": true,
```

## Self Defined JavaScript Funcs

> Vsnips.UserScriptFiles

User may create their own JavaScript template function, For example:

```
"Vsnips.UserScriptFiles": [
    "/home/corvo/.vim/UltiSnips/func.js"
],
```

## Log Level

> Vsnips.LogLevel

Adjust the vsnips' log level(default is 'NO'), only for debugging.

## AutoTriger

> Vsnips.EnableAutoTrigger

Please refer to [Issue-16](https://github.com/corvofeng/Vsnips/issues/16#issuecomment-583457611)

Enabling this configuration will complete as soon as it is triggered, and it will
affect the performance of VScode.

```
"Vsnips.EnableAutoTrigger": false,
```

## DisplayStrategy

> Vsnips.DisplayStrategy

Whether to dispaly all available snips.

'ALL' or 'PREFIX'

