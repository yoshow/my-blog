基于 Github Pages 和 Jekyll 技术的日常记事本

__注：这里默认安装环境已具备Ruby、RubyGems环境。__

安装 Jekyll  
<code># gem install jekyll</code>

创建新的网站  
<code># jekyll new my-blog  
\# cd my-blog
</code>

启动测试服务器

切换到站点的根目录执行如下命令  
<code># jekyll serve</code>

访问 http://localhost:4000 可以查看测试内容

#### 结合 Github Pages 使用 Jekyll ####  
进入GitRepo目录，键入git init命令，初始化一个git库。  
<code># cd /Users/yoshow/</code> 
将刚才在 Github 中创建的 Repo 克隆到你本地的Git库中，即刚在本地创建的 GitRepo 目录中。  
<code>git clone https://github.com/yoshow/my-blog</code>

在yoshow文件中会看到名为 my-blog 的文件夹，这就是你从 Github 中克隆的Repo文件。
Hello World，进入Repo目录中，创建一个 HTML 文件，名为index，内容为 “Hello World”。
cd /Users/yoshow/my-blog
echo “Hello World” > index.html
将创建的index.html文件push到github中
cd /Users/yoshow/username.github.io
git add .
git commit -m “Hello World update”
git push
在浏览器中访问
http://username.github.io ，你将
会看到index.html文件中的内容，我们这里
会显示“Hello World”。至此，基于 Github Pages 功能的个人站点就算搭建好了。
在克隆到本地的Repo文件中，按照上述的 Jekyll 文件目录结构手动创建所需的文件资
源，并上传。由于Github本身完美支持 Jekyll，所以只要符合Jekyll的文件目录，
Github 就自动使用 Jekyll 解析形成页面。
至此，我们应该有了一定的理解，这里我再简单
梳理一下：
Jekyll可以将我们使用markdown写的文章按
照指定模板解析为html文件。
Github Pages可以充当我们的服务器，通过
username.github.io可以访问到我们上传的 html 页面。
Github Pages 完美支持Jekyll，所以不需要我们自己编写复杂的 html 页面，只要将 Jekyll 的目录结构上传至 Github 中，就可以通过 username.github.io 访问由Jekyll解析生
成的html页面，从而形成了个人网站。

基本配置参见官方配置文档。 不同的模板，在该文件中的配置项也不一样，因为我自己使用了大师设计的模板，配置了如下参数（部分）：

title：网站名称。
description：网站说明。
logo：网站logo。
disqus_shortname：disqus标示符。
search：是否运行搜索。
url：网站中一些资源文件使用的url地址。
encoding：编码。

配置 _config.yml 文件

markdown：md解析模板。
timezone：时区。

可以看一下_posts下的jekyll给的例子：
```
---
layout: post
title: "Welcome to Jekyll!"
date: 2014-01-27 21:57:11
categories: jekyll update
---
You'll find this post in your `_posts` directory - edit this post and re-build (or run with the `-w` switch) to see your changes! 
To add new posts, simply add a file in the `_posts` directory that follo
ws the convention: YYYY-MM-DD-name-of-post.ext.
Jekyll also offers powerful support
for code snippets:
{ % highlight ruby % }
def print_hi(name)
puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{ % endhighlight % }
Check out the [Jekyll docs][jekyll]
for more info on how to get the most
```
编写博文
out of Jekyll. File all bugs/featur
e requests at [Jekyll's GitHub repo]
[jekyll-gh].
[jekyll-gh]: https://github.com/mojombo/jekyll
[jekyll]: http://jekyllrb.com

可以看到在博文的最上方有被两个---包裹起来的
一段，这里就定义了文章的一些参数，更多参数
在FrontMatter和Variables获取，简单的只需要
关注几个就好：
title：文章的标题。
date：文章的日期。
categories：定义了文章所属的目录。
layout：文章所使用的模板名称。
tags：文章标签。
这里就写一个最简单的文章，只是用其中的两个
参数：layout，title，如下：
```
---
layout: mylayout
title: hello-jekyll
---
Hello jekyll!
```
将这个写完的文章保存为 “年-月-日-标
题.markdown”的名字形式，上传至Github中的
_posts文件中，Jekyll会自动解析生成该文章的
html页面。
注：文章的文件名不要使用中文，否则会出
现Bug。
如果想自己编写模板可以参见如何创建Jekyll模
板。 或者可以使用大师们设计好的模板。Jekyll
模板锦集。

个性域名
个人网站要有一个称心的域名，使用 username.github.io 实在不像话，所以我说一下如何配置个性域名。如何申请域名这里就不再累赘。
在 Github 中的 User Site Repo 根目录（即 Github 中 Jekyll 目录的根目录）下创建CNAME目录，内容为你的个性域名，格式为 www.yourdomain.com 即可。
然后在域名管理系统中解析域名，添加CNAME记录，服务器为username.github.io。等待一个多小时后，就可以使用自己的域名访问了。

**相关链接**
http://jekyllrb.com/
http://jekyllthemes.org/
http://www.thxopen.com/jekyll/2014/04/25/i-and-jekyll.html
