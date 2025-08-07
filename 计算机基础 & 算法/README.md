- [1、tcp 协议中，三次握手四次挥手是怎样的](#tcp-协议中三次握手四次挥手是怎样的)
- [2、HTTP 状态码](#http-状态码)
- [3、http 常见的请求方法？get 和 post 的区别？](#http-常见的请求方法get-和-post-的区别)
- [4、说一说 TCP 的拥塞控制](#说一说-tcp-的拥塞控制)
- [5、说一说数组和链表有哪些区别？](#说一说数组和链表有哪些区别)
- [6、请用一句话描述冒泡排序，冒泡排序的时间复杂度最好和最坏情况是多少？](#请用一句话描述冒泡排序冒泡排序的时间复杂度最好和最坏情况是多少)
- [7、如何判断一个链表是否是循环链表？](#如何判断一个链表是否是循环链表)
- [8、解释一下什么是进程和线程？](#解释一下什么是进程和线程)
- [9、如何实现对一个数组去重？](#如何实现对一个数组去重)

<br>
<br>

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

#### 说一说数组和链表有哪些区别？

1、存储方式：数组每个元素在内存中是连续存储的；链表节点在内存中可以不连续存储。（不会产生外部碎片）<br>
2、访问方式：数组支持随机访问，时间复杂度是 O(1)；链表只支持顺序查找，时间复杂度是 O(N)<br>
3、插入和删除操作：数组插入/删除需要移动元素，时间复杂度是 O(N)；链表插入/删除不需要移动元素，时间复杂度是 O(1)<br>
4、空间效率：数组存储不需要额外的指针，占用空间较少；链表存储需要额外指针，占用内存空间大；<br>
5、大小：数组在内存中存储的大小是固定的；链表存储的大小是动态分配的

#### 请用一句话描述冒泡排序，冒泡排序的时间复杂度最好和最坏情况是多少？

冒泡排序是一种通过重复比较相邻元素并交换位置，将最大/小的元素逐渐“冒泡”到数组末尾的排序算法，最好的时间复杂度是 O(N)，最坏的时间复杂度是 O(N^2)

#### 如何判断一个链表是否是循环链表？

1、快慢指针法：初始化两个快慢指针 fast 和 slow 都指向链表的头节点，快指针一次走两步，慢指针一次走一步，如果链表是线性的，那么快指针会最终会指向 null，如果是循环链表，快慢指针最终会相遇。
2、使用哈希表：遍历链表，记录每一个链表节点的引用地址，如果在遍历过程中发现某个引用地址已经存在于哈希表中，说明是循环链表。

#### 解释一下什么是进程和线程？

1、进程是正在内存中执行的一段程序，操作系统会为每一个进程分配一个 PCB，用来控制和管理进程，进程是系统资源分配和调度的一个基本单位，各个进程之间都有自己的内存空间，代码段，数据段和系统资源，相互独立互不影响。<br>
2、线程是一个基本的 CPU 执行单元，也称为轻量级进程，一个进程可以包含多个线程，线程之间共享进程的内存空间和资源

#### 如何实现对一个数组去重？

1、使用 Set 构造函数：

```javascript
const array = [1, 2, 2, 3, 4, 4, 5];
const uniqueArray = [...new Set(array)];
```

2、使用 Map 构造函数

```javascript
const array = [1, 2, 2, 3, 4, 4, 5];
const uniqueArray = Array.from(new Map(array.map((item, index) => [item, index])).keys());
```

3、使用 for/forEach()遍历数组

```javascript
const array = [1, 2, 2, 3, 4, 4, 5];
const uniqueArray = [];
array.forEach((item) => {
  if (uniqueArray.indexOf(item) === -1) {
    uniqueArray.push(item);
  }
});
```

#### 在一个文档管理系统中，有多个用户上传了同一文档的不同版本。请实现一个函数，接收一个文档列表，根据文档的内容哈希值去重，并按照最后修改时间排序。

```typescript
interface Document {
  id: string;
  contentHash: string;
  lastModified: number; // 时间戳
  fileName: string;
}

function deduplicateAndSort(documents: Document[]): Document[] {
  const hashMap = new Map<string, Document>();

  for (const doc of documents) {
    const existing = hashMap.get(doc.contentHash);
    if (!existing || doc.lastModified > existing.lastModified) {
      hashMap.set(doc.contentHash, doc);
    }
  }

  // 提取去重后的文档列表并按最后修改时间降序排序
  return Array.from(hashMap.values()).sort(
    (a, b) => b.lastModified - a.lastModified
  );
}
```

#### 请实现 flattenTree 函数

```typescript
interface TreeNode {
  id: string;
  children?: TreeNode[];
}

function flattenTree(root: TreeNode): string[] {
  // 要求：返回所有节点的 id 按层级顺序组成的数组（广度优先）
  const result: string[] = [];
  const queue: TreeNode[] = [root];

  while(queue.length > 0) {
    const node = queue.shift()!;
    result.push(node.id);
    if(node.children && node.children.length > 0) {
      queue.push(...node.children);
    }
  }

  return result;
}
```
