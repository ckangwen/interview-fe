#JavaScript 

![[Pasted image 20230821152422.png]]
### Name

cookie的名称


### Value

cookie的值

### Doamin
Cookie 的作用域，如果未设置默认为 `/`
决定在向此域发送请求时，是否携带此cookie
如果指定了 `Domain`，则对子域名同样生效

### Path
Cookie的有效路径
对子路径也生效
假如Cookie1和Cookie2的Domain都是a.com
但 Cookie1的 Path 为 /b
Cookie2 的 Path 为 /b/c
则在a.com/b页面时只可以访问Cookie1，在a.com/b/c页面时，可访问Cookie1和Cookie2

### Expires/Max-age
Cookie的有效期
**Expires**
该Cookie被删除时的时间戳，格式为GMT,若设置为以前的时间，则该Cookie立刻被删除，并且该时间戳是服务器时间，不是本地时间！
若不设置则默认页面关闭时删除该Cookie。
**Max-age**
单位为秒，即多少秒之后失效，若设置为0，则立刻失效，设置为负数，则在页面关闭时失效。
默认为-1

### Size
Cookie的大小
超过限制之后会被忽略，且永远不会被设置
不同浏览器的cookie总大小不一致

|浏览器|cookie最大条数|cookie最大长度|
|---|---|---|
|IE|50|4095|
|Chrome|150|4096|
|FireFox|50|4097|
|Safari|无限|4097|

### HttpOnly

HttpOnly 的值为true或false
如果设置为true，则不允许通过脚本 document.cookie 去更改这个值，同样这个值在 document.cookie 中也不可见，但在请求时依旧会携带此cookie

### Secure

cookie的安全属性
如果设置为true，则浏览器只会在https和ssl等安全协议中传输此cookie，不会在不安全的http协议中传输此cookie

### SameSite

用来限制第三方 Cookie，从而减少安全风险
它有3个值
- Strict：完全禁止第三方Cookie，跨站点时，任何情况下都不会发送Cookie
- Lax：默认值。除了下面三种情况外，不发送第三方 Cookie
    - 链接：`<a href="..."></a>`
    - 预加载请求：`<link rel="prerender" href="..."/>`
    - GET 表单：`<form method="GET" action="...">`
- None：跨站都发送 Cookie

### Priority

优先级，定义了三种优先级，Low/Medium/High
当cookie数量超出时，低优先级的cookie会被优先清除。