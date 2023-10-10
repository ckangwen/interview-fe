#React 

## `const value = useContext(SomeContext)`



`useContext`可以读取和订阅组件中的context
> context是通过createContext创建的，本身不包含信息，只代表你可以提供或从组件中读取的信息类型

context 的值是，向上查找最近的的 `SomeContext.Provider` 的 `value`。
如果没有这样的 provider，那么返回值将会是为创建该 context 传递给 `createContext`的 `defaultValue`。

如果 context 发生变化，React 会自动重新渲染读取 context 的组件。


**注意事项**
- 相应的 `<Context.Provider>` 需要位于调用 `useContext()` 的组件 **之上**。
- 从 provider 接收到不同的 `value` 开始，React 自动重新渲染使用了该特定 context 的所有子级。先前的值和新的值会使用 [`Object.is`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/is) 来做比较。使用 [`memo`](https://zh-hans.react.dev/reference/react/memo) 来跳过重新渲染并不妨碍子级接收到新的 context 值。


---

## 在传递对象和函数时优化重新渲染
