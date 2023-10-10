#JavaScript 


this 可以根据上下文环境的变化而发生改变，导致它的指向变得混乱或难以预测。
常见的导致 this 指向混乱的原因包括以下几个方面：

### 函数调用方式不同：this 会指向调用该方法的对象
如果使用普通函数调用方式（如 func()），则 this 会指向全局对象 window

### 没有明确调用者时，this指向window


### 箭头函数的使用： 箭头函数的this指向外层作用域的this
箭头函数不具有自己的 this 值，它会捕获上下文中的 this 值。因此，如果在箭头函数中访问 this，它将引用外层作用域中的 this 值。

   
### apply、call 和 bind：apply、call 和 bind 方法可以将函数执行时的 this 值指向调用者
其中，apply 和 call 方法可以立即执行函数并传入参数，而 bind 方法可以返回一个新函数，该函数的 this 值被绑定到指定的对象上。


### 使用new调用时，this指向new出来的对象

当你用new来执行一个函数时，这个函数就变成了一个类，new关键字会返回一个类的实例给你，这个函数会充当构造函数的角色。作为面向对象的构造函数，必须要有能够给实例初始化属性的能力，所以构造函数里面必须要有某种机制来操作生成的实例，这种机制就是this。让this指向生成的实例就可以通过this来操作实例了


对象的嵌套和继承：当一个对象被嵌套在另一个对象中或者使用继承时，this 的指向可能会变得混乱。这是因为 this 的指向取决于函数被调用时的上下文环境，而不是对象本身。因此，在嵌套对象或继承类中使用 this 时，需要特别注意它的指向。



  
### DOM 事件处理程序的使用：在处理 DOM 事件时，浏览器会将事件处理程序内部的 this 指向触发事件的元素

```js
function func(e) {
  console.log(this === e.currentTarget);   // 总是true
  console.log(this === e.target);          // 如果target等于currentTarget,这个就为true
}

const ele = document.getElementById('test');

ele.addEventListener('click', func);

```
`currentTarget`指的是绑定事件的DOM对象，`target`指的是触发事件的对象。
DOM事件回调里面this总是指向`currentTarget`，如果触发事件的对象刚好是绑定事件的对象，即`target === currentTarget`，this也会顺便指向`target`。
如果回调是箭头函数，this是箭头函数申明时作用域的this。

