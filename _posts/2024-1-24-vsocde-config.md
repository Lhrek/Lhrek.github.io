---
layout:     post
title:      "Vscode 个人配置"
subtitle:   "vim in vscode"
date:       2024-01-24 13:27:00
author:     "GanZJ"
header-img: "img/bg-little-universe.jpg"
catalog: true
tags:
  - vscode
  - config
---



> 记录一些个人配置

## vscode快捷键

设置键盘快捷方式 `Ctrl+K Ctrl+S` ：

> 终端：向上重设终端大小   ` Ctrl + ↑`
>
> 终端：向下重设终端大小   ` Ctrl + ↓`
>
> 终端：向右重设终端大小   ` Ctrl + →`
>
> 终端：向左重设终端大小   ` Ctrl + ←`

`ctrl + ~` ： 切换到终端

`CTRL + 0` ：在左侧文件夹列表中选中文件

`ctrl + b` : 关闭/启用侧边栏

`ctrl + ↑/↓/←/→` ：设置终端大小（需在设置内配置快捷键）

vscode启用：`sticky`



## vim快捷键

`vib/vi(` : 选中括号内的内容

`viB/vi{` ：选中大括号中的内容

`via` : 选中函数参数

`gd` : 跳转定义 

`gh` ：查看vscode提示信息

**vim插件配置文件**

```json
    "vim.handleKeys": {
        "<C-a>": false,
        "<C-b>": false,
        "<C-c>": false,
        "<C-f>": false,
        "<C-y>": false,
        "<C-v>": false,
        "<C-w>": false,
        "<C-z>": false
    }, //取消vim中的部分键位映射，使用vscode的

   "vim.insertModeKeyBindings": [
    {
      "before": ["j", "j"],
      "after": ["<Esc>"]
    }
  ],  //jj 映射esc
```



## vimium c 浏览器拓展

`f` ：显示页面可跳转链接
`o` ：搜索，浏览器书签及调用搜索引擎
`v/c` : 光标模式和自由选择模式的切换
`d/u` : 向上向下翻半页 



## .vscode文件夹

**c_cpp_properties.json**

```json
{
    "configurations": [
        {
            "name": "Linux",
            "includePath": [
                "/usr/include/llvm-16/llvm/**",
                "/usr/include/**",
                "/usr/lib/llvm-16/include/**",
                "${workspaceFolder}/**"
            ],
            "defines": [],
            "compilerPath": "/usr/bin/clang++-16",
            "cStandard": "c99",
            "cppStandard": "c++17",
            "intelliSenseMode": "linux-clang-x64",
            // "compileCommands": "${workspaceFolder}/build/compile_commands.json",
            "configurationProvider": "ms-vscode.cmake-tools"
        }
    ],
    "version": 4
}
```



**launch.json**

```json
{
    // 使用 IntelliSense 了解相关属性。
    // 悬停以查看现有属性的描述。
    // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "(gdb) 启动",
            "type": "cppdbg",
            "request": "launch",
            "program": "/home/gzj/xxx/build/tool/xxx", //填写build后生成二进制文件的位置
            "args": [
				"xxxxxxxx",
                "--",
               "-std=c89"
            ], //填写测试代码位置
            "stopAtEntry": false,
            "cwd": "${fileDirname}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
            "preLaunchTask": "build_xxx",
            "setupCommands": [
                {
                    "description": "为 gdb 启用整齐打印",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                },
                {
                    "description": "将反汇编风格设置为 Intel",
                    "text": "-gdb-set disassembly-flavor intel",
                    "ignoreFailures": true
                }
            ]
        }
    ]
}
```



**tasks.json**

```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "build_xxx",
            "type": "shell",
            "command": "cd build;cmake .. -DLLVM_DIR=/usr/lib/llvm-16/lib/cmake/llvm -DClang_DIR=/usr/lib/llvm-16/lib/cmake/clang -DALLOW_A=ON -DCXX_CHECK=ON -DCMAKE_BUILD_TYPE=Debug;make -j8 ;",//VERBOSE=1
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ]
}
```