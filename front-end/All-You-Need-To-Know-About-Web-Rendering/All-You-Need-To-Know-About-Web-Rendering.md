---
layout:		post
title:		'All-You-Need-To-Know-About-Web-Rendering?'
excerpt:	'This practice is rather useful during the front-end development because, as you can understand, markup, styles and scripts are very important for that so you are ought to know some lifehacks.'
categories:	['translation']
tags:		['Web', 'DOM']
---

# All You Need to Know About Web Rendering
# 关于网页渲染你所需要知道的一些内容

Hi there! Today I want to highlight the topic of web rendering. I’m pretty sure that there are a lot of articles about that but most of them are so different … so let’s get it all together.

大家好！今天我想强调一下关于网页渲染的话题。我敢说现在肯定有很多关于网页渲染的文章，不过这些文章中大多数都不尽相同，所以让我们把这些内容理清楚来吧。

This practice is rather useful during the front-end development because, as you can understand, markup, styles and scripts are very important for that so you are ought to know some lifehacks.

这个实践对前端工程师来说是非常有用的，因为就像你明白标记语言、样式和脚本对前端来说非常重要一样，所以你应该知道一些关于网页渲染的技巧。

This article is not aimed at describing the accurate mechanics of work browsers, but rather on understanding its general principles. By the way, different browsers have different algorithms so we can’t be sure to collect all of them.

这篇文章的目的不是去描述浏览器的具体工作原理，而是去理解它的一些基本原则。顺便说一下，对于不同的浏览器有不同的算法，所以我们不能确保能收集到所以的技巧。

## The Rendering Process
## 渲染的过程

So let’s consider the sequence of browsers work step by step:
让我们一步一步的来思考浏览器的工作顺序：

- Building DOM (Document Object Model) from received HTML.
- Downloading and detecting styles, which formed by CSSOM (CSS Object Model).
- Building the **render tree** based on both DOM and CSSOM (Webkit names it as «renderer» or «render object», Gecko — «frame»). It doubles DOM but doesn’t show hidden elements like `<head>` or those who have display:none; style. Each line of text should be defined as different renderer. Each render object contains of it’s DOM object and it’s set style. So render tree describes the DOM visually.
- For each render tree element, calculated the position on the page — building layout. Browsers use method (flow), which in most cases enough only one pass for all elements (more passes required for tables).
- Painting all stuff in the browser.

- 基于接收到的 HML 来构建 DOM （文档对象模型）。
- 下载并根据 CSSOM （CSS 对象模型） 来检测样式。
- 基于 DOM 和 CSSOM （Webkit 叫渲染器或渲染对象，Gecko 称之为框架结构）构建**渲染树**。不过它并不会显示类似 `<head>` 或这样式含有 `display: none;` 的这些隐藏元素。每一行的文字都应该被定义为不同的渲染器。每个渲染对象包含各自的 DOM 对象并且设置样式。所以渲染树可视化的描述了 DOM 的结构。
- 对于每一个渲染树元素都会在页面上被计算出位置以构建布局。Browsers use method (flow), which in most cases enough only one pass for all elements (more passes required for tables).
- 在浏览器中绘制所有的元素。

During the interaction between user and page (by some of the scripts) this process can be done again.

在用户（或者一些脚本）与页面交互期间，这一过程可能会重复执行。

## Repaint
## 重绘

If object style was changed but it’s size and position weren’t changed (for example, background-color, border-color, visibility) then browser just paints this one again (it is also called **restyling**).

如果元素的样式（比如，`background-color`, `border-color`, `visibility`）被改变了，但是其大小和位置没有被改变，则浏览器只会单单重绘这个元素。

## Reflow
## 渲染

If the structure of our document was touched then browsers do reflow (or to **relayout**). The main occasions of this are:

如果文档的结构变动了，则浏览器会重新渲染整个页面。以下情况会发生重新渲染：

- DOM manipulations (resizing, removing, adding something).
- The text was changed.
- CSS properties were changed.
- New stylesheets were added or older are removed.
- Class attribute manipulations.
- Browser window changes: resizing, scrolling.
- Pseudo-class activation (for example, :hover).

- DOM 操作（改变大小、移动或增加元素）。
- 文字被改变。
- CSS 属性被改变。
- 添加了新的样式表或移除老的样式表。
- 元素的 class 的值被改变。
- 浏览器窗口发生改变：大小或滚动。
- 伪类被激活（比如 `:hover`）。

Usually, browsers try to localize repaint and reflow on the side of changed object. For example, if you change a size of absolute or fixed positioned object then it will affect only this object and it’s children, but if you edit another one with static position then the whole page would be reflowed.

One more interesting thing is that browser caches everything during the JavaScript execution and applies them after the second turn after the script ends.

Let’s discuss an example. This one will cause reflow and repaint only once and not more than it:

```
var $body = $('body');
$body.css('padding', '1px'); // reflow, repaint
$body.css('color', 'red'); // repaint
$body.css('margin', '2px'); // reflow, repaint
```

But, as described before, properties change will make a reflow. So we’re going to add only on call and get this:

```
var $body = $('body');
$body.css('padding', '1px');
$body.css('padding'); // forced reflow
$body.css('color', 'red');
$body.css('margin', '2px');
```

To sum up, we will get two reflows. So if you want to change any properties then try to collect all of them together in favour of performance (see an example [here](http://jsbin.com/duhah/2/edit)).

Sometimes we can’t avoid reflows. For example, we need to apply margin-left twice. The first one we’ll do without any animation (just set it to **100px**) and set it’s transition to \*50px on the second time. You can [see an example right now](http://jsbin.com/qutev/1/edit) but I still going to describe it here.

Let’s create a transition class:

```
.has-transition {
    -webkit-transition: margin-left 1s ease-out;
       -moz-transition: margin-left 1s ease-out;
         -o-transition: margin-left 1s ease-out;
            transition: margin-left 1s ease-out;
}
```

Then we will try to create what we need as follows:

```
var $targetElem = $('#targetElemId'); // our element which has a "has-transition" class // delete transition class
$targetElem.removeClass('has-transition'); // change the property thinking that transition is disabled because we have done it before
$targetElem.css('margin-left', 100); // set transition back
$targetElem.addClass('has-transition'); // change the property
$targetElem.css('margin-left', 50);
```

This solution won’t work as desired because browser caches and apply any changes only at the end of the script. Here we need a reflow. After using it our code should look like this (that will work):

```
// delete transition class
$(this).removeClass('has-transition'); // change the property
$(this).css('margin-left', 100); // we call a reflow. all changes made before were applied
$(this)[0].offsetHeight; // you can use any call here // set transition back
$(this).addClass('has-transition'); // change the property
$(this).css('margin-left', 50);

```
### Practical advice for optimization

Based on this and other articles about web-optimization we can collect the next rules for better front-end:

- Write valid HTML and CSS with charset definition. You’d better include all the styles in <head> and all scripts at the end of the `<body>`.

- Try to make css-selectors simpler (even if you use preprocessor). Less nesting is better. The effectiveness rank of selectors is as follows (the first is the fastest):

1. Identificator: `#id`
2. Class: `.class`
3. Tag: `div`
4. Neighbour selector: `a + i`
5. Children selector: `ul > li`
6. Universal selector: `*`
7. Attribute selector: `input[type=”text”]`
8. Pseudoelements and pseudoclasses: `a:hover`

Keep in mind that browsers look for selectors from right to left so you should put the most effective at the end:

```
div * {...} // bad
.list li {...} // bad
.list-item {...} // good
#list .list-item {...} // good
```

- Minimize any work with DOM. Cache all: properties, objects if you use them more than once. You can also use offline element (stores all the data in memory) if you work with hard operations.
- When using jQuery for elements choosing, see their recommendations for selector creation.
- It is better to use only a class attribute in DOM (as deep as it possible) when working with styles.
- Don’t animate those objects which don’t have absolute or fixed position. If it’s needed then change only transition property (used repaint) instead of margin (used reflow).
- You may disable difficult :hover during scrolling (with no-hover for example).

I suggest reading those article to learn more:

- [How browsers work](http://taligarsiel.com/Projects/howbrowserswork1.htm)
- [Rendering: repaint, reflow/relayout, restyle](http://www.phpied.com/rendering-repaint-reflowrelayout-restyle/)
