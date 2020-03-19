---
layout: post
title:  "基于 Visual Studio Code 开发 TypeScript"
date: 2017-04-07 20:00:00 +0800
tags: ["Editor","Visual Studio Code","TypeScript"]
--- 

安装开发环境  
{% highlight HTML %}
npm install -g typescript
{% endhighlight %}

打开创建  
创建 tsconfig.json 

{% highlight JavaScript %}
{
  "compilerOptions": {
    // 编译之后生成的JavaScript文件需要遵循的标准。有三个候选项：es3、es5、es2015。
    "target": "es5",
    // 为 false 时，如果编译器无法根据变量的使用来判断类型时，将用any类型代替。
    // 为 true 时，将进行强类型检查，无法推断类型时，提示错误。
    "noImplicitAny": false,
    // 遵循的 JavaScript 模块规范。主要的候选项有：commonjs、AMD 和 es2015。
    "module": "commonjs",
    // 编译生成的 JavaScript 文件是否移除注释。
    "removeComments": false,
    // 编译时是否生成对应的source map文件。
    "sourceMap": true
  }
}
{% endhighlight %}

创建 tasks.json

{% highlight JavaScript %}
{
    "version": "0.1.0", 
    "command": "tsc",
    "isShellCommand": true,
    "showOutput": "always",
    "args": ["-p", "."],
    "problemMatcher": "$tsc"
}
{% endhighlight %}

最后按下快捷键「Ctrl+Shift+B」，就可以看到 Visual Studio Code 编译 TypeScript, 并且输出对应的 JavaScript 档案：main.js。

**相关链接**  
[Editing TypeScript](https://code.visualstudio.com/docs/languages/typescript)  
[使用 Visual Studio Code 开发 TypeScript](http://www.cnblogs.com/clark159/p/4615031.html)