#JavaScript 
## cookie
不超过4KB的文本数据
它有一个名称、值、和其他几个用于控制cookie有效期、安全性、使用范围的可选属性组成
cookie在每次请求中都会被发送

常用属性
- Expires
- Max-Age
- Domain
- Path
- Secure


## localStorage

5MB大小限制
持久化的本地存储，除非主动删除，否则数据永远不会过期
存储的信息在用一个domain中是共享的
本页面操作了localstorage，本页面不会触发 storage事件，但是其他页面会
受同源策略影响

缺点
- 无法设置过期时间
- 只能存储字符串


## sessionStorage

与localStorage使用基本一致
区别在于一但页面关闭，数据就会被删除


## indexedDB

优点
- 操作是异步的
- 支持存储JS的对象
- 是一个数据库

缺点
- 操作繁琐

使用步骤
- 打开数据库，并开始一个事务
- 创建一个object store
- 构建一个请求来执行一些数据库操作，像是增加或提取数据
- 通过监听正确类型的DOM时间以等待操作完成


## 应用场景
- 标记用户，使用cookie
- 适合长期保存在本地的数据（token），使用localStorage
- 敏感账号一次性登录，使用sessionStorage
- 存储大量数据，富文本编辑器保存编辑历史，使用indexDB
