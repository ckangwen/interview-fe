#Vue 

Option API
用组件的选项 (`data、computed、methods、watch`) 组织逻辑
当组件变得复杂，导致对应属性的列表也会增长，这可能会导致组件难以阅读和理解。


Composition API
组件根据逻辑功能来组织的，一个功能所定义的所有 `API` 会放在一起（ 更加的 **高内聚，低耦合** ）

`Composition Api` 相对`Options Api`的两大优点
- 逻辑组织
	- Options Api，在处理一个大型的组件时，内部的逻辑点容易碎片化
	- Composition Api 将某个逻辑关注点相关的代码全都放在一个函数里，更加的 高内聚，低耦合

- 逻辑复用
	- 在`vue2.0`中，当混入多个`mixin`会存在两个非常明显的问题：命名冲突、数据来源不清晰
	- 而`Composition Api`可以通过编写多个hooks函数就很好的解决了

- 因为`Composition API`几乎是`函数`，会有更好的`类型推断`。
- `Composition API` 对 `tree-shaking` 友好，`代码也更容易压缩`
- `Composition API`中见不到`this`的使用，减少了`this`指向不明的情况