title: 利用jekyll 搭建github page博客
tags:
  - git，github， jekyll
id: 190
categories:
  - Front-end
  - linux
  - other
date: 2012-09-30 07:37:01
---

好久之前，见好多人都用这个搭建了自己的一个简洁博客，看起来灰常不错，事后我也一直想弄可由于时间原因，等各方面因素，一直没时间折腾，再加之我对git也不是很熟悉，现在放假了，准备自己折腾一下，其实一开实我挺想搞一个wiki来记录一些东西，也算是规划自己的学习，"vim+wiki+github"，这个任务又准备往后拖一拖了。

话说github page现在已经能够自动创建一个项目主页，但是我还是比较喜欢用git来控制，感觉很牛的样子，所以从网上一直在搜索相关文章，对github page的页面也简单的翻译了一下，网上文章不少所以自己，但感觉自己总结一下，也不错!！

最简单的方式是让github来帮助你搭建，点击github主页右下角的github pages来看看他的document文档，文档里面也详解介绍了github page 和 jekyll 是什么，这也不在啰嗦。

<!--more-->
创建个人主页

创建github上创建版一个名为username.github.com版本库(Create New Repo)，这个不用多说了吧，右上角的创建，创建完成以后，打开Admin页面，点击Auto Page Generator，这样其实，你只要一步一步往下点击选择自己喜欢的模板就可以生成出来一个名为username.github.com的博客，可以访问一下这个博客，username.github.com，这时候是你默认选择的模板。

然后就是在本地克隆刚才建立的username.github.com版本库，
[code]git clone https://github.com/username/username.github.com.git[/code]

克隆完成以后，默认会有隐藏的.git文件还有一些主题文件，这里不要把.git文件删除，只要把其实的文件删除就好，然后就可以自己定义一些页面了，可以先简单的定义一个index.html页面
[code]
$ cd username.github.com
$ touch index.html
$ gvim index.html (打开写一些内容进去，也可以是md后缀，因为github支持markdown文件)
[/code]

下面就可以提交看看是否成功了
[code]
$ git add index.html (追加到版本库)
$ git commit -am 'this is demo' (提交信息-a是所有更改)
$ git push origin master (推送到github，推送过程提示你输入帐号，密码，输入便可)
[/code]

然后你就可以访问username.github.com，是不是之前所有的模板都没了，只变成你刚才写的一些东西了，这就是最基本的原理了，这里可能需要等待10分钟。上面所述是创建一个个人主页，其实也可以创建项目主页。

创建个人项目主页

GitHub会为每个账号分配一个二级域名username.github.com作为用户的首页地址。实际上还可以为每个项目设置主页，项目主页也通过此二级域名进行访问，例如username.github.com/demo。

创建个人项目主页，其实和上面是一样的，只不过上面的分支是master，而个主页是gh-pages，所以推送的时候必须要推送到gh-pages，这里是需要注意的。剩下的就不多说了，只是创建的时候是创建的项目主页就好，推送的时候记得不要推送到master分支，而是推送到gh-pages分支

[code]$ git push origin gh-pages (项目主页分支)[/code]

下面就是要说到jekyll了，我其实没有怎么折腾jekyll，因为我是直接把别人的模板clone下来改了改，可能有些做的不对吧，但我是很喜欢，这个主题的，所以有兴趣的同学可以看看别人的，然后自己改改，不过要注意的是记得把一些配置文件改掉，这里
有详细的jekyll说明https://github.com/mojombo/jekyll。这里也不在详解介绍，原因还是一样的，你可以下载一套别人写好的模板到你本地，然后把模板里的配置都删除掉(包括.git)，然后把这些主题文件拷贝到你的username.github.com文件夹下，然后就再一次的
[code]
$ git add . (追加所有到版本库)
$ git commit -am 'temp' (提交信息-a是所有更改)
$ git push origin master (推送到github，推送过程提示你输入帐号，密码，输入便可)
[/code]

这样的话一个简单的jekyll+github page博客就出来了，要写博客的时候，在_post里新建一个markdown文件，文件名和文件里面的头部信息（学名叫YAML front matter）按照模板的格式改，编辑好内容后，再依次执行上面三条命令，这个是最简单的，还有好多东西要后续的去处理。
这里推荐几篇文章大家有兴趣去看一下。

[Github Pages极简教程]( http://chen.yanping.me/cn/blog/2012/03/18/github-pages-step-by-step/)
[像黑客一样写博客——Jekyll入门 ](http://www.soimort.org/tech-blog/2011/11/19/introduction-to-jekyll_zh.html)
[**PIZn**]( http://www.pizn.me/)