[`useMemo`](https://zh-hans.react.dev/reference/react/useMemo) 经常与 `useCallback` 一同出现。当尝试优化子组件时，它们都很有用。他们会 [记住](https://en.wikipedia.org/wiki/Memoization)（或者说，缓存）正在传递的东西：

```tsx
import { useMemo, useCallback } from 'react';

  

function ProductPage({ productId, referrer }) {

  const product = useData('/product/' + productId);

  

  const requirements = useMemo(() => { //调用函数并缓存结果

    return computeRequirements(product);

  }, [product]);

  

  const handleSubmit = useCallback((orderDetails) => { // 缓存函数本身

    post('/product/' + productId + '/buy', {

      referrer,

      orderDetails,

    });

  }, [productId, referrer]);

  

  return (

    <div className={theme}>

      <ShippingForm requirements={requirements} onSubmit={handleSubmit} />

    </div>

  );

}
```

区别在于你需要缓存 **什么**:

- **[`useMemo`](https://zh-hans.react.dev/reference/react/useMemo) 缓存函数调用的结果**。在这里，它缓存了调用 `computeRequirements(product)` 的结果。除非 `product` 发生改变，否则它将不会发生变化。这让你向下传递 `requirements` 时而无需不必要地重新渲染 `ShippingForm`。必要时，React 将会调用传入的函数重新计算结果。
- **`useCallback` 缓存函数本身**。不像 `useMemo`，它不会调用你传入的函数。相反，它缓存此函数。从而除非 `productId` 或 `referrer` 发生改变，`handleSubmit` 自己将不会发生改变。这让你向下传递 `handleSubmit` 函数而无需不必要地重新渲染 `ShippingForm`。直至用户提交表单，你的代码都将不会运行。

如果你已经熟悉了 [`useMemo`](https://zh-hans.react.dev/reference/react/useMemo)，你可能发现将 `useCallback` 视为以下内容会很有帮助：

```
// 在 React 内部的简化实现function useCallback(fn, dependencies) {  return useMemo(() => fn, dependencies);}
```

[阅读更多关于 `useMemo` 与 `useCallback` 之间区别的信息](https://zh-hans.react.dev/reference/react/useMemo#memoizing-a-function)。