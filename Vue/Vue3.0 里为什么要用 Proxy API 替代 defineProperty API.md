#Vue


### Object.defineProperty
`Object.defineProperty()` 方法会直接在一个对象上定义一个新属性，或者 修改一个对象的现有属性，并返回此对象

**为什么能实现响应式**
通过defineProperty的两个属性，`get`和`set`
get
属性的 getter 函数，当访问该属性时，会调用此函数
执行时不传入任何参数， 但是会传入 this 对象
该函数的返回值会被用作属性的值

set
属性的 setter 函数，当属性值被修改时，会调用此函数
该方法接受一个参数（也 就是被赋予的新值），会传入赋值时的 this 对象。
默认为 undefined

```js
function update(obj) {
  app.innerText = obj.foo
}

function defineReactive(obj, key, val) {
  Object.defineProperty(obj, key, {
    get() {
      return val
    },
    set(newVal) {
      if (val !== newVal) {
        val = newVal
        update(obj)
      }
    }
  })
}
```
调用defineReactive函数，数据发生变化，触发update函数，实现数据响应式

**在对象存在多个key的情况下，需要进行遍历**
```js
function observe(obj) {
  if (typeof obj !== "object" || obj === null) {
    return
  }

  Object.keys(obj).forEach((key) => {
    defineReactive(obj, key, obj[key])
  })
}
```

如果存在嵌套对象的情况，还需要在`defineReactive`中进行递归
``` js
function defineReactive(obj, key, val) {
  observe(obj)

  Object.defineProperty(obj, key, {
    get() {
      return val
    },
    set(newVal) {
      if (val !== newVal) {
        val = newVal
        update(obj)
      }
    }
  })
}
```

当给 key 赋值为对象的时候，还需要在 set 属性中进行递归
``` js
function defineReactive(obj, key, val) {
  observe(obj)

  Object.defineProperty(obj, key, {
    get() {
      return val
    },
    set(newVal) {
      if (val !== newVal) {
        val = newVal
        observe(newVal)
        update(obj)
      }
    }
  })
}
```

存在的问题
- 对一个对象的删除与增加属性，无法劫持到
- 无法对数组侦听
- 需要对每个属性进行遍历监听，如果嵌套对象，需要深层监听，会造成性能问题

所以在Vue2中，增加了`set`, `delete` API，并且对数组的api方法进行了重写



### Proxy

Proxy 可以监听对这个对象的所有操作

[[-实现基于Proxy的Vue3响应式库]]