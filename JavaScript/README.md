- [1、js 基本数据类型，复杂数据类型有哪些？](#js-基本数据类型复杂数据类型有哪些)
- [2、往数组中插入一个元素有哪些方法？](#往数组中插入一个元素有哪些方法)

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
