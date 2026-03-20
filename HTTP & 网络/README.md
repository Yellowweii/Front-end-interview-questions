#### 请求头Header中有哪些字段，分别代表什么意思？

HTTP 请求头（HTTP Request Headers）是客户端在发送 HTTP 请求时附带的一组 键值对（Key: Value），用于向服务器描述客户端的信息、请求的特性以及期望的响应方式。<br>
Host https://target.com 目标服务器的域名<br>
User-Agent Chrome 客户端浏览器的信息<br>
Accept application/json 客户端可接受的响应类型<br>
Connection keep-alive 控制HTTP连接是否保持<br>
============================可能会出现============================<br>
Origin https://example.com 跨域请求会携带<br>
Authorization Bearer token 接口需要认证时需要携带<br>
Cookie sessionId=abc123 当浏览器存在cookie时会携带<br>
Content-Type application/json 指定请求体的类型，当存在请求体时会携带<br>

#### 访问跨域请求和访问同源请求有什么区别？

1、访问同源请求时，浏览器会直接发送请求，直接接收响应，不会有额外步骤；而访问跨域请求时，浏览器会做CORS校验，如果服务器没有设置允许跨域响应头Access-Control-Allow-Origin，浏览器会拦截响应<br>
2、访问跨域请求时，请求头会携带origin，代表客户端网页的域名<br>
3、如果是复杂的跨域请求，还会发送一次预检 OPTIONS 请求

#### 如何允许跨域请求？

最常用的方式就是后端设置 Access-Control-Allow-Origin 响应头<br>

#### tcp 协议中，三次握手四次挥手是怎样的

建立连接：<br>
1、客户端发送 SYN 请求，表示客户端希望建立 TCP 连接<br>
2、服务器收到客户端的 SYN 请求后，回复 SYN/ACK 报文段，表示接受连接请求并准备好建立连接。<br>
3、客户端收到服务器的 SYN-ACK 后，回复一个 ACK 确认报文段，表示连接已建立。<br>
释放连接：<br>
1、客户端发送 FIN 请求，表示客户端没有数据要发送了，但是仍然可以接收数据。<br>
2、服务器收到客户端的 FIN 请求后，发送一个 ACK 确认报文段，表示收到客户端的关闭请求。<br>
3、服务器发送 FIN 请求，表示服务器没有数据要发送了，但仍然可以接收数据。<br>
4、客户端收到服务器的 FIN 请求后，发送一个 ACK 确认报文段，表示客户端也同意关闭连接。<br>
5、客户端等待 2 个 MSL（Maximum Segment Lifetime，最大报文生存时间）后，关闭连接。

#### HTTP 状态码

2xx：表示请求成功处理<br>
3xx：重定向 {<br>
301 Moved Permanently：请求的资源已永久移动到新的 URL<br>
302 Found：请求的资源临时从另一个 URL 响应<br>
304 Not Modified：资源未修改，客户端可以使用缓存<br>
}<br>
4xx：客户端错误，即请求发送到服务器时，由于客户端请求的格式、内容或者权限等问题，导致服务器无法理解或处理请求。客户端需要检查请求并进行修正。{<br>
400 Bad Request：请求有语法错误，服务器无法理解<br>
401 Unauthorized：请求未经授权，通常是因为缺少有效的认证信息<br>
403 Forbidden：请求被拒绝，服务器禁止访问<br>
404 Not Found：请求的资源不存在,可能是请求的 URL 错误<br>
405 Method Not Allowed：请求的方法（如 GET、POST、PUT、DELETE 等）不被服务器支持或禁止<br>
}<br>
5xx：服务器错误

#### http 常见的请求方法？get 和 post 的区别？

GET, POST, PUT, DELETE<br>
区别：get 用于向服务器请求获取数据，post 用于向服务器提交数据

#### 说一说 TCP 的拥塞控制

TCP 的拥塞控制通常包括：<br>
1、慢启动：TCP 的拥塞窗口从一个最大报文段 MSS 开始，每当报文段被确认，拥塞窗口便以指数级的速度增加<br>
2、拥塞避免：当慢启动增长到一定数量时，会发生丢包现象，这时可以确定拥塞避免的阈值即为当前拥塞窗口的一半。当拥塞窗口达到阈值时，会进入拥塞避免阶段，拥塞窗口便以线性的速度增加<br>
3、快速重传和快速恢复：当 TCP 发送方在一定时间内连续收到三个重复的 ACK，发送方认为网络中的某个数据包丢失了。此时，TCP 会立即重传丢失的数据包，而不等待超时事件。随后 TCP 进入快速恢复阶段，阈值会变为当前拥塞窗口的一半，并且拥塞窗口会等于新的阈值，直接进入拥塞避免阶段而不进入慢启动阶段
