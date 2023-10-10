#HTTP

### 请求头
- **Accept**
用来告知（服务器）客户端可以处理的内容类型，这种内容类型用[MIME 类型](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Basics_of_HTTP/MIME_types)来表示
```txt
Accept: <MIME_type>/<MIME_subtype>
Accept: <MIME_type>/*
Accept: */*

// Multiple types, weighted with the [quality value](https://developer.mozilla.org/zh-CN/docs/Glossary/Quality_values) syntax:
Accept: text/html, application/xhtml+xml, application/xml;q=0.9, */*;q=0.8
```


- **Accept-Encoding**
将客户端能够理解的内容编码方式——通常是某种压缩算法——进行通知（给服务端）。通过内容协商的方式，服务端会选择一个客户端提议的方式，使用并在响应头 [`Content-Encoding`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Encoding) 中通知客户端该选择
```
Accept-Encoding: gzip
Accept-Encoding: compress
Accept-Encoding: deflate
Accept-Encoding: br
Accept-Encoding: identity
Accept-Encoding: *

// Multiple algorithms, weighted with the [quality value](https://developer.mozilla.org/zh-CN/docs/Glossary/Quality_values) syntax:
Accept-Encoding: deflate, gzip;q=1.0, *;q=0.5
```


- **Accept-Language**
**`Accept-Language`** 请求头允许客户端声明它可以理解的自然语言，以及优先选择的区域方言。借助[内容协商机制](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Content_negotiation)，服务器可以从诸多备选项中选择一项进行应用，并使用 [`Content-Language`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Language) 应答头通知客户端它的选择
```
Accept-Language: <language>
Accept-Language: *

// Multiple types, weighted with the [quality value](https://developer.mozilla.org/zh-CN/docs/Glossary/Quality_values) syntax:
Accept-Language: fr-CH, fr;q=0.9, en;q=0.8, de;q=0.7, *;q=0.5
```


- **Connection**
控制网络连接在当前会话完成后是否仍然保持打开状态。如果发送的值是 `keep-alive`，则连接是持久的，不会关闭，允许对同一服务器进行后续请求。
```
Connection: keep-alive
Connection: close
```

- **Host**
指明了请求将要发送到的服务器主机名和端口号
如果没有包含端口号，会自动使用被请求服务的默认端口（比如 HTTPS URL 使用 443 端口，HTTP URL 使用 80 端口）
```
Host: developer.mozilla.org
```

- **Referer**
包含了当前请求页面的来源页面的地址，即表示当前页面是通过此来源页面里的链接进入的
服务端一般使用 `Referer` 请求头识别访问来源，可能会以此进行统计分析、日志记录以及缓存优化等

在以下两种情况下，`Referer` 不会被发送：
- 来源页面采用的协议为表示本地文件的 "file" 或者 "data" URI；
- 当前请求页面采用的是非安全协议，而来源页面采用的是安全协议（HTTPS）
```
Referer: https://developer.mozilla.org/zh-CN/docs/Web/JavaScript
```

- **User-Agent**
用来让网络协议的对端来识别发起请求的用户代理软件的应用类型、操作系统、软件开发商以及版本号
```
User-Agent: Mozilla/<version> (<system-information>) <platform> (<platform-details>) <extensions>
```

- **Cache-Control**
被用于在 http 请求和响应中，通过指定指令来实现缓存机制。
缓存指令是单向的，这意味着在请求中设置的指令，不一定被包含在响应中。
```
Cache-Control: max-age=<seconds>
Cache-Control: max-stale[=<seconds>]
Cache-Control: min-fresh=<seconds>
Cache-control: no-cache
Cache-control: no-store
Cache-control: no-transform
Cache-control: only-if-cached
```


- **Cookie**
其中含有 先前由服务器通过 [`Set-Cookie`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Set-Cookie) 标头投放或通过 JavaScript 的 [`Document.cookie`](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/cookie) 方法设置，然后存储到客户端的 [HTTP cookie](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Cookies)
```
Cookie: PHPSESSID=298zf09hf012fh2; csrftoken=u32t4o3tb3gg43; _gat=1
```

- **Range**
告知服务器返回文件的哪一部分
通常用于断点续传
```
Range: bytes=200-1000, 2000-6576, 19000-
```


### 响应头

- **Cache-Control**
被用于在 http 请求和响应中，通过指定指令来实现缓存机制。
缓存指令是单向的，这意味着在请求中设置的指令，不一定被包含在响应中。
```
Cache-Control: max-age=<seconds>
Cache-Control: max-stale[=<seconds>]
Cache-Control: min-fresh=<seconds>
Cache-control: no-cache
Cache-control: no-store
Cache-control: no-transform
Cache-control: only-if-cached
```

- **Content-Type**
用于指示资源的 MIME 类型 [media type](https://developer.mozilla.org/zh-CN/docs/Glossary/MIME_type) 。
在响应中，Content-Type 标头告诉客户端实际返回的内容的内容类型。

- **Content-Encoding**
列出了对当前实体消息（消息荷载）应用的任何编码类型，以及编码的顺序。
它让接收者知道需要以何种顺序解码该实体消息才能获得原始荷载格式。Content-Encoding 主要用于在不丢失原媒体类型内容的情况下压缩消息数据。

- **Date**
其中包含了报文创建的日期和时间

- **Server**
包含了处理请求的源头服务器所用到的软件相关信息
```
Server: Apache/2.4.1 (Unix)
```

- **Transfer-Encoding**
**`Transfer-Encoding`** 消息首部指明了将 [entity](https://developer.mozilla.org/zh-CN/docs/Glossary/Entity_header) 安全传递给用户所采用的编码形式。

`Transfer-Encoding` 是一个[逐跳传输消息首部](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers#hbh)，即仅应用于两个节点之间的消息传递，而不是所请求的资源本身。一个多节点连接中的每一段都可以应用不同的`Transfer-Encoding` 值。如果你想要将压缩后的数据应用于整个连接，那么请使用端到端传输消息首部 [`Content-Encoding`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Encoding) 。

当这个消息首部出现在 [`HEAD`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/HEAD) 请求的响应中，而这样的响应没有消息体，那么它其实指的是应用在相应的 [`GET`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/GET) 请求的应答的值。

- **Expires**
**`Expires`** 响应头包含日期/时间，即在此时候之后，响应过期。

无效的日期，比如 0，代表着过去的日期，即该资源已经过期。

如果在[`Cache-Control`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Cache-Control)响应头设置了 "max-age" 或者 "s-max-age" 指令，那么 `Expires` 头会被忽略。
```
Expires: Wed, 21 Oct 2015 07:28:00 GMT
```


- **Last-Modified**
包含源头服务器认定的资源做出修改的日期及时间
它通常被用作一个验证器来判断接收到的或者存储的资源是否彼此一致
```
Last-Modified: Wed, 21 Oct 2015 07:28:00 GMT
```

- **Connection**

- **Etag**
**`ETag`** HTTP 响应头是资源的特定版本的标识符。
这可以让缓存更高效，并节省带宽，因为如果内容没有改变，Web 服务器不需要发送完整的响应。而如果内容发生了变化，使用 ETag 有助于防止资源的同时更新相互覆盖（“空中碰撞”）。

如果给定 URL 中的资源更改，则_一定_要生成新的 `ETag` 值。比较这些 `ETag` 能快速确定此资源是否变化。
```
ETag: "33a64df551425fcc55e4d42a148795d9f25f89d4"
ETag: W/"0815"
```


- **Refresh**

- **Access-Control-Allow-Origin**
指定了该响应的资源是否被允许与给定的[来源（origin）](https://developer.mozilla.org/zh-CN/docs/Glossary/Origin)访问资源
```
Access-Control-Allow-Origin: *
Access-Control-Allow-Origin: <origin>
Access-Control-Allow-Origin: null
```

- **Access-Control-Allow-Methods**
在对 [preflight request](https://developer.mozilla.org/zh-CN/docs/Glossary/Preflight_request).（预检请求）的应答中明确了客户端所要访问的资源允许使用的方法或方法列表
```
Access-Control-Allow-Methods: POST, GET, OPTIONS
```

- **Access-Control-Allow-Credentials**
用于在请求要求包含 credentials（[`Request.credentials`](https://developer.mozilla.org/zh-CN/docs/Web/API/Request/credentials) 的值为 `include`）时，告知浏览器是否可以将对请求的响应暴露给前端 JavaScript 代码。

当请求的 credentials 模式（[`Request.credentials`](https://developer.mozilla.org/zh-CN/docs/Web/API/Request/credentials)）为 `include` 时，浏览器仅在响应标头 `Access-Control-Allow-Credentials` 的值为 `true` 的情况下将响应暴露给前端的 JavaScript 代码。
```
Access-Control-Allow-Credentials: true
```


- **Content-Range**
显示的是一个数据片段在整个文件中的位置
```
Content-Range: bytes 200-1000/67589
```

---

https://juejin.cn/post/6844903745004765198