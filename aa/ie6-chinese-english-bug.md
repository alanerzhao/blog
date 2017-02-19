title: ie 中英混排问题总结
tags:
  - ie6中英文混排
id: 356
categories:
  - Front-end
  - HTML/CSS
date: 2013-02-02 09:08:49
---

最近在改项目里的bug，其实挺无聊的，必定不是我写的，一些代码我都不想去看，不过为了适应工作，我必须要静下心来去改一些bug，从bug中去学习，以前一直以为自己已经掌握了一些所谓的ie bug，其实不然，如果真心去做一个大的网站，遇到的问题还是不少的，我想也总结果一套我自己遇到的bug并来记录修改这些bug所需要场景。今天就说一下ie 6中文英文混排的bug。
一般咱们做网站都会定义一个统一字体家族，那一般的视觉设计师和产品都是要我们都用“**宋体**”来做为共用字体英文字体一般是"**Arial**"，或许会有别的地方也用到“**微软雅黑**”等这样特殊的字体。那换做我们来做的时候一般是这样,当然这里是按照需求的变更，这里只是例举一下。
<!--more-->
<pre class="brush:[css]"> 
body {
 font: 12px/1.5 Arial,Helvetica,宋体,sans-serif;
}</pre>
因为字体是可继承的嘛，所以全局都通用了，这里面意思是12px大小字体，1.5倍的行高,首先是英文的arial字体，如果不支持则是Helvetica字体，依次往后下去，中文采用“宋体”。这里还需要提到的就是如果你这样定义了中文字体，那么如果你浏览器无论更改为什么你喜欢的字体，网页是无法改变的，因为你已经定死在客户端了，好处就是英文字体不会对中文字体造成影响，这样也就是说中文字体受浏览器的字体影响了。
记得看过张鑫旭的文章说过，最好不要定死字体，但这就看产品需求了，最好是做到自适应。也就说上面的定义的英文字体就按照“**arial,helvetica**”去渲染，而中文则按照“**宋体**”来渲染，这种情况下你想一想也可以猜的到，中英文行高是不一样的，这里又牵扯到**vertical-align**问题，为什么这么说？vertical-align有很多的属性比如说middle啊，baseline啊，top啊，还可以定义百分比等，我们知道middle是中线对齐，可想而知，英文的middle和中文的middle有可能相同么？
如果真理解这些属性，那么建议去看看张鑫旭的文章吧，这里不多说，那么如果你做类似于垂直居中等用到了这个属性，并且又是中英文的那么就有可能出现中文和英文不在一排上显示。那么为什么下面给一段demo代码做试验用，前题是你使用了**vertical-align**的**middle**属性
<pre class="brush:[html]"> 
<span>
   <input type="text" />
   <label style="vertical-align: middle;" for="">中文spanEmail</label>
</span></pre>
如果不出意料的话，是不是不是居中的？那就对了。费话不多说，上面已经解释的很清楚了，那么解决方案有两种。
第一种，**vertical-align:baseline**;
为什么能解决掉，因为中文或是英文的基线肯定是一样的。不用多说了吧？肯定是可行的。但问题在于，咱们的有时候需求是不同的，用baseline属性的应用场景大体是用在那种大篇文章里中英混篇时，不涉及一些文本input框对齐啊等常见的问题。那么如果我们要做input框与文字垂直对齐，是不是大家都习惯用vertical-align:middle？然后不IE6等浏览器在写一些hack，到现在为止，还没有谁给一个特别好的的解决方案是针对input框与文本垂直居中的方案呢吧，那这样的话，我们怎么解决中英文混排？
第二种，
<pre class="brush:[css]"> 
.ie6lh{_font_-family:\5b8b\4f53;_line-height:1.231;}</pre>
这是一个类定义一个字体和行高，为什么这样用？这样单儿加一个类其实就是在ie6下用宋体，然后用行高的方式对齐左边,这个类加在父级也可以用，加在label也可以用。
<pre class="brush:[css]">  
<span>
     <input style="vertical-align: middle;" type="text" />
     <label class="ie6lh" style="vertical-align: middle;" for="">中文spanEmail</label>
</span></pre>

## 推荐文章

[新浪UED对此的解读：](http://ued.sina.com.cn/?p=95 "新浪UED中英混排")
[字体对照表](http://lifesinger.googlecode.com/svn/trunk/lab/2009/web-default-font.html "中英文对照表")（看名字好像是玉伯大大的）