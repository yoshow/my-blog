---
layout: post
title:  "Visual Studio Code 配置"
date:   2017-03-06 20:00:00 +0800
categories: editor
tags: ["Editor","Visual Studio Code"]
---

我的配置

**设置**  

{% highlight json%}  
// 将设置放入此文件中以覆盖默认设置
{
    "workbench.activityBar.visible": true,
    "workbench.statusBar.visible": true,
    "workbench.colorTheme": "Monokai",
    "workbench.iconTheme": "vs-seti",
    // -------------------------------------
    // 编辑器配置
    // -------------------------------------
    // 控制在多少个字符后编辑器会自动换到下一行。将其设置为 0 则将打开视区宽度换行(自动换行)。将其设置为 -1 则将强制编辑器始终不换行。
    // "editor.wrappingColumn": 140
    // The number of spaces a tab is equal to. This setting is overriden based on the file contents when `editor.detectIndentation` is on.
    "editor.tabSize": 4,
    // -------------------------------------
    // Javascript 配置
    // -------------------------------------
    // 定义左大括号是否针对函数而放置在新的一行
    // "javascript.format.placeOpenBraceOnNewLineForFunctions": true,
    // 定义左大括号是否针对控制块而放置在新的一行
    // "javascript.format.placeOpenBraceOnNewLineForControlBlocks": true
    // Specifies the full path to the OmniSharp server.
    // -------------------------------------
    // C# 配置
    // -------------------------------------
    // "omnisharp.path": "D:\\dev\\OmniSharp\\omnisharp-win-x64-netcoreapp1.0\\OmniSharp.exe"
    // -------------------------------------
    // Python 配置
    // -------------------------------------
    // Format the document upon saving.
    "python.formatting.formatOnSave": true,
    // Arguments passed in. Each argument is a separate item in the array.
    "python.formatting.autopep8Args": [
        "--max-line-length=80",
        "--indent-size=4"
    ],
    "python.linting.pylintArgs": [
        "--include-naming-hint=n",
        "--disable=W0311",
        "--disable=W0223",
        "--disable=C0103",
        "--disable=E1101"
    ],
    
    // 剪裁尾随空格
    // "files.trimTrailingWhitespace": true,
    "files.exclude": {
        "**/.git": true,
        "**/.svn": true,
        "**/.hg": true,
        "**/.DS_Store": true,
        "*.py~": true,
        "*.pyc": true
    }
}
{% endhighlight %}  

**插件**
- EditorConfig for VS Code
- C/C++
- C#
- Python
- reStructuredText

**相关链接**  
[https://code.visualstudio.com/](https://code.visualstudio.com/)  
