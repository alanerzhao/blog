title: 最近写的一个jQuery滚动插件
tags:
  - jQuery
  - jQuery插件
id: 307
categories:
  - Front-end
  - HTML/CSS
  - JavaScript
date: 2012-12-26 10:43:31
---

郁闷的事情总是发生在我的头上，真的很郁闷，唉!但我不能放弃，在这破公司，一切皆是插件，所以也要让我写，正好他们现在的项目中要用到，所以我也学习了jQuery插件的写法，然后写了这个插件。附上code，发这么长的代码，真信不适合放到博客上，不过这是我写的第一插件，还是记念一下吧。其实写jquery插件的话，最好理解面向对象的思想，否则的话，其实挺难写的，当然也没必要全部写成面向对象的思想，只不过这样看起来更清晰更通用些。

如果实在看不懂，或者感觉垃圾就算了，反正就我是写着玩，给个demo地址：
[http://www.rankber.com/lab/slideshow/slideshow.htm](http://www.rankber.com/lab/slideshow/slideshow.htm "slideshow")
下面介绍一下如何使用，首先你得加载一个jQuery库吧，这个不用多说。然后给出一个Examples用例
<pre class="brush:[javascript]"> 
$("#wrapper").Slider({ 
            "prev" : "prev",
            "next" : "next",
            "content" : "list",
            "sliderAuto" :false
       });
        /*
         * prev 代表的是左按钮
         * next 代表的是右按钮
         * content 代表的是滚动外层地元素一般都是div
         * sliderAuto 是否开启自动滚动
         * */</pre>
<!--more-->
<pre class="brush:[javascript]"> 
;(function($) {
	var defaults = {
        /*
         * 参数配置
         * sliderNum : 滚动数量
         * sliderEvent : 触发方式
         * sliderSpeed : 移动速度
         * sliderTime : 自动调用时间
         * sliderAuto : 是否自动滚动
         * */
		sliderNum: 5,
		sliderEvent: 'click',
		sliderSpeed: "slow",
		sliderTime: 2000,
		sliderAuto: true,
        sliderWrap: "",
        sliderPath: "marginLeft"
	};
	function Slider(options) {
		this.options = $.extend({}, defaults, options);
		/*
         * this.prev : 上按钮
         * this.next : 下按钮
         * this.content : 移动块
         * this.wrap : 默认取到第二层
         * */
		this.prev = $("#" + this.options.prev);
		this.next = $("#" + this.options.next);
		this.content = $("#" + this.options.content);
        this.wrap = this.options.sliderWrap ? $("#" + this.options.sliderWrap) : this.content.parent().parent();
		/*
         * this.sliderWidth : 移动宽度
         * */
		var $item = this.content.find("li");
		this.len = $item.length;
		this.itemWidth = $item.eq(0).width();
		this.sliderWidth = this.options.sliderNum * this.content.find("li").eq(0).width();
		this.init();
	}
	Slider.prototype = {
		init: function() {
			this.bindEvent();
            //给定宽度
			this.content.width(this.len * this.itemWidth)
			//自动滚动
			this.options.sliderAuto ? this.sliderAuto() : false;
		},
		bindEvent : function() {
			var self = this,
			prev = this.prev,
			next = this.next,
			content = self.content,
			sliderWidth = self.sliderWidth
			sliderSpeed = this.options.sliderSpeed,
			sliderEvent = this.options.sliderEvent;
			//列表左移动
			prev.bind(sliderEvent, function() {
				if (!content.is(":animated")) {
					content.animate({
						"marginLeft": - sliderWidth
					}, sliderSpeed, function() {
						content.css({
							"marginLeft": 0
						}).find("li:lt(" + self.options.sliderNum + ")").appendTo(content);
					});
				}
			});
			//列表右移动
			next.bind(sliderEvent, function() {
				if (!content.is(":animated")) {
					var _index = content.find("li").length - self.options.sliderNum - 1;
					content.css({
						"marginLeft": - sliderWidth
					});
					content.find("li:gt(" + _index + ")").prependTo(content);
					content.animate({
						"marginLeft": 0
					},sliderSpeed);
				}
			});
		},
		sliderAuto : function() {
			var self = this,
			timer = null;
			this.wrap.hover(function() {
				clearInterval(timer);
			},
			function() {
				timer = setInterval(function() {
					if (!self.content.is(":animated")) {
						self.content.animate({
							"marginLeft": - self.sliderWidth
						},
						function() {
							self.content.css({
								"marginLeft": 0
							}).find("li:lt(" + self.options.sliderNum + ")").appendTo(self.content);
						});
					}
				},self.options.sliderTime)
			}).trigger("mouseleave")
		}
	}
	$.fn.Slider = function(options) {
		return this.each(function() {
			new Slider(options);
		})
	}
})(jQuery)</pre>
可能写的很垃圾，以后再慢慢修改，以后我会加上各种滚动吧，上下也可以最好了，呵呵 。