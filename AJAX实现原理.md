#JavaScript 
通过`XMLHttpRequest`对象向服务器发动异步请求
1. 实例化`XMLHttpRequest`对象
2. 通过`open`方法与服务器建立连接
3. 通过`send`方法向服务器发送消息
4. 绑定`onreadystatechange`事件，监听服务器通信状态
5. 通过responseText获取结果

XMLHttpRequest.readyState属性有5种状态
- UNSENT  open方法为调用
- OPENED  send方法未调用
- HEADERS_RECEIVED  send方法已调用
- LOADING responseText已获取部分数据
- DONE 请求完毕
