---
layout: post
title: "Console 调试各种姿势指南"
date: 2019-6-11 12:15
comments: true
tags: 
	- js
---

# Day09 - Console 调试各种姿势指南

> 作者：©Mrlin(史密斯林)
> 简介：学习记录，用于记录在CSDN课程中的学习内容。
> 课程：[30天完成30个JS原生开发项目挑战视频教程](https://edu.csdn.net/course/detail/5776)。[JavaScript30](https://javascript30.com) 是 [Wes Bos](https://github.com/wesbos) 推出的一个 30 天挑战。项目免费提供了 30 个视频教程、30 个挑战的起始文档和 30 个挑战解决方案源代码。目的是帮助人们用纯 JavaScript 来写东西，不借助框架和库，也不使用编译器和引用。


<!-- more -->
    
## 各种调试正确姿势

### `.log` 的更多用法

这个是最常用的，但它还有一些更多功能：比如参数支持类似 C 语言的字符串替换模式。

- `%s` 字符串
- `%d` 整数
- `%f` 浮点值
- `%o` Object
- `%c` 设定输出的样式，在之后的文字将按照第二个参数里的值进行显示

```js
console.log("I am a String: %s ", "log"); //log
console.log("I am a int number: %d ", 1); //1
console.log("I am a float number: %d ", 1.23); //1.23
let dog = {name: "Lucky",age: "5"};
console.log("%o",dog);
console.log("%c3D Text"," text-shadow: 0 1px 0 #ccc,0 2px 0 #c9c9c9,0 3px 0 #bbb,0 4px 0 #b9b9b9,0 5px 0 #aaa,0 6px 1px rgba(0,0,0,.1),0 0 5px rgba(0,0,0,.1),0 1px 3px rgba(0,0,0,.3),0 3px 5px rgba(0,0,0,.2),0 5px 10px rgba(0,0,0,.25),0 10px 10px rgba(0,0,0,.2),0 20px 20px rgba(0,0,0,.15);font-size:5em");
```

### 清空 console 面板输出内容

要清空已经打印输出的内容，有两种方式，一种是 JavaScript 语句： `console.clear()`。另一个是快捷键 `Ctrl ＋ L`。

### 不同样式的输出

除了常规的 `log` 之外，还有一些其他已设定好的样式，区别在于图标或者颜色不一样：

```js
// warning!
console.warn("用于输出警示信息");
// Error :|
console.error("用于输出错误信息");
// Info
console.info("用于输出提示性信息");
//debug
console.debug("用于输出调试信息");
```

### 打印DOM节点

获取 DOM 元素之后，可以直接打印输出。

```js
const p = document.querySelector('p');
console.log(p);
console.dir(p);
```

*  .log 输出这个 DOM 的 HTML 标签。

* .dir 则会输出这个 DOM 元素的属性列表。

### 断点调试

`console.asset(arg1,arg2)`方法接受一个表达式作为参数，如果参数返回值是`false`，则会输出第二个参数中的内容。


```js
const p = document.querySelector('p');
console.assert(p.classList.contains('ouch'), 'That is wrong!');
```

### 打印表格
`console.table()`方法，可以将数组、对象以表格的形式打印输出，如果只输出其中的某一列，可以加上第二个参数，如下所示：

```Javascript
console.table(dogs);
console.table(dogs, ["age"]);
```
### 分组打印

```Javascript
const dogs = [{ name: 'Snickers', age: 2 }, { name: 'hugo', age: 8 }];
dogs.forEach(dog => {
    console.group(`${dog.name}`);        
//  console.groupCollapsed(`${dog.name}`);  // 列表默认叠起状态
    console.log(`${dog.name}`);
    console.log(`${dog.age}`);
    console.log(`${dog.name} 有 ${dog.age} 岁了`);
    console.groupEnd();
});
```
`group()`方法中可以传入这个分组的名称。`group()/groupCollapsed() `与 `groupEnd()` 之间的内容会自动分组，区别在于是否能自动折叠。

### console.count() 计数

通过`console.count()`可以对输出的对象进行计数。但需要注意的是这里的计数对象仅限于由 `count()` 输出的内容，并非所有 `console` 中的输出。

![](http://om1c35wrq.bkt.clouddn.com/day9-count11.png)

### `time` 计时

用 `time("name")` 和 `timeEnd("name")` 分别控制开始点和结束点，它们两的参数表示当前计时的名称，可以自定义但需要保持相同。所以如果想看异步获取数据花了多场时间，可以这样写：

````js
console.time('fetch my data');
fetch("https://api.github.com/users/soyaine")
  .then(data => data.json())
  .then(data => {
  console.timeEnd('fetch my data');
  console.log(data);
});
````

如果 timeEnd 中的名称如果和上面不一样，得到的数据是系统当前时间换算后的毫秒值。
