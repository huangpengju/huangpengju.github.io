---
layout: post
title:  使用github pages搭建个人博客
date:   2023-03-08 17:00:35 +0800
image:  2023_03_08_github_pages/blog.jpg
tags:   用 Jekyll 搭建博客
---
## 一、环境准备
使用Github Pages搭建个人博客，一劳永逸，可以让我们更加专注于博客的撰写。博客的更新是通过将新建或改动的博客放在指定文件夹并推送到远程Github仓库来完成的，所以我们本地需要有Git环境，如果还没有安装Git，可以看下面的文章：

1. 安装Git
2. Git关联远程GitHub仓库

## 二、搭建博客

#### （一）新建仓库
以 __username.github.io__ 作为仓库名称。<br>
![]({{ site.baseurl }}/images/2023_03_08_github_pages/username.png)

#### （二）本地克隆
本地创建文件夹，用于存放远程仓库，打开所创建的文件夹，右键选择git bash here，表示在当前目录打开git bash程序，然后执行如下命令，将刚才创建的仓库克隆到本地：<br>
git clone git@github.com:huangpengju/huangpengju.github.io.git

#### （三）新建主页
在仓库文件夹下创建 __index.html__：
{% highlight ruby %}
<!DOCTYPE html>
<html>
	<head> </head>
	<body>
	<p>hello, my first page!</p>
	</body>
</html
{% endhighlight %}

#### （四）推送到远程仓库
在仓库文件夹下，右键选择git bash here，然后执行命令：
{% highlight markdown %}
git add .
git commit -m "add index.html"
git push origin master
{% endhighlight %}

#### （五）验证
成功push到远程仓库后，在浏览器地址栏输入 *__username.github.io__*，浏览器显示出如下界面：<br>
![]({{ site.baseurl }}/images/2023_03_08_github_pages/index.png)<br>
这表示通过Github Pages搭建个人博客成功了。

## 三、更换主题
上面裸奔的博客主页，跟原始人类一样，你一定不满意，我们穿越几千年文明，直接站在巨人的肩膀上，选一套主题吧。<br>
Github Pages基于Jekyll构建，Jekyll 可以帮助我们把纯文本转换为静态博客网站，实现一劳永逸。<br>

#### （一）下载主题
你可以在 <a href="http://jekyllthemes.org/page2/">JekyllThemes</a>  找到喜欢的主题，也可以在其他地方找。<br>
我选择的是<a href="https://github.com/artemsheludko/zolan">Zolan</a>
![]({{ site.baseurl }}/images/2023_03_08_github_pages/Zolan.png)Zolan是Jekyll的一个最小的博客主题。<br>
<a href="http://artemsheludko.com/zolan/"> __预览Zolan__ </a> | <a href="https://github.com/artemsheludko/zolan/archive/master.zip"> __下载Zolan__ </a><br>


下载后，首先将我们仓库文件夹下的文件清空，但是要保留.git文件夹：<br>
![]({{ site.baseurl }}/images/2023_03_08_github_pages/git.png)

然后将下载的主题压缩包解压到仓库文件夹下，结果如下：<br>
![]({{ site.baseurl }}/images/2023_03_08_github_pages/r_zolan.png)

访问 <a href="http://jekyllcn.com/docs/structure/">Jekyll-目录结构</a> 详细了解每个文件夹的功能：

{% highlight markdown %}
.
├── _config.yml
├── _drafts
|   ├── begin-with-the-crazy-ideas.textile
|   └── on-simplicity-in-technology.markdown
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts
|   ├── 2007-10-29-why-every-programmer-should-play-nethack.textile
|   └── 2009-04-26-barcamp-boston-4-roundup.textile
├── _site
├── .jekyll-metadata
└── index.html
{% endhighlight %}

#### （二）搭建Jekyll环境
只有主题文件是不够的，我们需要搭建Jekyll环境，通过遵循Jekyll的规范，让Jekyll帮助我们生成静态网站。

1.安装Ruby：点击查看→<a href="https://www.ruby-lang.org/zh_cn/documentation/installation/"> Ruby安装教程</a><br>
2.打开CMD，执行命令安装Jekyll：
{% highlight markdown %}
gem install jekyll
{% endhighlight %}

3.进入仓库文件夹（比如：在CMD中 cd C:\Users\Vcom\go\src\Blog\huangpengju.github.io），执行命令：
{% highlight markdown %}
bundle install
{% endhighlight %}
注意，必须进入仓库文件夹下再执行上述命令，否则会有如下提示，表示bundle找不到gemfile文件：<br>
![]({{ site.baseurl }}/images/2023_03_08_github_pages/error.png)<br>
Rails 3中引入Bundle来管理项目中的所有Gem依赖，该命令只能在一个含有Gemfile的目录下执行，bundle install 命令将尝试更新系统中已存在的gem包。更多参考：<a href="https://blog.csdn.net/huaishu/article/details/38778777">bundle install 命令</a>

4.启动Jekyll服务
{% highlight markdown %}
bundle exec jekyll serve
{% endhighlight %}
启动Jekyll服务时，可能会遇到如下错误：
{% highlight ruby %}
 Conversion error: Jekyll::Converters::Scss encountered an error
  while converting 'css/main.scss':
                    Invalid GBK character "\xE2" on line 10
jekyll 3.4.0 | Error:  Invalid GBK character "\xE2" on line 10
{% endhighlight %}
很明显，是编码问题，参考网上方法解决 Invalid GBK character "\xE2" 过程中的发现，找到D:\RailsInstaller\Ruby2.3.3\lib\ruby\gems\2.3.0\gems\sass-3.7.2\lib\sass.rb文件，在require后追加：
{% highlight ruby %}
Encoding.default_external = Encoding.find('utf-8')
{% endhighlight %}
然后重新启动Jekyll服务：bundle exec jekyll serve，看到如下打印，表示启动成功：
![]({{ site.baseurl }}/images/2023_03_08_github_pages/jekyll_serve.png)

5.验证<br>
用浏览器访问 __http://127.0.0.1:4000__，当你发现你的博客首页像是从一个原始人变成光鲜亮丽的现代人时，表示博客主题已经应用成功了。

6.推送到远程仓库<br>
做完上述操作后，由于还没有将修改提交到远程仓库，所以当你访问username.github.io时，你看到的还是一个光溜溜的原始人，执行以下命令完成进化吧皮卡丘：
{% highlight markdown %}
git add .
git commit -m "apply theme"
git push origin master
{% endhighlight %}
成功推送到远程仓库后，等待几分钟，访问username.github.io，OK，成功。<br>
这里的 *username* 指的是你的 *github登录身份*

## 四、发布博客
在仓库文件夹下，进入_posts目录，所有的文章都必须放在_posts文件夹下，访问 Jekyll-目录结构 详细了解每个文件夹的功能。

以markdown文档为例，按照如下格式创建md文件。
{% highlight markdown %}
yyyy-MM-dd-filename.md
{% endhighlight %}
![]({{ site.baseurl }}/images/2023_03_08_github_pages/post.png)<br>
完成后push到远程仓库，即可完成更新。

## 五、修改主题
尝试阅读下图中的各种文件，将网站的信息改成自己的，如果你对这套主题不太满意，并且具备web基础，可以动手修改。<br>
![]({{ site.baseurl }}/images/2023_03_08_github_pages/r_zolan.png)