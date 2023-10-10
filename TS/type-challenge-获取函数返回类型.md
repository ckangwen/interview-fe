#Typescript

```ts
const fn = (v: boolean) => {
  if (v)
    return 1
  else
    return 2
}

type a = MyReturnType<typeof fn> // 应推导出 "1 | 2"
```


```ts
type MyReturnType<T extends Function> =
  T extends (...args: any) => infer R
    ? R
    : never
```

