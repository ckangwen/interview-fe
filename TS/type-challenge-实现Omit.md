#Typescript 

```ts
type MyOmit<T, K extends keyof T> = {
  [P in keyof T as P extends K ? never: P] :T[P]
}
```

---


```ts
type MyOmit<T, K extends keyof T> = Pick<T, Exclude<keyof T, K>>
```


---

```ts
type MyOmit<T, K extends keyof T> = Pick<T,{
  [O in keyof T]: O extends K ? never : O
}[keyof T]>
```