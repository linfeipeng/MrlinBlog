---
layout: post
title: "openLayers"
date: 2019-5-1 12:15
comments: true
tags: 
	- openLayers
---
# Day1 - 初始化地图 

> 作者：©Mrlin(史密斯林)
> 简介：学习记录，用于记录在CSDN课程中的学习内容。
> 课程：[Openlayers开发视频教程](https://edu.csdn.net/course/detail/8114)。[Openlayers](https://openlayers.org/) A high-performance, feature-packed library for all your mapping needs.OpenLayers makes it easy to put a dynamic map in any web page. It can display map tiles, vector data and markers loaded from any source. OpenLayers has been developed to further the use of geographic information of all kinds. It is completely free, Open Source JavaScript, released under the 2-clause BSD License (also known as the FreeBSD).(来自官方介绍)


## 效果如下

<iframe src="/assets/demo/openlayers_learn/m01Hello.html" width="800" height="400" scrolling="auto"></iframe>

<br/>

<!-- more -->

第1天初始化地图

## HTML 代码

```html
<!doctype html>
<html lang="en">
<head>
    <link rel="stylesheet" href="https://openlayers.org/en/v4.6.5/css/ol.css" type="text/css">
    <!-- <link rel="stylesheet" href="libweb/v464/ol.css" type="text/css"> -->
    <style>
        .map {
            height: 400px;
            width: 100%;
        }
    </style>
    <script src="https://openlayers.org/en/v4.6.5/build/ol.js" type="text/javascript"></script>
    <!-- <script src="libweb/v464/ol.js" type="text/javascript"></script> -->
    <title>OpenLayers example</title>
</head>
<body>
<h2>My Map</h2>
<div id="map" class="map"></div>
<script type="text/javascript">
    var map = new ol.Map({
        target: 'map',
        layers: [
            new ol.layer.Tile({
                source: new ol.source.OSM()
            })
        ],
        view: new ol.View({
            center: ol.proj.fromLonLat([37.41, 8.82]),
            zoom: 4
        })
    });
</script>
</body>
</html>
```

- 地图三要素
>target  (加载的dom元素或者dom元素id)
>layers  (图层)
>view    (中心点、坐标系、缩放等级)

```js
 var map = new ol.Map({
        target: 'map',
        layers: [
            new ol.layer.Tile({
                source: new ol.source.OSM()
            })
        ],
        view: new ol.View({
            center: ol.proj.fromLonLat([37.41, 8.82]),
            zoom: 4
        })
    });
```
- [new ol.Map](https://openlayers.org/en/latest/apidoc/module-ol_Map-Map.html)
常用方法:

```js
addControl(control)  //添加控制
addInteraction(interaction)  //添加交互
addLayer(layer)   //添加图层
addOverlay(overlay)  //添加遮盖物
forEachFeatureAtPixel(pixel, callback, opt_options) //遍历每一块feature
forEachLayerAtPixel(pixel, callback, opt_options) //遍历每一个layer
```