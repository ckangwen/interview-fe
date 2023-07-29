#JavaScript 


## yield

`[rv] = yield [expression]`

```js
function* foo(index) {
  while(index < 2) {
    yield index;
    index++;
  }
}

const iterator = foo(0)

console.log( iterator.next().value )
// 0

console.log( iterator.next().value )
// 1
```

`yield` 关键字使生成器函数执行暂停
`yield` 关键字后面的表达式的值返回给生成器的调用者
它可以被认为是一个基于生成器的版本的 `return` 关键字。

`yield` 关键字实际返回一个 `IteratorResult` 对象
它有两个属性，`value` 和 `done`
`value` 属性是对 `yield` 表达式求值的结果，而 `done` 是 `false`，表示生成器函数尚未完全完成

一旦遇到 `yield` 表达式，生成器的代码将被暂停运行，直到生成器的 `next()` 方法被调用
每次调用生成器的 `next()` 方法时，生成器都会恢复执行，直到达到以下某个值：
- `yield`，导致生成器再次暂停并返回生成器的新值。下一次调用 `next()` 时，在 `yield` 之后紧接着的语句继续执行
- `throw` 用于从生成器中抛出异常。这让生成器完全停止执行，并在调用者中继续执行，正如通常情况下抛出异常一样。。
- 到达生成器函数的结尾.在这种情况下，生成器的执行结束，并且 `IteratorResult` 给调用者返回 `value` 的值是 `undefined`并且 `done` 为 `true`。
- 到达 `return` 语句。在这种情况下，生成器的执行结束，并将 `IteratorResult` 返回给调用者，其 `value` 的值是由 `return` 语句指定的，并且 `done` 为 `true`。

---

调用Generator函数之后，该函数并不执行，返回的也不是函数运行结果
而是一个指向内部状态的指针对象，也就是遍历器对象(Iterator Object)
下一步，必须调用遍历器对象的`next`方法，是的指针移向下一个状态


Generator 函数返回的遍历器对象，只有调用next方法才会遍历下一个内部状态
所以其实提供了一个可以暂停执行的函数
yield 表达式就是暂停标志
```js
function *fetch() {
    yield ajax('aaa')
    yield ajax('bbb')
    yield ajax('ccc')
}
let gen = fetch()
let res1 = gen.next() // { value: 'aaa', done: false }
let res2 = gen.next() // { value: 'bbb', done: false }
let res3 = gen.next() // { value: 'ccc', done: false }
let res4 = gen.next() // { value: undefined, done: true } done为true表示执行结束

```
