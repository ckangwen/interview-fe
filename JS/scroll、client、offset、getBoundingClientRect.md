#JavaScript 

## offset
![[8e70bf2d5a2044b89cb3ea03a4534457~tplv-k3u1fbpfcp-zoom-in-crop-mark_4536_0_0_0.webp]]

offsetWidth
元素在水平方向上占用的空间大小
offsetWidth = borderLeftWidth + paddingLeft + width + paddingRight + borderRightWidth


offsetHeight
元素在垂直方向上占用的空间大小


offsetTop
元素的上外边框至offsetParent元素的上内边框之间的像素距离


offsetLeft
元素的左外边框至offsetParent元素的左内边框之间的像素距离


offsetParent
**与当前元素最近的经过定位(position不等于static)的父级元素，如果没有找到，则会选定为body**


## client

![[346c669d683b421db3608fd3ecb25be7~tplv-k3u1fbpfcp-zoom-in-crop-mark_4536_0_0_0.webp]]

clientHeight
clientHeight = paddingTop + height + paddingBottom
不包含页面不可见部分

clientWidth
clientWidth = paddingLeft + width + paddingRight
不包含页面不可见部分

clientLeft
左边框的宽度

clientTop
上边框的宽度


## scroll

![[957d454b02864754a0001afb5487d25c~tplv-k3u1fbpfcp-zoom-in-crop-mark_4536_0_0_0.webp]]
scrollHeight
元素的总高度，包括由于溢出而无法展示在网页的不可见部分
> 因为子元素比父元素高，父元素不想被子元素撑的一样高就显示出了滚动条，在滚动的过程中本元素有部分被隐藏了，scrollHeight代表包括当前不可见部分的元素的高度。而可见部分的高度其实就是clientHeight
> 
> 在有滚动条时讨论scrollHeight才有意义，在没有滚动条时scrollHeight=clientHeight恒成立

scrollWidth
元素的总宽度，包括由于溢出而无法展示在网页的不可见部分

scrollTop
被隐藏在内容区域上方的高度，与scrollY返回值一样

scrollLeft
被隐藏在内容区域左侧的的宽度，与scrollX返回值一样

window.scrollX
文档/页面水平方向滚动的像素值，需要注意这个是属性是window对象独享的，并且window.pageXOffset是它的别名

window.scrollY
文档/页面垂直方向滚动的像素值，需要注意这个是属性是window对象独享的，并且window.pageYOffset是它的别名


## getBoundingClientRect

提供了元素大小，以及其相对于视口的位置

![[Pasted image 20230722163354.png]]

