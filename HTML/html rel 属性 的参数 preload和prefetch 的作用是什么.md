#HTML

rel属性定义了所链接的资源与当前文档的关系
例如
- icon，表示当前文档的图标
- stylesheet，导入样式表
- prefetch，为了提示浏览器，用户未来的浏览有可能需要加载目标资源，所以浏览器有可能通过事先获取和缓存对应资源，优化用户体验
- preload，允许你在 HTML 的 [`<head>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/head) 中声明获取请求，指定页面很快就需要的资源，这些资源是你希望在页面生命周期的早期就开始加载的，早于浏览器的主要渲染机制启动


---
``` html
<link rel="stylesheet" href="styles/main.css" />

<link rel="preload" href="style.css" as="style" />
```
最常使用 `<link>` 标签来加载一个 CSS 文件
然而，在这里，我们将使用值为 `preload` 的 `rel` 属性，这会将 `<link>` 标签转变成任何我们想要的资源的预加载器
你还需要指定：
- [`href`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/link#href) 属性中的资源路径。
- [`as`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/link#as) 属性中的资源类型。

---


- preload 告诉浏览器立即加载资源
- prefetch 告诉浏览器在空闲时才开始加载资源
- ==preload是提前加载当前页面的资源，prefetch是在空闲时加载以后页面可能会用到的资源==
- ==preload的优先级高于prefetch —— 当前页面比下一页更重要==

preload、prefetch 仅时加载资源，并不会执行
在使用 `preload`、`prefetch` 加载资源时，如果发生了页面跳转，此时没有完成的请求将会被取消掉
当页面中实际用到的资源与 `preload`、`prefetch` 加载的资源重复时，浏览器不会进行重复请求
prefetch 它是用于预取将在下一次导航/页面加载时使用的资源（例如，当你跳转到下一页时）。这是可以的，但对于当前页面没有用
