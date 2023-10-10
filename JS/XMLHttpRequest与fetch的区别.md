#JavaScript 
https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API

相同点
- 都是浏览器提供的功能，可以发送http网络请求，接收服务器返回的数据
- 在浏览器中都存在跨域问题
-
-

区别
- XMLHttpRequest是回调方式，fetch
- 是promise
- fetch支持流式返回，XMLHttpRequest只能等到结果全部返回
- fetch需要通过AbortController中止，XMLHttpRequest可以 通过abort方法中止
-  fetch返回一个promise，promise返回Response对象
- 在网络错误或跨域是会reject，接口500不会reject
- fetch 可以在 ServiceWorker 使用，XMLHttpRequest 不行

XMLHttpRequets和fetch虽然功能类似，但是在核心实现上是不一样的
- fetch底层是对http接口的封装
- XMLHttpRequets基于回调函数，而Fetch是基于promise的设计


XMLHttpRequets兼容性非常好，基本是所有的浏览器都支持
fetch由于是新的api，所以兼容性比XMLHttpRequets要差点，但是主流的浏览器基本都已经支持了

进度读取
可以对下载和上传的进度进行监听, 监听的事件需要写在`open`方法之前
```js
# 下载数据监听
const xhr = new XMLHttpRequest()
xhr.addEventListener('progress', (e) => {
}, false)
xhr.open()
xhr.send()


# 上传数据监听
const xhr = new XMLHttpRequest()
xhr.upload.addEventListener('progress', (e) => {
    
}, false)
....

```

fetch无法监听到进度


请求中断
在请求中可以设置超时属性，可以通过abort()中断当前请求
```js
const xhr = new XMLHttpRequest()
xhr.open('get', 'http://xxx.com/api', true)
xhr.timeout = 30000
xhr.onload = () => {
    // 请求完成 todo
}
xhr.ontimeout = (e) => {
    // 请求超时todo
}
xhr.send()

```

fetch没有超时属性和终止当前请求的方法，需要手动的实现



`fetch`：是 `http` 的数据请求方式，是 `XMLHttpRequest` 的一种代替方案，没有使用到 `XMLHttpRequest` 这个类。`fetch` 不是 ajax，而是原生的 js。`fetch()` 使用 `Promise`，不使用回调函数。`fetch` 是 ES8 中新增的 api，兼容性不是很好，IE 完全不兼容 `fetch` 写法。

`fetch()` 采用模块化设计，API 分散在 `Response` 对象、`Request` 对象、`Headers` 对象上。

`fetch()` 通过数据流（Stream 对象）处理数据，对于请求大文件或者网速慢的场景相当有用。`XMLHttpRequest` 没有使用数据流，所有的请求都必须完成后才拿到


思考 fetch 的缺点

1. `fetch` 的 `get/head` 请求不能设置 `body` 属性。
2. `fetch` 请求后，服务器返回的状态码无论是多少包括(4xx, 5xx)，`fetch` 都不认为是失败的，也就是使用 `catch` 也不能直接捕捉到错误，需要再第一个 `then` 中做一些处理。