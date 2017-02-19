title: ajax与jsonp的使用
tags:
  - ajax，javascript，jsonp
id: 159
categories:
  - Front-end
  - JavaScript
date: 2012-08-18 14:01:43
---

近期接触到了一些我比较喜欢的东西，，就是标题中提到的ajax（异步传输）与jsonp（跨域），ajax一直是我想研究的个小技术，可一直没有折腾明白，通过一个星期的学习，大体会使用了，但是在跨域方面还是没有深入研究，所以后来又学了jsonp，因为这个东西能跨域，其实所谓的跨域之不过是把json格式的内容请求过来，包含到了页面了，能过callback回调函数的方式来操作数据。几个前端框架貌似也都包含在了自己的库里面了。这里还要知到一下ajax的属性，方法，还有监控事件

[javascript]

open方法:

 1.数据提交方式
 2.数据提交的地址
 3.是否异步
 同步：同一时间做一件事情
 异步：同一时间做很多事情

 oAjax.open('get', 'users.txt', true);
 oAjax.send()  //send方法：发送数据
 readyState    //请求状态
 onreadystatechange   // 当请求状态反生改变的时候触发的事件
 status   //服务器(HTTP)状态(码)
 responseText   //返回的内容
 onreadystatechange  //事件
 readyState    //属性：请求状态[/javascript]

<!--more-->0    （未初始化）还没有调用open()方法
1    （载入）已调用send()方法，正在发送请求
2    （载入完成）send()方法完成，已收到全部响应内容
3    （解析）正在解析响应内容
4    （完成）响应内容解析完成，可以在客户端调用了

status属性：请求结果
这里不得不提一下的就是请求状态码status，它会返回一些请求状态码，这个大家应该非常熟悉，如404，302，等都属于它的返回值，如果不熟悉的话可以自行Google一下，这里不多说了，最重要的是记住200就可以了，还有一些需要注意的地方那就是
1.      缓存问题：url ? 后面加上随机数/时间戳 new Date().getTime()
2.     请求地址数据的构建
3.     中文乱码：encodeURI()
4.     ie6 : ActiveXObject('Microsoft.XMLHTTP');
5.    因为你请求的json是字符串，所有要用eval : 把字符串解析成js代码，但是eval再解析两边一开始出现“｛｝”的代码时会出会错误，
所以再使用前一定要在前面加上小括号

[javascript]

 var data = '{n:5}';
 var json = eval('('+data+')');[/javascript]

有人一直分不清ajax和jsonp，不过我的理解就是它只不过是和ajax封在一个函数里而以，如果使用了jsonp来做跨域，下面的代码不会执行,我就是这么简单的理解的。下面是这个封装的函数，大体思想和jQuery 类似吧。

[javascript]function ajax(method, url, data, fnSuc, charset) {
 if (!charset) {
 charset = 'utf-8'; //编码转换
 }
 if (method == 'jsonp') { //jsonp
 var oScript = document.createElement('script');
 if (data) {
 url += '?' + data;
 }
 oScript.src = url;
 oScript.charset = charset;
 fnSuc &amp;&amp; fnSuc();
 document.body.appendChild(oScript);
 return ;
 }
 var oAjax = null;
 if (window.XMLHttpRequest) {
 oAjax = new XMLHttpRequest();
 } else {
 oAjax = new ActiveXObject('Microsoft.XMLHTTP');  /IE
 }
 if (method == 'get') {
 url += '?' + data;
 }
 oAjax.open(method, url, true);
 if (method == 'get') {
 oAjax.send();
 } else {
 oAjax.setRequestHeader(&quot;Content-Type&quot;,&quot;application/x-www-form-urlencoded&quot;);  //请求头
 oAjax.send(data);
 }
 oAjax.onreadystatechange = function() {
 if (oAjax.readyState == 4) {
 if (oAjax.status == 200) {
 fnSuc &amp;&amp; fnSuc(oAjax.responseText);  //回调函数
 }
 }
 }
}[/javascript]

之前就一直喜欢研究豆瓣网，感觉豆瓣的技术非常强大，所以经常在上面泡小组和看书评，后来看到豆瓣有开发者API，我就又小看了一下，为了适应自己的好奇心，就用jsonp搞了一下豆瓣的数据，大体还是挺简单的，因为豆瓣大多都给出了指南，等有时间想拿豆瓣的一些API做一些实用的东西。现在还不太会利用豆瓣的那些数据。这里把我练习的demo贴出来，好无意义只是贴一下，只是把豆瓣的一些数据请求过来了，等有时间了再扩展一下吧。

[javascript]&lt;script type=&quot;text/javascript&quot; src=&quot;http://www.douban.com/js/api.js?v=2&quot;&gt;&lt;/script&gt;
 &lt;script type=&quot;text/javascript&quot; src=&quot;http://www.douban.com/js/api-parser.js?v=1&quot;&gt;&lt;/script&gt;
 DOUBAN.apikey = '042e21ac7f84b4bd0c8a65057e8e1e37';
 var list = document.getElementById('list');
 var content = document.getElementById('content');
 var getTitle = document.getElementsByTagName('h3')[0];
 var getTag = document.getElementById('tag');
 var getImg = document.getElementById('img');
 ajax('get','http://api.douban.com/people/alanerzhao','alt=json',function(str){});
 ajax('jsonp','http://api.douban.com/book/subject/6021440','alt=xd&amp;callback=c',function () {
 c = function(data){
 getTitle.innerHTML = data.title.$t;
 content.innerHTML = data.summary.$t;
 for (var i = 0; i &lt; data[&quot;db:tag&quot;].length; i++) {
 var info = document.createElement('span');
 info.className = 'tag';
 info.innerHTML = data[&quot;db:tag&quot;][i][&quot;@name&quot;];
 getTag.appendChild(info);
 };
 for (var i = 0; i &lt; data[&quot;db:attribute&quot;].length; i++) {
 var item = document.createElement('li');
 item.innerHTML = data[&quot;db:attribute&quot;][i].$t + data[&quot;db:attribute&quot;][i].name;
 list.appendChild(item);
 };
 getImg.src = data[&quot;link&quot;][2][&quot;@href&quot;];
 }
 })[/javascript]

其实这下能做好多东西了，找各种接口做一些瀑布流什么的，这次就总结到这里，又是一顿乱写……

打完收功~！