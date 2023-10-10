#React 


## useCallback
`useCallback` 是一个允许你在多次渲染中缓存函数的 React Hook

用法
- 跳过组件的重新渲染
- 从memorized 回调中更新state
- 防止频繁触发 Effect
- 优化自定义hook


 **`useCallback(fn, dependencies)`**
 - fn：想要缓存的函数
	 - React 将会在**初次渲染**而非调用**时返回传入的fn函数**
	 - 当进行下一次渲染时，如果 `dependencies` 相比于上一次渲染时没有改变，那么 React 将会返回上一次渲染中缓存的fn函数
	 - 否则，React 将返回在最新一次渲染中传入的函数，并且将其缓存以便之后使用。

- dependencies
	- 有关是否更新 `fn` 的所有响应式值的一个列表
	- React 使用 `Object.is` 比较每一个依赖和它的之前的值。


## 用法

默认情况下，当一个组件重新渲染时，React将递归渲染它的所有子组件
不过可以将组件包裹在`memo`中
如果组件的props与上一次渲染时相同，组件将会跳过重新渲染


``` tsx
function ProductPage({ productId, referrer, theme }) {

  // 每当 theme 改变时，都会生成一个不同的函数

  function handleSubmit(orderDetails) {

    post("/product/" + productId + "/buy", {

      referrer,

      orderDetails,

    });

  }

  

  return (

    <div className={theme}>

      {/* 这将导致 ShippingForm props 永远都不会是相同的，并且每次它都会重新渲染 */}

      <ShippingForm onSubmit={handleSubmit} />

    </div>

  );

}
```

与字面量对象 `{}` 总是会创建新对象类似，**在 JavaScript 中，`function () {}` 或者 `() => {}` 总是会生成不同的函数**
这意味着 `ShippingForm` props 将永远不会是相同的
导致`memo`对性能的优化永远不会生效

这就是`useCallback`起作用的地方
```tsx
function ProductPage({ productId, referrer, theme }) {

  // 在多次渲染中缓存函数

  const handleSubmit = useCallback((orderDetails) => {

    post('/product/' + productId + '/buy', {

      referrer,

      orderDetails,

    });

  }, [productId, referrer]); // 只要这些依赖没有改变

  

  return (

    <div className={theme}>

      {/* ShippingForm 就会收到同样的 props 并且跳过重新渲染 */}

      <ShippingForm onSubmit={handleSubmit} />

    </div>

  );

}
```

**将 `handleSubmit` 传递给 `useCallback` 就可以确保它在多次重新渲染之间是相同的函数**，直到依赖发生改变。



---


## 是否应该在任何地方添加`useCallback`

使用 `useCallback` 缓存函数仅在少数情况下有意义
- 将其作为 props 传递给包装在 `memo` 中的组件。如果 props 未更改，则希望跳过重新渲染。
  缓存允许组件仅在依赖项更改时重新渲染。
- 传递的函数可能作为某些 Hook 的依赖。
  比如，另一个包裹在 `useCallback` 中的函数依赖于它，或者依赖于 `useEffect` 中的函数。

在其他情况下，将函数包装在 `useCallback` 中没有任何意义。不过即使这样做了，也没有很大的坏处。



---

## 防止频繁出发 Effect

有时，想要在 Effect 内部调用函数：
![[Pasted image 20230809165542.png]]

这会产生一个问题，每一个响应值都必须声明为 Effect 的依赖
但是如果将 `createOptions` 声明为依赖，它会导致 Effect 不断重新连接到聊天室
因为  `createOptions` 在每次渲染中都会改变

为了解决这个问题，需要在 Effect 中将要调用的函数包裹在 `useCallback` 中：
![[Pasted image 20230809165818.png]]

这将确保如果 `roomId` 相同，`createOptions` 在多次渲染中会是同一个函数。

**但是，最好消除对函数依赖项的需求**。将依赖函数移入 Effect **内部**：
![[Pasted image 20230809165852.png]]


---

## 优化自定义Hook

如果你正在编写一个 自定义 Hook，建议将它返回的任何函数包裹在 `useCallback` 中：
这确保了 Hook 的使用者在需要时能够优化自己的代码
![[Pasted image 20230809165947.png]]