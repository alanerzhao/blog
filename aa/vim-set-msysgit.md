title: vim配置msysgit
tags:
  - git
  - github
  - vim
id: 371
categories:
  - Front-end
  - HTML/CSS
  - JavaScript
  - linux
date: 2013-02-07 10:15:28
---

很久很久以前，我一直想把一个文本编辑器配置的像一个IDE一样，虽然它现在也很像IDE，但有些地方还是不够强大，但要比起谁操作更快，那就没得比了，我曾经在**vim.cn**的**google group**里问过vim如何配置svn，结果被好多大牛讽刺了，大多都是说，一个文本编辑器为啥要配置svn，所以我也不敢多问。但在看到回贴中有人貌似是配置了本地的git，所以我也尝试了一下，结果成功了，下面分享我的总结。

在配置之前当然就是下载git了，这里我选用的是msysgit，因为他有两种选择一个种是可视化，另一种是命令行，这也是配置的关键地方，这里要注意的是不要一路next而是要有选择的安装。在安装的时候一定要选择第二个“**run git from the windows command prompt**”也就是说：从Windows命令提示符下运行git或者第三个“**run git and included unix tools from the windows command prompt**”，因为第一个将不会安装windows命令符也就是cmd下运行，剩下的安装你可以自己考虑，如果需要在putty这种终端下使用或者使用SSH，则自己看相关说明了，一路next就好了。
<!--more-->
安装成功后第二部就下下载vim的git插件，在github上搜索关于vim的git插件，我搜到了两款，分别是**git-vim**，**git-fugitive**第二个插件的start是最高的，当然第一个也有不少人使用，我试用了第一种，但我现在用的是第二个插件，第一个插件虽然提供了语法高量，还有内部调用git的方法，但不够强大。至于这个插件的安装，就相当容易了，直接扔到vimfiles里面就可以了。网上还有好多插件管理插件等，这里不在去说起，我也不喜欢那种方式。这样基本的安装是成功了。

后面还有好多的配置，配置你的github托管配置等。请自行在gihub上查看如配置本地帐号信息等等，这里简单的提示几部，打开你的git,然后输入
<pre class="brush:[css]"> 
  git config --global user.name "youname"
  git config --global user.email "youemail"</pre>
然后你测试一下是否可以连接到**github**
<pre class="brush:[css]"> 
ssh -T git@github.com</pre>
然后你可以克隆一个库下来
<pre class="brush:[css]"> 
git clone https://github.com/motemen/git-vim.git</pre>
上面这些只是一些简单的配置，只是能让你用git至于详细的教程，下面资源中会给出。配置完毕后就试试你在vim下是否能够使用git吧，这里需要注意，git-fugitive并不是在所有目录都会在命令行提示，只在包含.git的目录文件才有效,可以看下官方文档，写的很清楚，不过是英文的，还是那句话没有人比我英语差。

那在vim的当前文件下的命令行里输入一个G试一下，是不是出来好多类似于git的命令，例如
**Gwrite **代表git里的git add也就是追加文件
**Git commit - m "update"** 这也就是git里的git commit -m "update" 代码注释
**Git push -u origin master** 这就是提交上传代码了

等好多的命令，其实就是利用vim调用git通过windows命令行而以。哈哈

## 关于git github的资源

[pro git 教程](http://http://git-scm.com/book/zh "pro git 教程")
[git权威指南](http://http://www.worldhello.net/ "git权威指南")
[git - 简易指南](http://http://rogerdudler.github.com/git-guide/index.zh.html)