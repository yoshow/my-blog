---
layout: post
title:  "Visual Studio Code 配置 ESLint 规则"
date: 2017-07-28 08:00:00 +0800
tags: ["Editor","Visual Studio Code","ESLint"]
--- 

#### 安装 ESLint 环境 ####   
{% highlight HTML %}
npm install -g eslint@3.19.0
{% endhighlight %}
注: 最新版 ESLint 4.0 版已发布, 但是目前大部分插件基于 3.0 版开发，所以此处安装版本为 3.19.0。

#### 安装 ESLint 常用插件 ####  
{% highlight HTML %}
npm install -g eslint-friendly-formatter eslint-plugin-standard eslint-plugin-promise eslint-plugin-html
{% endhighlight %}

#### Visual Sudio Code 安装 ESLint 插件 #### 

![ESLint 插件](/images/2017-07-28-visual-studio-code-eslint/A.png)

#### 配置 .eslintrc.js 文件 ####  

配置文件可以根据实际情况修改，大致内容如下:

{% highlight JavaScript %}  
// http://eslint.org/docs/user-guide/configuring
module.exports = {
  root: true,
  parser: 'babel-eslint',
  parserOptions: {
    sourceType: 'module'
  },
  env: {
    browser: true,
  },
  // https://github.com/feross/standard/blob/master/RULES.md#javascript-standard-style
  extends: 'standard',
  // required to lint *.vue files
  plugins: [
    'html', 'requirejs'
  ],
  // 全局配置
  'globals': {
    'define': false
  },
  // 自定义规则
  // 0 off 1 warn 2 error
  'rules': {
    // 分号结尾
    "semi": ["error", "always"],
    // 函数前空格
    'space-before-function-paren': 0,
    // 括号样式
    'brace-style': 0,
    // 未使用的变量
    'no-unused-vars': 1,
    // 空白的注释
    'spaced-comment': 0,
    // === 代替 ==
    'eqeqeq': 0,
    // 单引号字符
    'quotes': 0,
    // allow paren-less arrow functions
    'arrow-parens': 0,
    // allow async-await
    'generator-star-spacing': 0,
    // allow debugger during development
    'no-debugger': process.env.NODE_ENV === 'production' ? 2 : 0
  }
}
{% endhighlight %}

#### 错误提示效果 #### 

![ESLint 插件](/images/2017-07-28-visual-studio-code-eslint/B.png)

**相关链接**  
[ESLint 规则](http://eslint.org/docs/rules/)  