
Proxy对象，用于创建一个对象的代理，从而实现基本操作的拦截和自定义

`proxy = Proxy(target, handler)`
如果handler为空，所有对proxy的将操作都会转发给target

Reflect 提供拦截JavaScript操作的方法。这些方法与proxy handler的方法相同。Reflect不是一个函数对象，因此它是不可构造的


`Reflect` 允许我们将操作符（`new`，`delete`，……）作为函数（`Reflect.construct`，`Reflect.deleteProperty`，……）执行调用


**为什么要在Proxy内使用Reflect**
> https://juejin.cn/post/7080916820353351688

Proxy的get中还存在一个额外的参数`receiver`
receiver 不仅仅会表示 Proxy代理对象本身，同时还有可能表示 继承于Proxy代理对象的对象
receiver 为了传递正确的调用者指向


```js
const parent = {
  name: '19Qingfeng',
  get value() {
    return this.name;
  },
};

const handler = {
  get(target, key, receiver) {
    return Reflect.get(target, key);
    // 这里相当于 return target[key]
  },
};

const proxy = new Proxy(parent, handler);

const obj = {
  name: 'wang.haoyu',
};

// 设置obj继承与parent的代理对象proxy
Object.setPrototypeOf(obj, proxy);

// log: false
console.log(obj.value);

```

- 当我们调用 obj.value 时，由于obj本身不存在value属性
- 由于它继承的proxy对象中存在value的属性访问操作符，所以会发生屏蔽效果
- 此时会触发proxy上的get value()属性访问操作
- 由于访问了proxy上的value属性访问器，所以此时会触发get陷阱
- 进入陷阱时，target为源对象，也就是parent，key为value
- 陷阱中返回 `Reflect.get(target, key)`相当于`target[key]`
- 此时this指向在get陷阱中被偷偷修改掉了
- 原本调用方的 obj 在陷阱中被修改成为了对应的 target 也就是 parent 。
- 自然而然打印出了对应的 `parent[value]` 也就是 19Qingfeng 


**触发代理对象的劫持时，保持正确的this指向**


Reflect
Reflect.set 能够知道是否设置成功（例如修改只读属性时候）
Reflect不会因为报错而中断正常的代码逻辑执行
如果发生了继承，为了明确调用主体，需要使用到receiver
receiver可以把调用对象当作target参数，而不是原始Proxy构造的对象。


**`Reflect.get(target, propertyKey[, receiver])`**
- target：需要取值的目标对象
- propertyKey：需要获取的值的键值
- receiver：如果target对象中指定了getter，**receiver则为getter调用时的this值**


Reflect对象经常和Proxy代理一起使用，原因有三点：

1. Reflect提供的所有静态方法和Proxy第2个handle参数方法是一模一样的。
2. Proxy get/set()方法需要的返回值正是Reflect的get/set方法的返回值，可以天然配合使用，比直接对象赋值/获取值要更方便和准确。
3. receiver参数具有不可替代性。