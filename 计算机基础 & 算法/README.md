- [1、说一说数组和链表有哪些区别？](#说一说数组和链表有哪些区别)
- [2、请用一句话描述冒泡排序，冒泡排序的时间复杂度最好和最坏情况是多少？](#请用一句话描述冒泡排序冒泡排序的时间复杂度最好和最坏情况是多少)
- [3、如何判断一个链表是否是循环链表？](#如何判断一个链表是否是循环链表)
- [4、解释一下什么是进程和线程？](#解释一下什么是进程和线程)
- [5、如何实现对一个数组去重？](#如何实现对一个数组去重)

<br>
<br>

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
const uniqueArray = Array.from(
  new Map(array.map((item, index) => [item, index])).keys(),
);
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
    (a, b) => b.lastModified - a.lastModified,
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

  while (queue.length > 0) {
    const node = queue.shift()!;
    result.push(node.id);
    if (node.children && node.children.length > 0) {
      queue.push(...node.children);
    }
  }

  return result;
}
```

#### 给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串 s ，判断字符串是否有效,例：

输入：() -> 返回 true <br>
输入：()[]{} -> 返回 true <br>
输入：(] -> 返回 false <br>
输入：([)] -> 返回 false <br>
输入：{[]} -> 返回 true <br>

```javascript
const isValidString = (s) => {
  const map = new Map();
  map.set(")", "(");
  map.set("}", "{");
  map.set("]", "[");

  const stack = [];

  for (let char of s) {
    if (!map.has(char)) {
      stack.push(char);
    } else {
      if (stack.pop() !== map.get(char)) {
        return false;
      }
    }
  }

  return stack.length === 0;
};
```

#### 请完成注释中的要求

```typescript
declare const loadImage: (url: string) => Promise<string>;
/**
 * 获取图片
 * @param {string[]} urls 图片的路径
 * @param {number} limit 同时能获取的个数
 * @return  {Promise<string[]>}
 */

const loadImages = async (urls: string[], limit: number): Promise<string[]> => {
  const state = {
    i: 0,
  };
  const imgStrs: string[] = new Array(urls.length);

  const promises = new Array(limit)
    .fill(0)
    .map(() => loadLimitImage(state, urls, imgStrs));
  await Promise.all(promises);

  return imgStrs;
};

const loadLimitImage = async (
  state: { i: number },
  urls: string[],
  imgStrs: string[],
) => {
  while (state.i < urls.length) {
    const currentIndex = state.i++;
    try {
      const res = await loadImage(urls[currentIndex]);
      imgStrs[currentIndex] = res;
    } catch (err) {
      imgStrs[currentIndex] = "";
    }
  }
};
```

#### 输出数组中出现次数最多的元素，以及它的次数

```javascript
const arr = [1, 2, 3, 4, 5, 6, 7, 2, 2, 2, 2, 4];
const calculateCount = (arr) => {
  const map = new Map();
  for (let num of arr) {
    if (map.has(num)) {
      map.set(num, map.get(num) + 1);
    } else {
      map.set(num, 1);
    }
  }

  let maxKey = null;
  let maxCount = 0;
  for (let [num, count] of map) {
    if (count > maxCount) {
      maxKey = num;
      maxCount = count;
    }
  }

  return { maxKey, maxCount };
};

console.log(calculateCount(arr));
```

#### 谈一谈什么是强缓存和协商缓存？

强缓存是浏览器直接使用本地缓存，不向服务器发起任何请求，只有当缓存过期后，才会去请求服务器；<br>
协商缓存则是浏览器先向服务器发送请求，验证本地缓存是否有效，服务器决定是否返回新资源；

#### 请你完成下面的算法题

<img width="686" height="688" alt="image" src="https://github.com/user-attachments/assets/60ca6e22-4ee6-4fd9-8b02-063794502e1e" />

```javascript
const intToRoman = (num) => {
  const map = new Map([
    [1000, "M"],
    [900, "CM"],
    [500, "D"],
    [400, "CD"],
    [100, "C"],
    [90, "XC"],
    [50, "L"],
    [40, "XL"],
    [10, "X"],
    [9, "IX"],
    [5, "V"],
    [4, "IV"],
    [1, "I"],
  ]);

  let result = "";
  for (let [value, symbol] of map) {
    while (num >= value) {
      result += map.get(value);
      num -= value;
    }
  }

  return result;
};
```

#### 请你依据数组构建一棵二叉树

```javascript
// DFS
const arr = [1, 2, 3, 4, 5, 6, 7];

class TreeNode {
  constructor(val) {
    ((this.rootVal = val), (this.left = null), (this.right = null));
  }
}

const buildBinaryTree = (arr, index = 0) => {
  if (arr.length === 0) return null;
  if (index >= arr.length || arr[index] === null) return null;

  const node = new TreeNode(arr[index]);

  node.left = buildBinaryTree(arr, index * 2 + 1);
  node.right = buildBinaryTree(arr, index * 2 + 2);

  return node;
};

console.log(buildBinaryTree(arr));

// 层次遍历
const arr = [1, 2, 3, 4, 5, 6];

class TreeNode {
  constructor(val) {
    ((this.rootVal = val), (this.left = null), (this.right = null));
  }
}

const buildBinaryTree = (arr) => {
  if (arr.length === 0) return null;

  const binaryTree = new TreeNode(arr[0]);
  const queue = [binaryTree];
  let i = 0;

  while (i < arr.length) {
    const node = queue.shift();

    if (i < arr.length - 1) {
      node.left = new TreeNode(arr[++i]);
      queue.push(node.left);
    }

    if (i < arr.length - 1) {
      node.right = new TreeNode(arr[++i]);
      queue.push(node.right);
    }
  }

  return binaryTree;
};

console.log(buildBinaryTree(arr));
```

#### 实现fetchWithCache(url, fetcher, ttl)
要求：<br>
- 相同url并发请求去重<br>
- 成功缓存ttl毫秒<br>
- 失败不缓存<br>

```javascript
const promiseMap = new Map();
const dataMap = new Map();

const fetchWithCache = (url, fetcher, ttl) => {
  if (promiseMap.get(url)) {
    return promiseMap.get(url);
  }

  if (dataMap.get(url) && Date.now() - dataMap.get(url).timeStamp < ttl) {
    return Promise.resolve(dataMap.get(url).data);
  }

  const promise = (async () => {
    try {
      const res = await fetcher();
      dataMap.set(url, {
        data: res,
        timeStamp: Date.now(),
      });
      promiseMap.delete(url);
      return res;
    } catch (err) {
      console.log(err);
      promiseMap.delete(url);
      throw new Error(err);
    }
  })();

  promiseMap.set(url, promise);

  return promise;
};

(async () => {
  const result = await Promise.all([
    fetchWithCache("https://example.com", () => Promise.resolve(111), 5000),
    fetchWithCache("https://example.com", () => Promise.resolve(222), 5000),
  ]);

  console.log(result);
})();
```
