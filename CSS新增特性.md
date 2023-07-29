#CSS 





max-content
假设元素容器有足够的宽度，此时所占据的宽度是就是`max-content`所表示的尺寸
具体可以表现为，文本内容即便溢出也不会被换行。

min-content
采用内部元素最小宽度值最大的那个元素的宽度作为最终容器的宽度
具体可以表现为，元素宽度不会超过最长单词的宽度

fit-content
收缩宽度知道能够适应元素内容
盒子会使用可用的空间，但永远不会超过 max-content


**CSS 比较函数**
min(), max(), clamp()

clamp(min, val, max)
让val限制在最大值和最小值中间
> = max(min, min(val, max))


**CSS 容器查询**
`@container`规则，能够根据元素容器的大小应用样式
类似于`@media`只是匹配的尺寸对象不同
`@media`匹配的是浏览器窗体，而`@container`匹配的是某个元素

要使用容器查询，你需要在元素上，声明一个局限上下文（containment context），以便浏览器知道你可能希望稍后查询此容器的尺寸
需要使用`content-type`属性

content-type
表示指向容器的类型，是水平方向的（对应宽度），还是包括垂直方向的（对应宽度和高度）
- size：水平和垂直方向都建立
- inline-size: 只在水平方向建立
- normal：该元素不是任何容器大小查询的查询容器，但仍然是容器样式查询的查询容器

`container-name`的作用是给容器元素命名，这个属性在页面中存在多个容器元素的时候很有用

container-type和container-name可以简写为container属性
``` css
.post {
 /** container: sidebar / inline-size; **/
  container-type: inline-size;
  container-name: sidebar;
}
```



**gap**
CSS的`gap`属性现在**已经支持flexBox中使用了**，该属性用于设置元素之间的间距
https://fehey.com/css-flex-gap

面对一堆标签等间距排列，使用margin方案存在两个问题
```css
.tag { margin-right: 8px; margin-bottom: 8px; }
```
1. 每行标签的最右侧必定会存在一个 8px 的间距，我们无法通过 `:last-of-type` 来控制。
2. 最后一行标签存在无用的底部间距，无法通过标签自身来消除。

解决办法是为标签的父容器，设置一个负值的右间距和下间距，以此来消除其对外部布局产生的影响。

但是用gap属性，能够更容易地实现
``` css
.tag-list { display: flex; flex-wrap: wrap; gap: 8px; }
```
其不会产生额外的外间距影响。只对其内部元素之间的间距进行生效


**content-visibility**
https://juejin.cn/post/7108921365628977166
CSS的`content-visibility`属性于控制元素的内容是否显示，主要值就是`hidden`和`visible`(默认值)；

该属性如果设置为`hidden`浏览器就会跳过该元素内容的渲染，需要的时候在将其设置为 visible ，这样可以提高浏览器的渲染速度。

浏览器会将元素的布局推迟到元素被滚动到视图中或被 JavaScript 访问时才进行，这可以有效减少浏览器的工作量，提高页面的响应速度和用户体验。

设置了 `content-visibility: hidden` 的元素，**其元素的子元素将被隐藏，但是，它的渲染状态将会被缓存**。所以，当 `content-visibility: hidden` 被移除时，用户代理无需重头开始渲染它和它的子元素。



- visible：默认值，没有任何效果，相当于没有添加`content-visibility`，渲染效果与往常一致
- hidden：与`display: none`类似，浏览器将跳过内容渲染（跳过的是子元素的渲染，不包含自身）
- auto：如果该元素不在屏幕上，并且与用户无关，则不会渲染其子元素

`content-visibility: hidden`的效果与`display: none`类似，但其实两者还是有比较大的区别的：
- content-visibility: hidden 只是隐藏了子元素，自身不会被隐藏
- content-visibility: hidden 隐藏内容的渲染状态会被缓存，所以当它被移除或者设为可见时，浏览器不会重新渲染，而是会应用缓存，所以对于需要频繁切换显示隐藏的元素，这个属性能够极大地提高渲染性能。


**contain-intrinsic-size**
当然，除 `content-visibility` 之外，还有一个与之配套的属性 -- `contain-intrinsic-size`。

`contain-intrinsic-size`：控制由 `content-visibility` 指定的元素的自然大小。

上面两个属性光看定义和介绍会有点绕。

我们首先来看看 `content-visibility` 如何具体使用。

`content-visibility: visible` 是默认值，添加后没有任何效果，我们就直接跳过。

  

**will-change**
https://juejin.cn/post/7015387929870598158
允许你提前告知浏览器你可能会对一个元素进行什么样的改变
这样它就可以提前设置适当的优化，避免了可能会对页面的响应性产生负面影响的启动成本
这些元素可以更快地被改变和渲染，页面将能够迅速地更新，从而带来更流畅的体验


**aspect-ratio**
设置宽高比
``` css
.box { aspect-ratio: 16 / 9; }
```


**滚动捕捉**
`scroll-snap-type`、`scroll-padding*`


**overscroll-behavior**
CSS中的`overscroll-behavior`是一个合并写法，可以拆分为`overscroll-behavior-x`和`overscroll-behavior-y`，它控制的是**当元素滚动到边界后继续滚动的效果**。
它的值有三个，分别是
- `auto`：默认效果；
- `contain`：依旧触发滚动到底部的效果（反弹），但是临近的滚动区域不会被影响；
- `none`：不会触发触底效果也不会影响临近的滚动区域。

当`overscroll-behavior`的值为`auto`时，在列表区域滚动到底时会影响其他区域的滚动，当不为`auto`时就不会影响其他区域的滚动。