- [1、js 基本数据类型，复杂数据类型有哪些？](#js-基本数据类型复杂数据类型有哪些)
- [2、往数组中插入一个元素有哪些方法？](#往数组中插入一个元素有哪些方法)
- [3、操作数组的常用方法有哪些？](#操作数组的常用方法有哪些)
- [4、如何判断一个对象是否是空对象？](#如何判断一个对象是否是空对象)

<br>
<br>

#### js 基本数据类型，复杂数据类型有哪些？

基本数据类型：Number,String,Boolean,null,undefined<br>
BigInt:表示任意精度的整数<br>
Symbol:表示唯一且不可变的值，通常表示对象属性的键名<br>
复杂数据类型：Object,Array,Function

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
console.log(({}).constructor === Object); // true
