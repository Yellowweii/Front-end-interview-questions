#### 请求头Header中有哪些字段，分别代表什么意思？

HTTP 请求头（HTTP Request Headers）是客户端在发送 HTTP 请求时附带的一组 键值对（Key: Value），用于向服务器描述客户端的信息、请求的特性以及期望的响应方式。<br>
Host  https://target.com  目标服务器的域名<br>
User-Agent  Chrome  客户端浏览器的信息<br>
Accept  application/json  客户端可接受的响应类型<br>
Connection  keep-alive  控制HTTP连接是否保持<br>
==============================================可能会出现==================================================<br>
Origin  https://example.com  跨域请求会携带<br>
Authorization  Bearer token  接口需要认证时需要携带<br>
Cookie  sessionId=abc123  当浏览器存在cookie时会携带<br>
Content-Type  application/json  指定请求体的类型，当存在请求体时会携带<br>

#### 访问跨域请求和访问同源请求有什么区别？

1、访问同源请求时，浏览器会直接发送请求，直接接收响应，不会有额外步骤；而访问跨域请求时，浏览器会做CORS校验，如果服务器没有设置允许跨域响应头Access-Control-Allow-Origin，浏览器会拦截响应<br>
2、访问跨域请求时，请求头会携带origin，代表客户端网页的域名<br>
3、如果是复杂的跨域请求，还会发送一次预检 OPTIONS 请求

#### 如何允许跨域请求？

最常用的方式就是后端设置 Access-Control-Allow-Origin 响应头<br>
