#### 前端是如何实现流式输出LLM返回的响应结果的？

首先说原理：<br>
流式输出的底层是 HTTP 的 Transfer-Encoding: chunked 分块传输机制，服务端保持连接不关闭，LLM 每生成一段文字就立即写入响应流推送给客户端，而不是等全部生成完再返回。数据格式遵循 SSE（Server-Sent Events）规范，每块数据以 data: 开头，结束时发送 data: [DONE]。<br>
然后说实现：<br>
前端发请求时带上 stream: true 告诉 LLM 服务端使用流式返回，拿到响应后通过 response.body.getReader() 获取一个 ReadableStream 的读取器，在 while(true) 循环里不断调用 reader.read() 读取数据块，reader.read() 是一个 Promise，没有新数据时会挂起等待，有数据推过来才会 resolve。
每次拿到的 value 是二进制的 Uint8Array，用 TextDecoder 解码成字符串，再按换行符切割解析 SSE 格式，提取出 JSON 里的文字内容，追加到消息状态里触发 React 重新渲染，用户就能看到文字逐渐出现的打字效果。<br>
