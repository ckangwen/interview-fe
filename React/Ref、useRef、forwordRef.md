一个标准的`Ref`是一个对象：`{current:null}`，用来绑定`DOM`元素的引用和组件的实例

在生成`Ref`对象时，常用的有两种方法
在类组件中，我们往往使用`React.createRef`来生成`Ref`对象
而`useRef`通常用于函数组件中`Ref`对象的生成
这也是`React.createRef`与`useRef`在使用上的一个区别


## forwordRef 作用
react16新增的方法