#JavaScript 
> file:///D:/Document/WeChat/WeChat%20Files/wxid_1fyk8gebq5z622/FileStorage/File/2023-07/1.JavaScript%E9%9D%A2%E8%AF%95%E7%9C%9F%E9%A2%98-210%E9%A1%B5(4).pdf
> 31

- XSS（Cross Site Scripting）跨站脚本攻击
- CSRF（Cross-site request forgery）跨站请求伪造
- SQL注入


## XSS
攻击者将恶意代码植入到提供给其他用户使用的页面中
攻击目标是为了盗取存储在客户端的cookie或者其他敏感信息
一旦获取到合法用户的信息后，攻击者就可以假冒合法用户与网站进行交互

XSS攻击可以分为
- 存储型
- 反射型
- DOM型

预防
XSS攻击有两大要素
- 攻击者提交恶意代码
- 浏览器执行恶意代码

