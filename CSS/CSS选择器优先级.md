#CSS


CSS选择器
- id选择器
- 类选择器
- 标签选择器
- 后代选择器
- 子选择器
- 相邻同胞选择器
- 群组选择器
- 伪类选择器
- 伪元素选择器
- 属性选择器


**优先级**
!important > 内联样式 > ID 选择器 > 类选择器 = 属性选择器 = 伪类选择器 > 标签选择器 = 伪元素选择器

**计算权重**
计算权重的时候，可以用一组向量标志来表示(A, B, C, D)
- 如果存在内联样式，那么A=1，否则A=0
- B的值等于 ID选择器出现的次数
- C的值等于 类选择器 和 属性选择器 和 伪类 出现的总次数
- D的值等于 标签选择器 和 伪元素 出现的总次数

**比较规则**
- 从左向右进行比较，较大者优先级更高
- 如果相等，则比较后一位
- 如果4位数值全部相等，则后面的会覆盖前面的




