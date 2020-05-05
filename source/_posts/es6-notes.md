---
title: ES6学习笔记
date: 2019-10-10 15:21:12
tags: JavaScript
---

#### 变量的解构赋值
```javascript
function move({x = 0, y = 0} = {}) {
  return [x, y];
}

move({x: 3, y: 8}); // [3, 8]
move({x: 3}); // [3, 0]
move({}); // [0, 0]
move(); // [0, 0]
```
```javascript
function move({x, y} = { x: 0, y: 0 }) {
  return [x, y];
}

move({x: 3, y: 8}); // [3, 8]
move({x: 3}); // [3, undefined]
move({}); // [undefined, undefined]
move(); // [0, 0]
```

<!-- more -->

#### 字符串扩展
```javascript
let text = String.fromCodePoint(0x20BB7);

for (let i = 0; i < text.length; i++) {
  console.log(text[i]);
}
// " "
// " "

for (let i of text) {
  console.log(i);
}
// "𠮷"
```

#### 字符串(String)实例方法
##### includes(),startsWith()和endsWith()
传统上，JavaScript 只有indexOf方法，可以用来确定一个字符串是否包含在另一个字符串中。ES6 又提供了三种新方法。

- `includes(searchString[, position])`：返回*布尔值*，表示是否找到了参数字符串。
- `startsWith(searchString[, position])`：返回*布尔值*，表示参数字符串是否在原字符串的头部。
- `endsWith(searchString[, position])`：返回*布尔值*，表示参数字符串是否在原字符串的尾部。

```javascript
let s = 'Hello world!';
s.startsWith('world', 6) // true
```

##### repeat(count)
`repeat`方法返回一个*新字符串*，表示将原字符串重复n次。
参数如果是小数则会被向下取整
参数是负数或者Infinity，会报错。
```javascript
'x'.repeat(3) // "xxx"
'hello'.repeat(2) // "hellohello"
'na'.repeat(0) // ""

'na'.repeat(2.9) // "nana"

'na'.repeat(Infinity)
// RangeError
'na'.repeat(-1)
// RangeError
```

如果参数是 0 到-1 之间的小数，则等同于 0，这是因为会先进行取整运算。0 到-1 之间的小数，取整以后等于-0，repeat视同为 0
参数NaN等同于 0。

```javascript
'na'.repeat(-0.9) // ""
'na'.repeat(NaN) // ""
```
如果参数是字符串，则会先转换成数字。

##### padStart()，padEnd()
ES2017 引入了字符串补全长度的功能。如果某个字符串不够指定长度，会在头部或尾部补全。
`targetLength`位必选参数，`padString`为可选参数。
两个方法都返回一个在原字符串开头填充指定的填充字符串直到目标长度所形成的*新字符串*。
 - `padStart(targetLength [, padString])` 。另一个字符串填充当前字符串(重复，如果需要的话)，以便产生的字符串达到给定的长度。填充从当前字符串的开始(左侧)应用的。
 - `padEnd(targetLength [, padString])` 。另一个字符串填充当前字符串(重复，如果需要的话)，以便产生的字符串达到给定的长度。填充从当前字符串的开始(右侧)应用的。
 
 如果省略第二个参数，默认使用空格补全长度。
 ```javascript
 'x'.padStart(4) // '   x'
 'x'.padEnd(4) // 'x   '
 ```
 两个方法最常用的场景是，为数值补全指定位数
 ```javascript
 '1'.padStart(10, '0') // "0000000001"
 '12'.padStart(10, '0') // "0000000012"
 '123456'.padStart(10, '0') // "0000123456"
 ```
 另一使用场景是提示字符串格式。(其实并不常用)
 ```javascript
 '12'.padStart(10, 'YYYY-MM-DD') // "YYYY-MM-12"
 '09-12'.padStart(10, 'YYYY-MM-DD') // "YYYY-09-12"
 ```
 ##### trimStart()，trimEnd()
 ES2019 对字符串实例新增了`trimStart()`和`trimEnd()`这两个方法，它们的行为与`trim()`一致，`trimStart()`消除字符串头部的空格，`trimEnd()`消除尾部的空格。
 它们返回的都是新字符串，*不会修改原始字符串*。
 
 除了空格键，这两个方法对字符串头部（或尾部）的 tab 键、换行符等不可见的空白符号也有效。
 
 浏览器还部署了额外的两个方法，`trimLeft()`是`trimStart()`的别名，`trimRight()`是`trimEnd()`的别名。
 ##### matchAll()
 matchAll()方法返回一个正则表达式在当前字符串的所有匹配(暂时不理解，正则相关需另起一章)
 
 
 ##### 最后整理的的零碎小东西
 1. `Math.max()和Math.min()`
这两个方法在ES6中改进了，原先不允许传入数组，ES6之后可支持数组。
早前如果想要用这两个方法得出数组的最大和最小值，需要这样写：
```
var values = [12, 15, 0, 20, -1];
var max = Math.max.apply(Math, values);// 20
```
但是在ES6中我们可以这样写：
用于ES6使用了展开运算符“...”,JavaScript引擎读取后会将参数数组分割为各自独立的参数并依次传入：
```
let values = [12, 15, 0, 20, -1];
let max1 = Math.max(...values);//20
let min1 = Math.min(...values);//-1
let max2 = Math.max(...values, 100)//100

```
