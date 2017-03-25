---
layout: post
title:  "Silverlight 全屏方法"
date:   2012-08-23 20:00:00 +0800
tags: ["Windows", "Silverlight"]
---

{% highlight C# %}
/// <summary>全屏按钮事件</summary>
/// <param name="sender"></param>
/// <param name="e"></param>
private void BtnFullScreen_Click(object sender, RoutedEventArgs e)
{
    Application.Current.Host.Content.IsFullScreen = 
        Application.Current.Host.Content.IsFullScreen ? false : true;
}
{% endhighlight %}

__(*)我在Silverlight 3.0 测试通过. 但是全屏后Silverlight会有一些问题, 比如控件位置会产生偏移, 输入框没法输入东西, 不知道是不是我设置的问题.__