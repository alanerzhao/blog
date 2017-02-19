title: Fiddler 2的使用和总结
tags:
  - javascript
  - 前端工具
  - 抓包
  - 调试
id: 384
categories:
  - Front-end
  - HTML/CSS
  - JavaScript
date: 2013-03-02 16:47:27
---

又是好久没写博客了，看看自己的**Evernode**里好多的乱笔记又开始心烦了，整理控就是麻烦，以前年前一直在改一些前端的bug，所以使用一些合理的工具也是必然的，今天我就总结一下Fiddle的使用，方便自己以后看，因为一些技巧确实记不住，那我就写下来。
Fiddle相信都知道，网上文章也不少，大体讲的就是那些意思，本地映射修改文件，抓包，簒改数据等等，其实对于我来就只用到第一个，就是本地映射文件，来修改一些代码，然后运行看看效果怎么样。其实网站有好多视频教程还有好的文章，有时候对于我来说，就是都想看完，不过也没有必要了，差不多就行，太过追求技巧也没有啥用。安装就不多了，一直next下去，安装完成。
Firefox 需要手动设置代理，才能支持 Fiddler 支持。
**配置方式——主菜单：工具 -&gt; 选项 -&gt; 高级 -&gt; 网络 -&gt; 连接 -&gt; 设置...，选择手动设置代理，设置 HTTP 代理为：127.0.0.1，端口：8888**。
你可以下载一个 **AutoProxy **相信大家也不陌生吧，然后自己做一个小的代理，方便修改代理用。至于IE下你就不用管了，上来就能抓取到所有请求，chrome也是同理。默认下，Fiddler不会捕获HTTPS会话，需要你设置下, 打开**Fiddler Tool-&gt;Fiddler Options-&gt;HTTPS tab 选中checkbox, 弹出如下的对话框，点击"YES"**
<!--more-->
抓取请求：打开Fillder然后刷新要抓取的页面，Fiddler会自动抓取下来。

本地映射：打开**autoresponder**，有没有看到界面上有两个复选框？第一个的作用是开启或禁用自动重定向功能，我们就可以在下面添加重定向规则了。第二个复选框框勾上时，不影响那些没满足我们处理条件的请求，把**Enable automatic responses** 勾选上，还有**Unmatched requests passthroungh** 。然后，可以把需要映射本地的文件拖到**autoresponder**面板里也可以**add**过来（也就是左边栏里的请求文件可以拖过来），点击下方需要替换的本地方件，**save**一下，重新**CTRL+F5**刷新查看，就可以看到查看的更改了，可以把请求都拖到**composer**里查看请求的详情。

过查以通过在请求上右击选择“**unlock for Editing**”快捷是"**F2**"然后就可以修改**TextView **视图下的代码，然后再关闭“**unlock for Editing**”，同样，虽然这里不需要你映射本地文件，但你必须还是要打开映射“**Enable automatic responses** ”然后，刷新预览即可，其实是同理。如果遇到编码错误，按照提示encode便可以使用。

保存单个请求文件，**file--save--request--request body**
设置断点请求：我也是看了小坦克在博客园上的介绍摘录下来的，使用命令行**bpu **www.rankber.com，这样你请求的则会断点执行，在请求上会弹出一个stop的图标，然后可以通过右面的**Inspectors **来**choose response** 来更改请求返回值，例如可以映射一个本地的json文件过去。
<pre class="brush:[javascript]"> {
    "name":"baozi",
    "sex":"man",
    "age":"24" 

}</pre>
同理也可以把图片都替换掉的，那么如果不需要断点了，可以使用取消命令 bpuafter。

当然Fiddler中也能修改Response
第一种：打开Fiddler 点击**Rules-&gt; Automatic Breakpoint -&gt;After Response** (这种方法会中断所有的会话)
如何消除命令呢？ 点击**Rules-&gt; Automatic Breakpoint -&gt;Disabled**

Fiddler也可以查看统计，就在右边的 statistics面板，例如你请求了一个“http://www.rankber.com“，
然后把这些请求都按住shift选择上那么Fiddler会给你一个很好的统计例如
<pre class="brush:[php]">Request Count:   24
Unique Hosts:    2
Bytes Sent:      15,028           (headers:15,028; body:0)
Bytes Received:  56,374           (headers:7,863; body:48,511)

ACTUAL PERFORMANCE
--------------
Requests started at:       21:28:19.308
Responses completed at:    21:28:21.858
Sequence (clock) duration: 00:00:02.5500040
Aggregate Session duration:00:00:10.539
TCP/IP Connect duration:   2,021ms
HTTPS Handshake duration:  69ms

RESPONSE CODES
--------------
HTTP/200:     23
HTTP/404:     1

RESPONSE BYTES (by Content-Type)
--------------
application/javascript:    37,525
             ~headers~:    7,863
             text/html:    6,855
              text/css:    4,131</pre>
而且还可以点击下方的show chart来查看饼图，真的是很完美
Fiddler的左下角有一个命令行工具叫做QuickExec,允许你直接输入命令。
> 1.help 打开官方的使用页面介绍，所有的命令都会列出来> 
> 2.cls 清屏 (Ctrl+x 也可以清屏)> 
> 3.select 选择会话的命令> 
> 4.urlreplace xx 替换请求> 
> 5.?.png 用来选择png后缀的图片> 
> 6.bpu 截获request> 
> 7.bps 404 200 截获请求码> 
> 8.start 开启Fiddler> 
> 9.stop 关闭Fiddler> 
> 10.allbut javascript 过滤javascript> 
> 11.bold 加粗请求域名> 
> 12.ctrl+X 清除所有抓取数据> 
> 13.可以利用Fiddler2的decode来解压gzip的压缩> 
> 14.比较两个请求，可以选中两个文件，然后右击compare
我的使用总结就是这样的，还有一个小提示就是，**如果发现请求码为304的CSS可能没办法替换因为是缓存的，可以在firefox里清除一下缓存和cach**。