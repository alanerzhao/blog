title: handlebars入门教程
tags:
  - handlebars
  - javascript
  - 前端模板
id: 239
categories:
  - Front-end
  - JavaScript
date: 2012-11-16 15:55:26
---

最近，学习了一下前端的模板引擎，一方面是自己以前自己知道的这些东西，另一方面是公司正好要重构时可能用到，所以让我来学一下，顺便总结个文档，然后分享给大家。前端模板有很多，这个也不过多讨论了，因为我选择了**handlebars.js**做为模板引擎，从互联网资源来说，相关中文文档还比较少，我对我的英语水平非常之了解，所以翻译了几篇国外的文章还是官方主页的文档，夹杂着一些自己的想法。如果有感觉想吐的，就看原文吧。还有要注意的是这篇还算文章算个文档吧，因为是从我的github上拿过来的，而些这文章我是第一次采用markdown来编写的可能存在阅读困难，所以如果想仔细阅读的话请去我的github上吧。

附送地址：[http://www.github.com/alanerzhao/doc](https://github.com/alanerzhao/doc)

## **介绍**

**Handlebars**是JavaScript一个语义模板库，通过对**view**和**data**的分离来快速构建Web模板。它采用"**Logic-less template**"（无逻辑模版）的思路，在加载时被预编译，而不是到了客户端执行到代码时再去编译，这样可以保证模板加载和运行的速度。**Handlebars**兼容Mustache，你可以在**Handlebars**中导入**Mustache**模板。

<!--more-->

**Handlebars**的安装非常简单，你只需要从Github下载最新版本，你也可访问下面网址获取最新信息：http://handlebarsjs.com/。

目前handlebars.js已经被许多项目广泛使用了，**handlebars**是一个纯JS库，因此你可以像使用其他JS脚本一样用script标签来包含handlebars.js

    &lt;script type="text/javascript" src=".js/handlebars.js"&gt;&lt;/script&gt;
    `</pre>

    ## **基本语法**

    **Handlebars expressions** 是**handlebars**模板中最基本的单元，使用方法是加两个花括号{{value}}, **handlebars**模板会自动匹配相应的数值，对象甚至是函数。例如：

    <pre>`&lt;div class="demo"&gt;
        &lt;h1&gt;{{name}}&lt;/h1&gt;
        &lt;p&gt;{{content}}&lt;/p&gt;
    &lt;/div&gt;
    `</pre>

    你可以单独建立一个模板,ID（或者class）和type很重要，因为你要用他们来获取模板内容，例如：

    <pre>`&lt;script id="tpl" type="text/x-handlebars-template"&gt;
        &lt;div class="demo"&gt;
            &lt;h1&gt;{{title}}&lt;/h1&gt;
            &lt;p&gt;{{content.title}}&lt;/p&gt;
        &lt;/div&gt;
    &lt;/script&gt;
    `</pre>

    你也可以定义一个模板变量例如：

    <pre>`var tpl = "&lt;p&gt;Hello, my name is {{name}}. I am from {{hometown}}. I have " +
                 "{{kids.length}} kids:&lt;/p&gt;" +
                 "&lt;ul&gt;{{#kids}}&lt;li&gt;{{name}} is {{age}}&lt;/li&gt;{{/kids}}&lt;/ul&gt;";
    `</pre>

    handlebars会根据上下文来自动对表达式进行匹配，如果匹配项是个变量，则会输出变量的值，如果匹配项是个函数，则函数会被调用。如果没找到匹配项，则没有输出。表达式也支持点操作符，因此你可以使用{{content.title}}这样的形式来调用嵌套的值或者方法，handlebars会根据当前上下文输出content变量的title属性的值。

    在JavaScript中，使用`Handlebars.compile()`方法来预编译模板，例如：(这是一套规则)

    <pre>`//用jquery获取模板
    var tpl   =  $("#tpl").html();
    //原生方法
    var source = document.getElementById('#tpl').innerHTML;
    //预编译模板
    var template = Handlebars.compile(source);
    //模拟json数据
    var context = { name: "zhaoshuai", content: "learn Handlebars"};
    //匹配json内容
    var html = template(context);
    //输入模板
    $(body).html(html);
    `</pre>

    ## **Handlebar的表达式**

    **Block表达式**

    有时候当你需要对某条表达式进行更深入的操作时，Blocks就派上用场了，在Handlebars中，你可以在表达式后面跟随一个#号来表示Blocks，然后通过{{/表达式}}来结束Blocks。如果当前的表达式是一个数组，则Handlebars会“自动展开数组”，并将Blocks的上下文设为数组中的项目，让我们来看看下面的例子，例如：

    <pre>`&lt;ul&gt;
    {{#programme}}
        &lt;li&gt;{{language}}&lt;/li&gt;
    {{/programme}}
    &lt;/ul&gt;
    `</pre>

    有以下json数据

    <pre>`{
      programme: [
        {language: "JavaScript"},
        {language: "HTML"},
        {language: "CSS"}
      ]
    }
    `</pre>

    编译模板代码同上……，上面的代码会自动匹配people数据并展开数据，渲染DOM后就是这样的

    <pre>`&lt;ul&gt;
      &lt;li&gt;JavaScript&lt;/li&gt;
      &lt;li&gt;HTML&lt;/li&gt;
      &lt;li&gt;CSS&lt;/li&gt;
    &lt;/ul&gt;
    `</pre>

    ## **Handlebars的内置块表达式（Block helper）**

    **1.each block helper**

    你可以使用内置的each helper遍历列表块内容，用this来引用遍历的元素，例如：

    <pre>`&lt;ul&gt;
        {{#each name}}
            &lt;li&gt;{{this}}&lt;/li&gt;
        {{/each}}
    &lt;/ul&gt;
    `</pre>

    对应适用的json数据

    <pre>`{
        name: ["html","css","javascript"]
    };
    `</pre>

    这里的this指的是数组里的每一项元素，和上面的Block很像，但原理是不一样的这里的name是数组，而内置的each就是为了遍历数组用的，更复杂的数据也同样适用，一定是数组就好。

    **2.if、else block helper**

    Handlebars提供了{{if}} helper 你可以指定条件渲染dom，如果它的参数返回false，undefined, null, "" 或者 [] (a "falsy" value),Handlebar将不会渲染DOM，如果存在{{else}}则执行{{else}}后面的渲染，例如：

    <pre>`{{#if list}}
    &lt;ul id="list"&gt;
        {{#each list}}
            &lt;li&gt;{{this}}&lt;/li&gt;
        {{/each}}
    &lt;/ul&gt;
    {{else}}
        &lt;p&gt;{{error}}&lt;/p&gt;
    {{/if}}
    `</pre>

    对应适用json数据

    <pre>`var data = {
        info:['HTML5','CSS3',"WebGL"],
        "error":"数据取出错误"
    }
    `</pre>

    这里{{if}}判断是否存在list数组，如果存在则遍历list，如果不存在输出错误信息

    **3.unless block helper**

    这个表达式是反向的if语法也就是当判断的值为false时他会渲染DOM，例如：

    <pre>`{{#unless data}}
    &lt;ul id="list"&gt;
        {{#each list}}
            &lt;li&gt;{{this}}&lt;/li&gt;
        {{/each}}
    &lt;/ul&gt;
    {{else}}
        &lt;p&gt;{{error}}&lt;/p&gt;
    {{/unless}}
    `</pre>

    **4.with block helper**

    一般情况下，Handlebars模板会在编译的阶段的时候进行context传递和赋值。使用with的方法，我们可以将context转移到数据的一个section里面（如果你的数据包含section）。这个方法在操作复杂的template时候非常有用。

    <pre>`&lt;div class="entry"&gt;
      &lt;h1&gt;{{title}}&lt;/h1&gt;
      {{#with author}}
      &lt;h2&gt;By {{firstName}} {{lastName}}&lt;/h2&gt;
      {{/with}}
    &lt;/div&gt;
    `</pre>

    对应适用json数据

    {

    title: "My first post!",

    author: {

    firstName: "Charles",

    lastName: "Jolley"

    }

    }

    ## **Handlebar的注释**

    Handlebars也可以使用注释写法如下

    <pre>`{{! 这里是Handlebars的注释格式 }}
    `</pre>

    ## **Handlebars Path**

    Handlebar支持路径和mustache,Handlebar还支持嵌套的路径，使得能够查找嵌套低于当前s上下文的属性可以通过"."来访问属性也可以使用"../",来访问父级属性。例如:（使用.访问的例子）

    <pre>`&lt;h1&gt;{{author.id}}&lt;/h1&gt;
    `</pre>

    对应json数据

    <pre>` {
      title: "My First Blog Post!",
      author: {
        id: 47,
        name: "Yehuda Katz"
      },
      body: "My first post. Wheeeee!"
      };
    `</pre>

    例如：（使用"../"访问）

    {{#with person}}

    # {{../company.name}}

    <pre>`    {{/with}}
    对应适用json数据
      {
                "person":
                { "name": "Alan" },
                    company:
                {"name": "Rad, Inc." }
            };
    `</pre>

    ## **自定义helper**

    Handlebars，可以从任何上下文可以访问在一个模板，你可以使用"Handlebars.registerHelper"方法来注册一个helper。有两种类型的帮手，你可以使 Function helper 和block helper。

    **Function helper** 基本上都是定时功能，一旦注册，可以在你的模板中的任何地方。Handlebars写入到模板函数的返回值

    **block helper** 在本质上相似if each with 内置块助手，允许改变内容里的值它的辅助和辅助函数的名称作为registerHelper的参数

    Handlebars.js返回无论是从辅助功能，并将其写入的模板，所以一定要始终返回一个字符串，您的自定义helper。例如：

    <pre>`{{#person}}
        &lt;div&gt;Name: {{firstName}} {{lastName}}&lt;/div&gt;
        &lt;div&gt;Email: {{email}}&lt;/div&gt;
        &lt;div&gt;Phone: {{formatPhoneNumber phone}}&lt;/div&gt;
        {{/person}}

        var data = { person: {
            firstName: "Alan",
            lastName: "Johnson",
            email: "alan@test.com",
            phone: "123-456-7890"
          } };
        Handlebars.registerHelper("formatPhoneNumber", function(phoneNumber) {
          //return phoneNumber = phoneNumber.toString();
          return "(" + phoneNumber.substr(0,3) + ") " + phoneNumber.substr(3,3) + "-" + phoneNumber.substr(6,4);
        });
    var tpl = $("#text").html();
    var html = Handlebars.compile(tpl);
    $("body").html(html(data));
    `</pre>

    ## **子模板helper (Partials)**

    Handlebars.registerPartial()来注册子模板,当你想要复用模板的一部分，或者将长模板分割成为多个模板方便维护时，partials就派上用场了。直接看代码比较直接，母模板定义如下：其中用">partials" 来包含相应的子模板。注册一个partial。第一个参数是子模名字的字符串,第二个参数是已编译模板的名称，例如：

    <pre>` &lt;!--mother template--&gt;
        &lt;script id="mother-template" type="text/x-handlebars-template"&gt;
            &lt;div id="wrap"&gt;
                {{&gt; son}}
            &lt;/div&gt;
        &lt;/script&gt;
        &lt;!--son template--&gt;
        &lt;script id="son-template" type="text/x-handlebars-template"&gt;
            {{#son}}
            &lt;li&gt;{{name}} {{content}}&lt;/li&gt;
            {{/son}}
            &lt;/ul&gt;
        &lt;/script&gt;
    `</pre>

    对应适用json数据

    <pre>`var data = {
    son:[
        {name:"alanerzhao",content:"东西学多了就容易晕！"},
        {name:"zhao",content:"死了吧"}
        ]
    }
    //父模板
    var mother = $("#mother-template").html();
    var tpl = Handlebars.compile(mother);
    //子模板
    var son = $("#son-template").html();
    Handlebars.registerPartial("son",son);
    $("body").html(tpl(data))
    `</pre>

    ## **调试技巧**

    把下面一段"debug helper"加载到你的JavaScript代码里，然后在模板文件里通过"{{debug}} {{debug someValue}}"方便调试数据

    <pre>`Handlebars.registerHelper("debug", function(optionalValue) {
      console.log("Current Context");
      console.log("====================");
      console.log(this);
      if (optionalValue) {
        console.log("Value");
        console.log("====================");
        console.log(optionalValue);
      }
    });
    `</pre>

    ## **handlebars的jquery插件**

    <pre>`(function($) {
        var compiled = {};
        $.fn.handlebars = function(template, data) {
            if (template instanceof jQuery) {
                template = $(template).html();
            }
        compiled[template] = Handlebars.compile(template);
        this.html(compiled[template](data));
        };
    })(jQuery);
    $('#content').handlebars($('#template'), { name: "Alan" });
    