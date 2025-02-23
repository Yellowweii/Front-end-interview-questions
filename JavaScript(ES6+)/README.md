- [1、js 基本数据类型，复杂数据类型有哪些？它们有什么区别？](#js-基本数据类型复杂数据类型有哪些它们有什么区别)
- [2、往数组中插入一个元素有哪些方法？](#往数组中插入一个元素有哪些方法)
- [3、操作数组的常用方法有哪些？](#操作数组的常用方法有哪些)
- [4、如何判断一个对象是否是空对象？](#如何判断一个对象是否是空对象)
- [5、如何判断一个数据的数据类型？](#如何判断一个数据的数据类型)
- [6、说一说你对闭包的理解](#说一说你对闭包的理解)
- [7、var 和 let、const 的区别？什么是变量提升？](#var-和-let-const-的区别什么是变量提升)
- [8、介绍节流防抖原理以及应用，并手写一个防抖/节流函数](#介绍节流防抖原理以及应用并手写一个防抖节流函数)
- [9、JavaScript 中作用域和作用域链是什么意思？](#javascript-中作用域和作用域链是什么意思)
- [10、箭头函数和普通函数的区别？](#箭头函数和普通函数的区别)
- [11、聊一聊 js 中的事件循环](#聊一聊-js-中的事件循环)
- [12、对原型、原型链的理解](#对原型-原型链的理解)
<br>
<br>

#### js 基本数据类型，复杂数据类型有哪些？它们有什么区别？

基本数据类型：Number,String,Boolean,null,undefined<br>
BigInt:表示任意精度的整数<br>
Symbol:表示唯一且不可变的值，通常表示对象属性的键名<br>
复杂数据类型：Object,Array,Function<br>
区别：存储位置不同，简单数据类型存储在栈区，复杂数据类型存储在堆区

#### 往数组中插入一个元素有哪些方法？

1、Array.push()<br>
2、Array.unshift()<br>
3、Array.splice()方法可以在数组中的任意位置插入、删除元素.<br>
语法：<br>
array.splice(startIndex, deleteCount, item1, item2, ..., itemN)<br>
startIndex：从哪个索引开始操作。<br>
deleteCount：要删除的元素个数（如果为 0，则不删除元素）。<br>
item1, item2, ..., itemN：要插入的元素。<br>
4、使用索引直接赋值：arr[0] = 1; arr[1] = 2;<br>
5、Array.concat()方法将两个或多个数组合并成一个新的数组。它不会改变原来的数组，而是返回一个新数组。<br>
语法：<br>
array.concat(value1, value2, ..., valueN)<br>
let arr = [1, 2, 3];<br>
let newArr = arr.concat(4); // [1,2,3,4]<br>
6、展开运算符：let newArr = [...array, element]

#### 操作数组的常用方法有哪些？

arr.push()，arr.pop()，arr.shift()，arr.unshift()<br>
arr.splice()：向数组中添加、删除或替换元素。它可以删除指定位置的元素，也可以添加新的元素<br>
const newArr = Array.from(arr)：从类数组对象创建一个新的数组实例<br>
arr.indexOf()：返回数组中某个指定元素的第一个索引，如果不存在，则返回-1<br>
arr.includes()：判断数组是否包含某个元素，返回 true 或 false。<br>
arr.find()：返回数组中满足条件的第一个元素，若没有找到则返回 undefined。<br>
const newArr = arr.filter()：创建一个新数组，包含所有满足条件的元素<br>
arr.forEach()：对数组中的每个元素执行指定的回调函数<br>
const newArr = arr.map()：创建一个新数组，其中的元素是通过调用指定函数处理原数组的每个元素得到的<br>
arr.some()：检查数组中是否有至少一个元素满足条件，返回布尔值<br>
arr.every()：检查数组中是否所有元素都满足指定条件，返回布尔值<br>
arr.reduce()：对数组中的每个元素执行指定的回调函数，返回一个单一的值。通常用于累加<br>
arr.sort()：对数组中的元素进行排序，默认是按字典顺序排序<br>
arr.reverse()：反转数组中的元素顺序<br>
arr.join()：将数组中的元素连接成一个字符串，可以指定分隔符<br>
const newArr = arr1.concat(arr2)：合并两个或多个数组，返回新数组<br>
const newArr = arr.slice()返回一个数组的子数组（浅拷贝）

#### 如何判断一个对象是否是空对象？

1、使用 Object.keys()/Object.values()方法：Object.keys()/Object.values()会返回一个数组，数组中包含对象 obj 的所有属性名/属性值。如果返回的数组长度为 0，则表示对象为空<br>
2、使用 JSON.stringify()方法：通过将对象转换为 JSON 字符串，空对象会被转换成 "{}"，而有属性的对象则是一个包含内容的 JSON 字符串。可以通过比较转换后的字符串是否等于 "{}" 来判断对象是否为空。<br>
3、使用 for...in 遍历对象：如果对象没有任何可枚举属性，则不会进入循环体。你可以通过这种方式判断对象是否为空。<br>
4、使用 Object.getOwnPropertyNames()方法：Object.getOwnPropertyNames() 返回一个数组，数组包含对象的所有自有属性的键名。通过检查该数组的长度是否为 0 来判断对象是否为空。

#### 如何判断一个数据的数据类型？

1、使用 typeof<br>
console.log(typeof 123); // 'number'<br>
console.log(typeof 'hello'); // 'string'<br>
console.log(typeof true); // 'boolean'<br>
console.log(typeof undefined); // 'undefined'<br>
2、使用 instanceof<br>
console.log([] instanceof Array); // true<br>
console.log({} instanceof Object); // true<br>
3、Array.isArray()<br>
console.log(Array.isArray([1, 2, 3])); // true<br>
console.log(Array.isArray('hello')); // false<br>
4、使用 constructor 属性<br>
console.log([].constructor === Array); // true<br>
console.log(({}).constructor === Object); // true<br>
5、使用 Object.prototype.toString.call()：<br>
Object.prototype.toString.call() 中，call()被用来指定 this，即我们可以将任意类型的值作为参数传给 Object.prototype.toString()，以便获取该值的类型。

#### 说一说你对闭包的理解

闭包是内层函数用到了外层函数的局部变量，闭包的作用是函数外部可以访问函数内部的变量，从而实现数据的私有，闭包不会被垃圾回收机制回收，会造成内存泄漏的问题。

#### var 和 let、const 的区别？什么是变量提升？

var 是 ES5 的语法，var 修饰的变量存在变量提升；let、const 是 ES6 的语法，let,const 修饰的变量具有块级作用域，同样也存在变量提升，但只会将它们提升到暂时性死区，在初始化之前访问会抛出异常。<br>
变量提升指的是无论变量或函数在哪里声明，它们都会在代码执行之前被提前处理，变量的声明和函数的声明都会被提升到当前作用域的最前面

#### 介绍节流防抖原理以及应用，并手写一个防抖/节流函数

防抖是在一定时间内，多次频繁触发，只执行最后一次的操作；节流是在一定时间内，多次频繁触发，只会执行第一次的操作。<br>
应用：<br>
1、用户输入：当用户输入时，防止频繁发送请求<br>
2、窗口大小变化：防止因调整窗口大小时频繁计算布局。<br>
3、按钮点击：防止在短时间内重复点击按钮，避免多次请求。

```javascript
//防抖
function debounce(fn, delay) {
  let timer;
  return function () {
    if (timer) clearTimeout(timer);
    timer = setTimeout(fn, delay);
  };
}
//节流
function throttle(fn, delay) {
  let timer = null;
  return function () {
    if (!timer) {
      setTimeout(() => {
        fn();
        timer = null;
      }, delay);
    }
  };
}
```

#### JavaScript 中作用域和作用域链是什么意思？

作用域指的是一个变量或函数在程序中可以被访问的区域或范围。JavaScript 的作用域有全局作用域和局部作用域。<br>
作用域链是 JavaScript 用来查找变量的机制。当访问一个变量时，JavaScript 会通过作用域链沿着函数嵌套关系进行查找，直到找到变量或者到达全局作用域为止。

#### 箭头函数和普通函数的区别？

1、语法差异：箭头函数使用 => 语法定义，通常比普通函数更加简洁。<br>
2、this：箭头函数没有自己的 this，通常和外层函数的 this 指向保持一致；普通函数的 this 指向函数的调用者。<br>
3、构造函数：箭头函数不能作为构造函数使用，它不能用 new 关键字来创建实例，没有原型对象 prototype；普通函数可以作为构造函数使用，能够通过 new 创建实例。<br>
4、arguments 对象： 箭头函数没有 arguments 对象，如果需要 arguments，可以使用剩余参数来代替。普通函数有自己的 arguments 对象，包含传递给函数的所有参数。

#### 聊一聊 js 中的事件循环

事件循环是 js 处理同步任务和异步任务的一种机制，因为 js 是单线程语言，一次只能执行一行代码，为了避免异步任务阻塞主线程，js 引擎在遇到 Promise 对象的成功回调函数后，会放入微任务队列，遇到 setTimeout、setInterval、I/O 操作等会将它们放入宏任务队列，遇到同步任务时会放入执行栈中依次执行，待执行栈中的同步代码执行完后，会先不断地轮询查看是否有微任务，如果有就会把它们放到执行栈中执行，如果没有，再轮询查看宏任务队列，执行其中的代码。

#### 对原型、原型链的理解

每个对象都有原型\_\_proto\_\_，它指向该对象构造函数的原型对象 prototype。如果访问对象的某个属性或方法时，首先会检查该对象自身是否有。如果没有，就会沿着原型链向上查找，直到找到为止，或者到达 null。
通过原型链，子对象可以继承父对象的属性和方法。
