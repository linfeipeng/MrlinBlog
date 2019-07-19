---
layout: post
title: "js-视频播放速率拖拽"
date: 2019-7-07 12:15
comments: true
tags: 
	- js
---
# Day28 - Video Speed Controller

> 作者：©Mrlin(史密斯林)
> 简介：学习记录，用于记录在CSDN课程中的学习内容。
> 课程：[30天完成30个JS原生开发项目挑战视频教程](https://edu.csdn.net/course/detail/5776)。[JavaScript30](https://javascript30.com) 是 [Wes Bos](https://github.com/wesbos) 推出的一个 30 天挑战。项目免费提供了 30 个视频教程、30 个挑战的起始文档和 30 个挑战解决方案源代码。目的是帮助人们用纯 JavaScript 来写东西，不借助框架和库，也不使用编译器和引用。


## 效果如下

<iframe src="/assets/demo/js_learn/class28/index-FINISHED.html" width="100%" height="400" scrolling="auto"></iframe>

<!-- more -->

第28天的挑战主要是拖拽右边的进度条来设置当前视频的播放速率。

## HTML 源码


```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <title>Video Speed Scrubber</title>
  <link rel="stylesheet" href="style.css">
</head>

<body>

  <div class="wrapper">
    <video class="flex" width="765" height="430" src="https://www.dropbox.com/s/nf6jfkwck1glsyo/12%20-%20flex-wrapping-and-columns.mp4?dl=1"
      loop controls></video>
    <div class="speed">
      <div class="speed-bar">1×</div>
    </div>
  </div>
</body>

</html>
```

由上面的代码不难看出，UI由左边的一个video和右边的一个div组成。

## CSS 代码

```css
body {
  margin: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: #4C4C4C url('https://unsplash.it/1500/900?image=1021');
  background-size: cover;
  font-family: sans-serif;
}

.wrapper {
  width: 850px;
  display: flex;
}

video {
  box-shadow: 0 0 1px 3px rgba(0, 0, 0, 0.1);
}

.speed {
  background: #efefef;
  flex: 1;
  display: flex;
  align-items: flex-start;
  margin: 10px;
  border-radius: 50px;
  box-shadow: 0 0 1px 3px rgba(0, 0, 0, 0.1);
  overflow: hidden;
}

.speed-bar {
  width: 100%;
  background: linear-gradient(-170deg, #2376ae 0%, #c16ecf 100%);
  text-shadow: 1px 1px 0 rgba(0, 0, 0, 0.2);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2px;
  color: white;
  height: 16.3%;
}
```

## JS 源码

```js
<script>
  const speed = document.querySelector('.speed');
  const bar = speed.querySelector('.speed-bar');
  const video = document.querySelector('.flex');

  function handleMove(e) {
      const y = e.pageY - this.offsetTop;
      const percent = y / this.offsetHeight;
      const min = 0.4;
      const max = 4;
      const height = Math.round(percent * 100) + '%';
      const playbackRate = percent * (max - min) + min;
      bar.style.height = height;
      bar.textContent = playbackRate.toFixed(2) + '×';
      video.playbackRate = playbackRate;
    }

  speed.addEventListener('mousemove', handleMove);

</script>
```

**代码逻辑：**

- 获取组建

```js
const speed = document.querySelector('.speed');
const bar = speed.querySelector('.speed-bar');
const video = document.querySelector('.flex');
```


- 监听`speed`控件，鼠标是否处于移动状态，如果在移动，调用`handleMove`函数。

```js
speed.addEventListener('mousemove', handleMove);
```

- 改变`speed`的状态，以及及时更新`video`的`playbackRate`属性以改变播放速率

```js
function handleMove(e) {
    const y = e.pageY - this.offsetTop;
    const percent = y / this.offsetHeight;
    const min = 0.4;
    const max = 4;
    const height = Math.round(percent * 100) + '%';
    const playbackRate = percent * (max - min) + min;
    bar.style.height = height;
    bar.textContent = playbackRate.toFixed(2) + '×';
    video.playbackRate = playbackRate;
}
```
