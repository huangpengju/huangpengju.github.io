---
layout: page
title: 样式指南
permalink: /styleguide/
image: 08.jpg
---

这里是一段文字，很长很长的………………………………………………………………………………………………………………………………………………

***

### 默认标题:

# 这是默认标题
## 这是默认标题
### 这是默认标题
#### 这是默认标题
##### 这是默认标题
###### 这是默认标题

{% highlight markdown %}
## 一级标题
### 二级标题
#### 三级标题
{% endhighlight %}

***

### 列表  

#### 有序列表示例:

1. 这是第一段话。
2. 这是第二段话。
3. 这是第三段话。
4. 这是第四段话。
5. 这是第五段话。

***

#### 无序列表示例:

* 这是第一段话。
* 这是第二段话。
* 这是第三段话。
* 这是第四段话。
* 这是第五段话。

{% highlight markdown %}
1. 订单列表项目 1
2. 订单列表项目 1

* 未排序列表项目 1
* 未排序列表项目 2
{% endhighlight %}

***

### 引用

> 这里是名言警句

***

### 语法 标记

{% highlight js %}
  $('.top').click(function () {
    $('html, body').stop().animate({ scrollTop: 0 }, 'slow', 'swing');
  });
  $(window).scroll(function () {
    if ($(this).scrollTop() > $(window).height()) {
      $('.top').addClass("top-active");
    } else {
      $('.top').removeClass("top-active");
    };
  });
{% endhighlight %}

***

### 视频

<iframe src="https://haokan.baidu.com/v?vid=8116644409163308989&" frameborder="0" allowfullscreen></iframe>
    
***

### 图片

![]({{site.baseurl}}/images/09.jpg)
*Backyard*

***