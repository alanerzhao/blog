title: 一个月了，javascript学习总结
tags:
  - 总结，javascript
id: 150
categories:
  - Front-end
  - HTML/CSS
  - JavaScript
date: 2012-08-06 15:00:31
---

来北京一个月了，学习JavaScript也一个多月了，从刚开始在家里规划到现在，感觉自己没什么太大的变化，为什么这么说，买了N多本书，基本 每一本都没怎么看，一直再看的就是《javascript高级程序设计》，这书感觉甚好，讲的非常细，对没基础的我帮助很大，以前看书都是看一下感觉就会 了，现在则不然， 基本每天不熟悉的都会翻回来再看看，这样印象更深刻。

不过虽然没啥大的进步，总体而言也写了一些小的东西，一些小的效 果，主要是把我的笨的脑袋开发一下吧，我的逻辑能力太差，所以做东西非常苦恼，经常是半夜三更的从而在电脑前面，不知道怎么写，头发都掉了好多，唉，现在 发现了以前没有好好学习数学和英语的下场了。真的，如果你想搞互联网或者计算机，如果你不把数学和英语学好，那么你学起新东西来真的很难，因为好些东西都 是国外的，你要学习新的东西，毕业要去国外看英文，我一开始不信，不过后来我真信了，为什么这么说，国内所解决的好多前端兼容问题，其实大部分都是来自国 外的，只不过把英文变成了中文而以，但有些国人翻译的不是太好，导致了新手一直不理解，这也是有些东西你会写但不知道原因的问题所在。

下个 月的规划，也就是这个月的规划，争取能把JavaScript从头到尾都走一遍，这样大体对JavaScript又更深一步了解了，然后继续把基础巩固 好，继续提高逻辑，那么上个月我学会了什么？更多的是一些做效果的思路，如何去分析，如何去考虑，如何去扩展，如何做到兼容，这都是以后工作要做的，必须 要考虑全面，扩展做好，这样以后做的东西，才不会被XX说：你这XX不行。

<!--more-->下面是一些吐槽:

具体学会了什么？ 一些调试JavaScript的方法，主要是控制台Console的一些方法，要比我以前用的alert方法强很多，特别是用到setTimeout、setInterval的时候，用这个太好用了，都可以在控制台来看，控制台语句

[js]
console.log();
console.time('start time'); //检测时间
console.timeEnd('start time');
console.profile(); 性能
console.profileEnd()性能结束
console.warn('这里是警告')
console.error('这里是错误')
console.group('第一组')
console.groupEnd()
console.dir(对象) //显示所有的信息
console.dirxml(odiv) //显示当前元素的结构
console.assert(a) //断言
console.trace() //走向[/js]

这 里不过多介绍，要想学习控制台的话，去看一下阮一峰或者“Google　Firefox Console” 都有好多的教程，学好了这个也是一门手艺。

事件学习了onmouseover、onmouseout、onfocus、 onblur、onclick、onscroll、onresize、onkeydown等等一些的常用方法。

常用的数据类型number、string、 boolean、undefined、object、function，一些数据转换parseInt，parseFloat，Number，还有 isNaN，还有一些重要的隐式转换。

数组和字符串做为最基本也是最常用的东西被我练了又练，终于分清楚了
<div>[js]添加
push(元素)，从尾部添加
unshift(元素)，从头部添加
删除
pop()，从尾部弹出
shift()，从头部弹出
splice(开始, 长度,元素…)
先删除，后插入
删除
splice(开始,长度)
插入
splice(开始, 0, 元素…)
替换
[/js]

</div>
字符串更不用多说，

[js]charAt ——获取指定位置的字符
charCodeAt——获取指定位置字符的编码
fromCharCode——把编码转换成字 符
indexOf——从前往后查找指定的子字符串
lastIndexOf——从后向前查找指定的子字符串
substring——截取字符串
split——切分成数组
toUpperCase——转成大写
toLowerCase——转成小写[/js]

input框默认就是string的所以有时间也要做转换，其间还学到了自定义属性，灰常好用，可以做一些关联用。

DOM感觉也学了个一些，DOM存在的兼容问题其实挺多的，不过还好用一些封装函数可以很好的解决掉。主要用到的就那几个吧，这里列举一下:

[js]
childNodes\children——所有子节点，所有子元素节点
firstChild \ firstElementChild——第一个子节点，第一个元素子节点
lastChild \ lastElementChild——最后一个子节点，最后一个元素子节点
nextSibling \ nextElementSibling——下一个兄弟节点，下一个元素兄弟节点
previousSibling \ previousElementSibling——上一个兄弟节点，上一个元素兄弟节点
parentNode——父元素节点
获取：getAttribute(名称)
设置：setAttribute(名称, 值)
删除：removeAttribute(名称)
创建DOM元素
createElement(标签名) 创建一个节点
appendChild(节点) 追加一个节点
插入元素
insertBefore(节点, 原有节点) 在已有元素前插入
删除DOM元素
removeChild(节点) 删除一个节点
替换DOM元素
replaceChild(节点, 已有节点) 替换节点[/js]

当前书上还写好多不过大体没用上。
还有一些区域问题

[js]窗口尺寸、工作区尺寸
可视区尺寸
document.documentElement.clientWidth
document.documentElement.clientHeight

滚动距离
document.body.scrollTop
document.documentElement.scrollTop

内容高度
scrollHeight

文档高度
document.body.offsetHeight[/js]

BOM我没有仔细去研究，感觉用处不是很大，当然如果以后做项目用到还是得回头看看把BOM抓起来。

网上的收获也不少，认识了一位百度的前端工程师，不过这位师傅的教学条件让我没办法继续，他必须要我拿东西换，我又没什么好东西怎么换，所以就在人家那里求学了一次，不过这一次让我受益匪浅。以后多找点东西和他交换。

这篇文章算做笔记，做记录吧，别的没什么了，呵呵，随时更新！