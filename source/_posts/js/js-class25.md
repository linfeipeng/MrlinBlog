---
layout: post
title: "js-事件冒泡处理"
date: 2019-7-4 12:15
comments: true
tags: 
	- js
---

# Day25 - Event Capture, Propagation, Bubbling and Once

> 作者：©Mrlin(史密斯林)
> 简介：学习记录，用于记录在CSDN课程中的学习内容。
> 课程：[30天完成30个JS原生开发项目挑战视频教程](https://edu.csdn.net/course/detail/5776)。[JavaScript30](https://javascript30.com) 是 [Wes Bos](https://github.com/wesbos) 推出的一个 30 天挑战。项目免费提供了 30 个视频教程、30 个挑战的起始文档和 30 个挑战解决方案源代码。目的是帮助人们用纯 JavaScript 来写东西，不借助框架和库，也不使用编译器和引用。

## 效果如下


<iframe src="/assets/demo/js_learn/class25/index.html" width="100%" height="400" scrolling="auto"></iframe>

<!-- more -->

第25天的训练是学习DOM的事件机制，主要包括事件捕获，事件冒泡，单次执行事件。



## 源代码

[addEventListener参考文档](https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget/addEventListener)

```Javascript
 <script>
        let divs = document.querySelectorAll('div');
        let one = document.querySelector('.one');
        let two = document.querySelector('.two');
        let three = document.querySelector('.three');
        divs.forEach(div => div.addEventListener('click', logText, {
            once: true,
            capture: false
        }));

        // one.addEventListener('click', logText1, {
        //     // capture: true
        // });
        // two.addEventListener('click', logText2, {
        //     // capture: true
        // });
        // three.addEventListener('click', logText3, {
        //     capture: true
        // });

       
        function logText(e) {
            console.log(this.classList.value);
            // e.stopPropagation();
        }

        function logText1(e) {
            console.log(this.classList.value);
            // e.stopPropagation();
        }

        function logText2(e) {
            console.log(this.classList.value);
            // e.stopPropagation();
        }

        function logText3(e) {
            console.log(this.classList.value);
            e.stopPropagation();
        }
        
</script>
```
同时也看一下HTML的文档结构，对于事件机制的理解也很重要：

```html
<div class="one">
    <div class="two">
        <div class="three">
        </div>
    </div>
</div>
```
* `EventTarget.addEventListener('eventName',callback,option)`：元素的事件注册方法，接收三个参数，第一个参数为事件的名称（点击`click`、双击`dbclick`、改变`change`等），第二个参数是该事件的回调函数，也称为监听器，第三个参数为事件注册的选项对象，通常会包含两个配置项（是否事件捕获`capture`以及单次执行`once`事件，它们两个的默认值都是`false`）。
* 当我们点击`class="three"`的`div`的时候，我们也相当于同时点击了`class="two"`和`class="one"`。
* `e.stopPropagation();`是否停止冒泡，如果调用了这个方法，就不会触发父组建的方法。
