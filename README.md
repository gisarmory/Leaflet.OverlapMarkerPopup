# leaflet如何优雅的展示重叠点位的气泡窗口


## 简介：

在平时项目工作中，经常遇到这种需求，两个或者多个点位完全重合了，但就是想点击时同时看到这些个点位的信息。

在此，我们从两个维度来解决此问题。



## 方案一 PopupListLayer：

此方案的处理方式是，点击时获取与该点位重合的所有点位，然后整合需要在气泡中展示的内容，添加切换功能，达到切换展示所有气泡信息的效果。

### 用法：

第一步：初始化`popupListLayer` 

`var popupListLayer = new L.popupListLayer().addTo(map)`。

第二步：将点位以及气泡内容传入`popupListLayer`

`popupListLayer.addMarker(marker, contentHTML)`

![202012040101](https://blogimage.gisarmory.xyz/202012040101.png)



## 方案二 PopupLayoutLayer：

此方案主要是借鉴在GIT上发现的`leaflet-tooltip-layout`这个插件。通过处理`L.tooltip()`位置关系，实现多气泡信息展示，同时尽可能避免气泡之间的遮盖。

该方案支持**通过点击点位展示气泡**以及**同时展示所有点位气泡**。

### 用法：

我们将该方法封装成插件，引用插件后，只需简单的两步即可实现上述效果。

第一步：初始化`popupLayoutLayer`。如需查看所有点位气泡，需将 `showAll` 参数设置为 `true`，默认为`false，点击查看气泡信息。

`var popupLayoutLayer = new L.popupLayoutLayer({`

​	`showAll: true // true，显示所有气泡；默认为 false，通过点击查看气泡`，

`}).addTo(map)`

第二步：将点位以及气泡内容传入popupLayoutLayer

`popupLayoutLayer.addMarker(marker, contentHTML)`

如果为点击查看气泡，只需上面两步即可实现效果；若要展示所有气泡，还需下面一步，显示所有气泡。

`popupLayoutLayer.showPopup()`

![202012040102](F:\myself\gisarmory\Leaflet.TooltipLayout\202012040102.png)



## 示例：

[PopupListLayer 切换显示气泡](http://gisarmory.xyz/blog/index.html?demo=LeafletOverlapMarkerPopup1)

[PopupLayoutLayer 显示所有气泡](http://gisarmory.xyz/blog/index.html?demo=LeafletOverlapMarkerPopup2)

[PopupLayoutLayer 点击显示气泡](http://gisarmory.xyz/blog/index.html?demo=LeafletOverlapMarkerPopup3)



## 君子协议
只要star本库，并关注公众号“GIS兵器库”，你就可以免费使用此插件。公众号二维码：

![](http://blogimage.gisarmory.xyz/20200923063756.png)

（若上方二维码无法显示，点此链接 [GIS兵器库](http://blogimage.gisarmory.xyz/20200923063756.png) ）

## 相关链接

[Leaflet](https://leafletjs.com/index.html)、[Leaflet.Path.DashFlow](https://gitlab.com/IvanSanchez/Leaflet.Path.DashFlow)

