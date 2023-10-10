#CSS 


1. 是否占据空间
	- `display: none` 不占据任何空间
	- `visibility:hidden` 该元素空间依旧存在

2. 是否渲染
	- display:none，会触发reflow（回流），进行渲染
	- visibility:hidden，只会触发repaint（重绘），因为没有发现位置变化，不进行渲染

3. 是否是继承属性
	- display:none，display不是继承属性。父元素为display:none，子元素也不显示
	- visibility:hidden，visibility是继承属性。父元素为visibility:hidden，若子元素使用了visibility:visible，这个子孙元素又会显现出来

4. 读屏器是否读取
	- 读屏器不会读取display：none的元素内容（将 display 设置为 none 会将元素从 可访问性树 accessibility tree 中移除，这会导致该元素及其所有子代元素不再被屏幕阅读技术 screen reading technology 访问）
	- 会读取visibility：hidden的元素内容