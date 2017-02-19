title: VIM的Less配置总结
tags:
  - less，vim
id: 172
categories:
  - Front-end
  - other
date: 2012-08-22 08:23:42
---

Sublime的强大，我不想让我的Vim弱下来，所以加强了一些以前没有的CSS3 HTML5高亮、提示等，而且最重要的是我加上了LESS的高亮，感觉还不错，说是自己折腾的，其实大部分还是这里复制一点，那里复制一点，最后在改改修修的，就成了自己喜欢的那一种了。最近一直在看IBM的Deve也就是开发者社区，发展有许多好文章，所以大家也不妨去看看，别看年限很老了，技术还是很实用的所谓，温故而知新吗。

先说说LESS的配置吧，那先简单介绍一下LESS
LESS 为 Web 开发者带来了福音，它在 CSS 的语法基础之上，引入了变量，Mixin（混入），运算以及函数等功能，大大简化了 CSS 的编写，并且降低了 CSS 的维护成本，就像它的名称所说的那样，LESS 可以让我们用更少的代码做更多的事情. ——摘自IBM
如果想进一步学习Less的话，我这里也有几篇不错的文章
[LESS CSS 框架简介 ](http://www.ibm.com/developerworks/cn/web/1207_zhaoch_lesscss/index.html "LESS CSS 框架简介")
[LESS 官网](http://lesscss.rog "LESS")（需要翻墙）
[Sass](http://sass-lang.com "Sass")与其类似的框架
[LESS](http://lesscss.net "LESS中国")的国内官网

<!--more-->

那么如果你是从事前端，你又在使用Vim如果不配置它的话是不是感觉有些不爽呢，所以果断的查阅资料，我是从stackoverflow上找到答案，插件名称是[less-vim](https://github.com/groenewege/vim-less "LESS-VIM")，作者做了好多兼容处理，兼容了大部分插件，作者的主页有更详解的说明，如果有同学英文不是很好，或者看不懂，那我就简单的告诉你吧,其实就是简单的翻译，你大可不必看它说什么，只要按代码复制就可以。
首先安装[pathogen](http://www.vim.org/scripts/script.php?script_id=2332 "pathogen")插件，下载下来放到vimfiles里的autoload文件里，然后在_vimrc里加入一条
[javascript]call pathogen#infect()[/javascript]

然后就是把[vim-less](https://github.com/groenewege/vim-less/downloads "LESS-VIM")地址：插件下载下来，然后把ftdetect， ftplugin， indent， syntax文件夹复制出来，粘贴到你的vimfiles文件夹里替换一下
最后在你的_vimrc里加入一条（我当时加的时候不知道这条是什么意思，有人懂的话告诉我）

[javascript]nnoremap ,m :w &lt;BAR&gt; !lessc % &gt; %:t:r.css&lt;CR&gt;&lt;space&gt;[/javascript]

这样的话，再打开一个.less文件看一看？是不是有高亮了，就像作者的github上放的图一样？
作者还说了两个颜色插件，这里不在叙述了。
那么接下来是HTML5的高亮和自动提示了，其实再之前就已经有一些高亮了，不过不是很全，这个插件几乎连自定义属性都可以高亮，个人感觉还可以,[HTML5](https://github.com/othree/html5.vim "html5-vim").vim插件的主页还是在github，这个安装就不用多说了，还是down下来，粘贴到vimfiles里便可以了，没什么复制的地方，不过可以自定义设置把你需要高亮的设置一下
禁用事件处理程序属性的支持：

[javascript]let g:html5_event_handler_attributes_complete = 0[/javascript]

禁用RDFa属性的支持：

[javascript]let g:html5_rdfa_attributes_complete = 0[/javascript]

禁用微观数据的属性支持：

[javascript]let g:html5_microdata_attributes_complete = 0[/javascript]

禁用WAI -ARIA属性的支持：

[javascript]let g:html5_aria_attributes_complete = 0[/javascript]

安装成功，怎么样？新建一个html文件，打上几个section试试看？感觉还不错吧？

接下来是我比较喜欢的JavaScript文件高亮了，其实之前一直用一个叫JQuery的高亮插件，自我感觉不怎么样好多关键字都不能高亮，当然高手有高手的解决办法，低手也有低手的解决办法，那就是搜，这个插件呢也是在github上找到的，不过先提示一下，这个插件高亮JavaScript太多，所以有的可能看不习惯，如果不是很喜欢，那就放弃吧。

插件[vim-javascript-syntax](https://github.com/jelera/vim-javascript-syntax "vim-javascript-syntax")
至于安装方法，我就不多说了，只说一句同上，然后在vimrc里加一句

[javascript]au FileType javascript call JavaScriptFold()[/javascript]

可以不加，加上之后，它就会按照自己的风格来折行了，这个插件的作者还有套自己的vim-web-dev放在github上，想偷懒的同学，可以果断去下载。

这就是一些简单的配置，那么我的vim配置详解在我的github上，如果有童鞋喜欢我这款就拿走吧，大家一起分享[vimfiles](https://github.com/alanerzhao/vim "vimfiles")
更详解的配置信息我都在vimrc里写着呢，我的水平还是很差。希望能得到谅解。