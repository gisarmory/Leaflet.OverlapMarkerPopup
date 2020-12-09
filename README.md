# leaflet如何优雅的展示重叠点位的气泡窗口


## 简介：

在平时工作中，经常遇到这种问题，两个或者多个点位完全重合了，鼠标无法点击到被遮盖的点位，从而无法查看其气泡信息。

今天我们从另外两个维度来讨论，如何解决此问题。



## 方案一 PopupListLayer：

此方案的处理方式是，点击时获取与该点位重合的所有点位，然后整合需要在气泡中展示的内容，添加切换功能，达到切换展示所有气泡信息的效果。

### 用法：

第一步：初始化`popupListLayer` 

```js
var popupListLayer = new L.popupListLayer().addTo(map)
```

第二步：将点位以及气泡内容传入`popupListLayer`

```js
popupListLayer.addMarker(marker, contentHTML)
```

![2020120904](https://blogimage.gisarmory.xyz/2020120904.png)



## 方案二 PopupLayoutLayer：

此方案主要是借鉴在GIT上发现的`leaflet-tooltip-layout`这个插件。通过处理`L.tooltip()`位置关系，实现多气泡信息展示，同时尽可能避免气泡之间的遮盖。

该方案支持**通过点击点位展示气泡**，以及**同时展示所有点位气泡**。

### 用法：

我们将该方法封装成插件，引用插件后，只需简单的三步即可实现上述效果。

第一步：初始化`popupLayoutLayer`。如需查看所有点位气泡，需将 `showAll` 参数设置为 `true`，默认为`false`，点击查看气泡信息。

```js
var popupLayoutLayer = new L.popupLayoutLayer({

	showAll: true // true，显示所有气泡；默认为 false，通过点击查看气泡

}).addTo(map)
```

第二步：将点位以及气泡内容传入`popupLayoutLayer`

```js
popupLayoutLayer.addMarker(marker, contentHTML)
```

第三步：分为点击查看气泡和展示所有气泡两种情况

1、点击查看气泡。添加点击事件，在点击事件中添加气泡

```js
popupLayoutLayer.on('click', function(evt) {})
```

2、展示所有气泡，需将`showAll` 参数设置为 `true`

```js
popupLayoutLayer.showPopup()
```

![2020120903](https://blogimage.gisarmory.xyz/2020120903.png)



## 示例：

[PopupListLayer 切换显示气泡](http://gisarmory.xyz/blog/index.html?demo=LeafletOverlapMarkerPopup1)

[PopupLayoutLayer 显示所有气泡](http://gisarmory.xyz/blog/index.html?demo=LeafletOverlapMarkerPopup2)

[PopupLayoutLayer 点击显示气泡](http://gisarmory.xyz/blog/index.html?demo=LeafletOverlapMarkerPopup3)



## 君子协议
只要star本库，并关注公众号“GIS兵器库”，你就可以免费使用此插件。公众号二维码：

![](http://blogimage.gisarmory.xyz/20200923063756.png)

（若上方二维码无法显示，点此链接 [GIS兵器库](http://blogimage.gisarmory.xyz/20200923063756.png) ）

## 相关链接

[Leaflet](https://leafletjs.com/index.html)、[leaflet-tooltip-layout](https://github.com/ZijingPeng/leaflet-tooltip-layout)

