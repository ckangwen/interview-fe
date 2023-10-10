#JavaScript 

相同点：都是用来遍历的
不同点：
- for-in可以 数组 + 对象 、for-of 只可以遍历数组
- for-in 可以遍历原型中的属性、 for-of 不可以遍历原型中的属性
- 遍历数组时 for-in可以遍历 下标 + 元素 for-of之能遍历元素

```js
    const arr = [10, 20, 30]
    for(let key in arr) {
      console.log(key)
      console.log(arr[key])
    }

    for(let item of arr) { //只遍历元素
      console.log(item)
    }


    const obj = {
      name: '张三',
      age: 18,
      gender: '男'
    }

    for(let key in obj) {
      console.log(key)
      console.log(obj[key])
    }

    // for(let item of obj) {
      // console.log(item)
    // } 直接报错

```

## forEach
- 只能遍历数组
- 遍历时能够获取当前元素以及元素下标
- 无法使用break、continue、return中断循环，不过可以通过抛出异常的方式中断循环

## for-in
- 可以遍历对象、数组，并且原型链上的所有属性都将被访问
- 遍历时获取索引/键名
- 优先迭代数组属性
- 无法迭代Symbol 类型的属性
- 跟forEach相比，可以正确响应break，continue，return
- 遍历顺序有可能不是按照实际数组的内部顺序


## for-of
- for of 循环是基于Iterator(遍历器的) 只要拥有Iterator 机制的数据结构都能用for of 循环，例如Set、Map
- 获取到的是当前元素
- 可以迭代Symbol 类型的属性
- 支持字符串遍历

## for
- 只能遍历数组
- 可以获取到索引
- 可以控制循环的起始点与结束条件
