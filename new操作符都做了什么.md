#JavaScript 


new 操作符用于创建一个给定构造函数的实例对象

流程
- 创建一个新的对象
- 将对象与构造函数通过原型链连接起来
- 将构造函数中的this绑定到新建的对象上
- 根据构造函数返回类型作判断，如果是原始值则被忽略，如果是返回对象，需要正常处理

```js
function myNew(Con, ...args) {
  // 创建一个新的空对象
  let obj = {};
  // 将这个空对象的__proto__指向构造函数的原型
  // obj.__proto__ = Con.prototype;
  Object.setPrototypeOf(obj, Con.prototype);
  // 将this指向空对象
  let res = Con.apply(obj, args);
  // 对构造函数返回值做判断，然后返回对应的值
  return res instanceof Object ? res : obj;
}

```









