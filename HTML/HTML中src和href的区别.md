#HTML 

==简单来说 src 就是 “我想加载这个资源”，而 href 就是 “我想和这个资源建立关联”==
- src 主要用于元素替换
- href 用于和相关文档和外部资源建立相关链接

src(Source)是指向物件的来源地址，是引入，在 img、script、iframe 等元素上使用

href(Hypertext Reference)是超文本引用，指向需要连结的地方，是与该页面有关联的，是引用，在 link和a 等元素上使用

**src**是source的缩写，是指向外部资源的位置，指向的内部会迁入到文档中当前标签所在的位置；在请求**src**资源时会将其指向的资源下载并应用到当前文档中，例如js脚本，img图片和frame等元素。

---

<script src="js.js"></script>当浏览器解析到这一句的时候会暂停其他资源的下载和处理，直至将该资源加载，编译，执行完毕，图片和框架等元素也是如此，类似于该元素所指向的资源嵌套如当前标签内，这也是为什么要把js饭再底部而不是头部。

<link href="common.css" rel="stylesheet"/>当浏览器解析到这一句的时候会识别该文档为css文件，会下载并且不会停止对当前文档的处理，这也是为什么建议使用link方式来加载css而不是使用@import。