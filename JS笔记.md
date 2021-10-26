# JavaScript 学习笔记
## 变量
### 使用var声明变量
var声明的变量作用域只有两种，全局作用域和函数作用域。
在函数外用var声明的变量作用域为全局。而在函数内用var声明的变量作用域为该函数。
```js
var x = 3;
var y = 4;
var z = x + y;
```
### 使用let声明变量(ES6后添加)
let声明的变量作用域为块级，在当前块{}声明的变量只在当前块起作用。
声明全局变量时和var效果几乎相同。

### let和var的区别：
1. **var声明的全局变量属于windows对象**，而**let声明的全局变量不属于windows对象**。
   ```js
   var food = "carrot"
   //可以使用window.food访问变量
   ```
   ```js
   let food = "carrot"
   //不能使用window.food访问变量
   ```
2. **重置变量**

   使用var声明的变量在任何地方都可以修改
   ```js
   var food = "banana";
   //现在food为"banana"
   var food = "carrot";
   //现在food为"carrot"
   ```
   在相同的作用域块级作用域中，不能用let重置var或let声明的变量
   ```js
   var x = 2;
   let x = 3;//不合法
   {
       let x = 3;
       let x = 4;//不合法
   }
   ```
3. **变量提升**

   var定义的变量可以先使用再声明。而let定义的变量必须先声明再使用
   ```js
   x = 3;
   var x;//合法
   ```
   ```js
   x = 3//不合法
   let x = 3;
   ```
### 使用const声明常量(ES6后添加)
const和let几乎一致，而const用来定义常量，声明的常量必须初始化，之后不能再赋值修改。
```js
const x;//不合法
const x = 3;//合法
```
ps：尽管常量赋值后不能在更改。但常量表示数组或对象等时，数组或对象的内容依旧是可以修改的。你可以理解成c++的const指针。
### 向未声明的变量分配值
如果您把值赋给尚未声明的变量，该变量将被自动作为 window 的一个属性。
## 数据类型
JavaScript拥有动态类型，相同的变量可用作不同类型
```js
var x;//x为undefined
x = 5;//x现在为数字类型
x = "carrot"//x现在为字符串类型
```
### 值类型
#### 字符串(String)
```js
    var food1 = "banana";
    var food2 = 'carrot';
    var food3 = 'carrot is "food"';
    var food4 = "banana is 'food'";
    var food5 = "carrot is \"food\"";
    var food6 = "banana" + "is food";//可以使用+来连接字符串
    var char = food2[0];//可以通过索引位置得到字符串的每个字符
```
##### 属性
###### length
得到字符串的长度

##### 方法
###### charAt()
返回指定索引位置的字符
###### charCodeAt()
返回指定索引位置的自负的Unicode值
###### concat()
连接两个或多个字符串，返回连接后字符串。

###### 
#### 数字(Number)
JavaScript只有一种数字类型。
```js
var x1 = 3;
var x2 = 3.2;
var x3 = 1e9 + 7;
```
#### 布尔(Boolean)
布尔类型只有两个值true和false
```js
var x1 = true;
var x2 = false;
```
#### 空(Null)
可以通过将变量的值设置为null来清空变量
```js
var x = 3;//此时x为3
x = null;//此时x为null
```
#### 未定义(Undefined)
可以通过将变量的值设置为undefined来清空变量
```js
var x = 3;//此时x为3
x = undefined;//此时x为undefined
```
#### null和undefined的区别
几乎是没有区别的，
转换为数字类型时，null为0，undefined为NaN。
#### Symbol
### 引用类型
#### 对象(Object)
对象由花括号分隔。括号内，对象的属性以名称和值对的形式(name: value)来定义。属性之间用逗号分隔
```js
var person = {
    name : 'carrot',
    age : '21'
}
```
对象属性有两种访问方式
```js
var name = person.name;
var name = person['name'];
```
#### 数组(Array)
数组的下标从0开始
```js
var users = new Array();
cars[0] = 'iwriaw';
cars[1] = 'likely';
cars[2] = 'zhaoxiaotian';
```
```js
var users = new Array("iwriaw", "likely", "zhaoxiaotian");
```
```js
var users = ['iwriaw', 'likely', 'zhaoxiaotian'];
```
#### 函数(Function)
```js
function max(a, b) {
    return a > b ? a : b;
}
var talk = function() {
        return "Hello world!";
}
```
## AJAX
###  什么是 AJAX？

AJAX = Asynchronous JavaScript And XML.

AJAX 并非编程语言。

AJAX 仅仅组合了：

- 浏览器内建的 XMLHttpRequest 对象（从 web 服务器请求数据）
- JavaScript 和 HTML DOM（显示或使用数据）

Ajax 是一个令人误导的名称。Ajax 应用程序可能使用 XML 来传输数据，但将数据作为纯文本或 JSON 文本传输也同样常见。

Ajax 允许通过与场景后面的 Web 服务器交换数据来异步更新网页。这意味着可以更新网页的部分，而不需要重新加载整个页面。
### XMLHttpRequest 对象
Ajax 的核心是 XMLHttpRequest 对象。

所有现代浏览器都支持 XMLHttpRequest 对象。

XMLHttpRequest 对象用于同幕后服务器交换数据。这意味着可以更新网页的部分，而不需要重新加载整个页面。

### 跨域访问
出于安全原因，现代浏览器不允许跨域访问。

这意味着尝试加载的网页和 XML 文件都必须位于相同服务器上。

## 数据结构
### Set
Set 对象允许你存储任何类型的唯一值，无论是原始值或者是对象引用。
Set对象是值的集合，你可以按照插入的顺序迭代它的元素。 Set中的元素只会出现一次，即 Set 中的元素是唯一的。
#### 值的相等
因为 Set 中的值总是唯一的，所以需要判断两个值是否相等。在ECMAScript规范的早期版本中，这不是基于和===操作符中使用的算法相同的算法。具体来说，对于 Set s， +0 （+0 严格相等于-0）和-0是不同的值。然而，在 ECMAScript 2015规范中这点已被更改。有关详细信息，请参阅浏览器兼容性 表中的“Key equality for -0 and 0”。

另外，NaN和undefined都可以被存储在Set 中， NaN之间被视为相同的值（NaN被认为是相同的，尽管 NaN !== NaN）。

#### 构造函数
```js
Set()
```
创建一个新的Set对象。
#### 静态属性
get Set[@@species]
构造函数用来创建派生对象.
#### 实例属性
Set.prototype.size
返回 Set 对象中的值的个数

#### 实例方法
```js
Set.prototype.add(value)
```
在Set对象尾部添加一个元素。返回该Set对象。
```js
Set.prototype.clear()
```
移除Set对象内的所有元素。
```js
Set.prototype.delete(value)
```
移除Set中与这个值相等的元素，返回Set.prototype.has(value)在这个操作前会返回的值（即如果该元素存在，返回true，否则返回false）。Set.prototype.has(value)在此后会返回false。
```js
Set.prototype.entries()
```
返回一个新的迭代器对象，该对象包含Set对象中的按插入顺序排列的所有元素的值的[value, value]数组。为了使这个方法和Map对象保持相似， 每个值的键和值相等。
```js
Set.prototype.forEach(callbackFn[, thisArg])
```
按照插入顺序，为Set对象中的每一个值调用一次callBackFn。如果提供了thisArg参数，回调中的this会是这个参数。
```js
Set.prototype.has(value)
```
返回一个布尔值，表示该值在Set中存在与否。
```js
Set.prototype.keys() (en-US)
```
与values()方法相同，返回一个新的迭代器对象，该对象包含Set对象中的按插入顺序排列的所有元素的值。
```js
Set.prototype.values()
```
返回一个新的迭代器对象，该对象包含Set对象中的按插入顺序排列的所有元素的值。
```js
Set.prototype[@@iterator]()
```
返回一个新的迭代器对象，该对象包含Set对象中的按插入顺序排列的所有元素的值。
#### 示例
##### 使用Set对象
```js
let mySet = new Set();

mySet.add(1); // Set [ 1 ]
mySet.add(5); // Set [ 1, 5 ]
mySet.add(5); // Set [ 1, 5 ]
mySet.add("some text"); // Set [ 1, 5, "some text" ]
let o = {a: 1, b: 2};
mySet.add(o);

mySet.add({a: 1, b: 2}); // o 指向的是不同的对象，所以没问题

mySet.has(1); // true
mySet.has(3); // false
mySet.has(5);              // true
mySet.has(Math.sqrt(25));  // true
mySet.has("Some Text".toLowerCase()); // true
mySet.has(o); // true

mySet.size; // 5

mySet.delete(5);  // true,  从set中移除5
mySet.has(5);     // false, 5已经被移除

mySet.size; // 4, 刚刚移除一个值

console.log(mySet);
// logs Set(4) [ 1, "some text", {…}, {…} ] in Firefox
// logs Set(4) { 1, "some text", {…}, {…} } in Chrome
```
##### 迭代Set
```js
// 迭代整个set
// 按顺序输出：1, "some text", {"a": 1, "b": 2}, {"a": 1, "b": 2}
for (let item of mySet) console.log(item);

// 按顺序输出：1, "some text", {"a": 1, "b": 2}, {"a": 1, "b": 2}
for (let item of mySet.keys()) console.log(item);

// 按顺序输出：1, "some text", {"a": 1, "b": 2}, {"a": 1, "b": 2}
for (let item of mySet.values()) console.log(item);

// 按顺序输出：1, "some text", {"a": 1, "b": 2}, {"a": 1, "b": 2}
//(键与值相等)
for (let [key, value] of mySet.entries()) console.log(key);

// 使用 Array.from 转换Set为Array
var myArr = Array.from(mySet); // [1, "some text", {"a": 1, "b": 2}, {"a": 1, "b": 2}]

// 如果在HTML文档中工作，也可以：
mySet.add(document.body);
mySet.has(document.querySelector("body")); // true

// Set 和 Array互换
mySet2 = new Set([1, 2, 3, 4]);
mySet2.size;               // 4
[...mySet2];               // [1,2,3,4]

// 可以通过如下代码模拟求交集
let intersection = new Set([...set1].filter(x => set2.has(x)));

// 可以通过如下代码模拟求差集
let difference = new Set([...set1].filter(x => !set2.has(x)));

// 用forEach迭代
mySet.forEach(function(value) {
  console.log(value);
});

// 1
// 2
// 3
// 4
```
##### 实现基本集合操作
```js
function isSuperset(set, subset) {
    for (let elem of subset) {
        if (!set.has(elem)) {
            return false;
        }
    }
    return true;
}

function union(setA, setB) {
    let _union = new Set(setA);
    for (let elem of setB) {
        _union.add(elem);
    }
    return _union;
}

function intersection(setA, setB) {
    let _intersection = new Set();
    for (let elem of setB) {
        if (setA.has(elem)) {
            _intersection.add(elem);
        }
    }
    return _intersection;
}

function symmetricDifference(setA, setB) {
    let _difference = new Set(setA);
    for (let elem of setB) {
        if (_difference.has(elem)) {
            _difference.delete(elem);
        } else {
            _difference.add(elem);
        }
    }
    return _difference;
}

function difference(setA, setB) {
    let _difference = new Set(setA);
    for (let elem of setB) {
        _difference.delete(elem);
    }
    return _difference;
}
//Examples
let setA = new Set([1, 2, 3, 4]),
    setB = new Set([2, 3]),
    setC = new Set([3, 4, 5, 6]);

isSuperset(setA, setB);          // => true
union(setA, setC);               // => Set [1, 2, 3, 4, 5, 6]
intersection(setA, setC);        // => Set [3, 4]
symmetricDifference(setA, setC); // => Set [1, 2, 5, 6]
difference(setA, setC);          // => Set [1, 2]
```
##### Array 相关
```js
let myArray = ["value1", "value2", "value3"];

// 用Set构造器将Array转换为Set
let mySet = new Set(myArray);

mySet.has("value1"); // returns true

// 用...(展开操作符)操作符将Set转换为Array
console.log([...mySet]); // 与myArray完全一致
```
##### 数组去重
```js
// Use to remove duplicate elements from the array
const numbers = [2,3,4,4,2,3,3,4,4,5,5,6,6,7,5,32,3,4,5]
console.log([...new Set(numbers)])
// [2, 3, 4, 5, 6, 7, 32]
```
##### String 相关
```js
let text = 'India';

let mySet = new Set(text);  // Set {'I', 'n', 'd', 'i', 'a'}
mySet.size;  // 5

// 大小写敏感 & duplicate ommision
new Set("Firefox")  // Set(7) [ "F", "i", "r", "e", "f", "o", "x" ]
new Set("firefox")  // Set(6) [ "f", "i", "r", "e", "o", "x" ]
```

### Map
Map 对象保存键值对，并且能够记住键的原始插入顺序。任何值(对象或者原始值) 都可以作为一个键或一个值。

一个Map对象在迭代时会根据对象中元素的插入顺序来进行 — 一个  for...of 循环在每次迭代后会返回一个形式为[key，value]的数组。

#### 键的相等(Key equality)
- 键的比较是基于 sameValueZero 算法：
- NaN 是与 NaN 相等的（虽然 NaN !== NaN），剩下所有其它的值是根据 === 运算符的结果判断是否相等。
- 在目前的ECMAScript规范中，-0和+0被认为是相等的，尽管这在早期的草案中并不是这样。

#### Objects 和 maps 的比较
Objects 和 Maps 类似的是，它们都允许你按键存取一个值、删除键、检测一个键是否绑定了值。因此（并且也没有其他内建的替代方式了）过去我们一直都把对象当成 Maps 使用。不过 Maps 和 Objects 有一些重要的区别，在下列情况里使用 Map 会是更好的选择：

|          | Map                                                                            | Object                                                                             |
| -------- | ------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------- |
| 意外的键 | Map 默认情况不包含任何键。只包含显式插入的键。                                 | 一个 Object 有一个原型, 原型链上的键名有可能和你自己在对象上的设置的键名产生冲突。 |
| 键的类型 | 一个 Map的键可以是任意值，包括函数、对象或任意基本类型。                       | 一个Object 的键必须是一个 String 或是Symbol。                                      |
| 键的顺序 | Map 中的 key 是有序的。因此，当迭代的时候，一个 Map 对象以插入的顺序返回键值。 | 一个 Object 的键是无序的                                                           |
| Size     | Map 的键值对个数可以轻易地通过size 属性获取                                    | Object 的键值对个数只能手动计算                                                    |
| 迭代     | Map 是 iterable 的，所以可以直接被迭代。                                       | 迭代一个Object需要以某种方式获取它的键然后才能迭代。                               |
| 性能     | 迭代一个Object需要以某种方式获取它的键然后才能迭代。                           | 在频繁添加和删除键值对的场景下未作出优化。                                         |

#### 构造函数
```js
Map()
```
创建Map对象
#### 属性
##### Map.length
属性 length 的值为 0 。

想要计算一个Map 中的条目数量， 使用 Map.prototype.size.
##### get Map[@@species]
本构造函数用于创建派生对象。
##### Map.prototype (en-US)
表示 Map 构造器的原型。 允许添加属性从而应用于所有的 Map 对象。
#### 实例方法
```js
Map.prototype.clear()
```
清空Map
```js
Map.prototype.delete(key)
```
如果该键存在则删除该键值对并返回true，否则返回false。
```js
Map.prototype.get(key)
```
返回改键所对应的值，如果该键不存在，则返回undefined
```js
Map.prototype.has(key)
```
如果该键存在则返回true，否则返回false
```js
Map.prototype.set(key, value)
```
设置该键所对应的值（添加或更新）。返回该Map对象
##### 迭代方法
```js
Map.prototype[@@iterator]()
```
返回一个包含[key, value]的数组的新迭代器对象
```js
Map.prototype.keys()
```
返回一个包含所有key的数组（按插入顺序排列）的新迭代器对象
```js
Map.prototype.values()
```
返回一个包含所有value的数组（按插入顺序排列）的新迭代器对象
```js
Map.prototype.entries()
```
返回一个包含所有[key, value]的数组（按插入顺序排列）的新迭代器对象
```js
Map.prototype.forEach(callbackFn[, thisArg])
```
按照插入顺序，为Set对象中的每个[key, value]调用一次callBackFn。如果提供了thisArg参数，回调中的this会是这个参数。
#### 示例
```js
let myMap = new Map();

let keyObj = {};
let keyFunc = function() {};
let keyString = 'a string';

// 添加键
myMap.set(keyString, "和键'a string'关联的值");
myMap.set(keyObj, "和键keyObj关联的值");
myMap.set(keyFunc, "和键keyFunc关联的值");

myMap.size; // 3

// 读取值
myMap.get(keyString);    // "和键'a string'关联的值"
myMap.get(keyObj);       // "和键keyObj关联的值"
myMap.get(keyFunc);      // "和键keyFunc关联的值"

myMap.get('a string');   // "和键'a string'关联的值"
                         // 因为keyString === 'a string'
myMap.get({});           // undefined, 因为keyObj !== {}
myMap.get(function() {}); // undefined, 因为keyFunc !== function () {}
```
#### 将 NaN 作为 Map 的键
NaN 也可以作为Map对象的键。虽然 NaN 和任何值甚至和自己都不相等(NaN !== NaN 返回true)，但下面的例子表明，NaN作为Map的键来说是没有区别的:
```js
let myMap = new Map();
myMap.set(NaN, "not a number");

myMap.get(NaN); // "not a number"

let otherNaN = Number("foo");
myMap.get(otherNaN); // "not a number"
```

#### 使用 for..of 方法迭代 Map
Map可以使用for..of循环来实现迭代：
```js
let myMap = new Map();
myMap.set(0, "zero");
myMap.set(1, "one");
for (let [key, value] of myMap) {
  console.log(key + " = " + value);
}
// 将会显示两个log。一个是"0 = zero"另一个是"1 = one"

for (let key of myMap.keys()) {
  console.log(key);
}
// 将会显示两个log。 一个是 "0" 另一个是 "1"

for (let value of myMap.values()) {
  console.log(value);
}
// 将会显示两个log。 一个是 "zero" 另一个是 "one"

for (let [key, value] of myMap.entries()) {
  console.log(key + " = " + value);
}
// 将会显示两个log。 一个是 "0 = zero" 另一个是 "1 = one"
```
#### 使用 forEach() 方法迭代 Map
Map也可以通过forEach()方法迭代：
```js
myMap.forEach(function(value, key) {
  console.log(key + " = " + value);
})
// 将会显示两个logs。 一个是 "0 = zero" 另一个是 "1 = one"
```
#### Map 与数组的关系
```js
let kvArray = [["key1", "value1"], ["key2", "value2"]];

// 使用常规的Map构造函数可以将一个二维键值对数组转换成一个Map对象
let myMap = new Map(kvArray);

myMap.get("key1"); // 返回值为 "value1"

// 使用Array.from函数可以将一个Map对象转换成一个二维键值对数组
console.log(Array.from(myMap)); // 输出和kvArray相同的数组

// 更简洁的方法来做如上同样的事情，使用展开运算符
console.log([...myMap]);

// 或者在键或者值的迭代器上使用Array.from，进而得到只含有键或者值的数组
console.log(Array.from(myMap.keys())); // 输出 ["key1", "key2"]
```

#### 复制或合并 Maps
Map 能像数组一样被复制：
```js
let original = new Map([
  [1, 'one']
]);

let clone = new Map(original);

console.log(clone.get(1)); // one
console.log(original === clone); // false. 浅比较 不为同一个对象的引用
//重要：请记住，数据本身未被克隆。
```
Map对象间可以进行合并，但是会保持键的唯一性。
```js
let first = new Map([
  [1, 'one'],
  [2, 'two'],
  [3, 'three'],
]);

let second = new Map([
  [1, 'uno'],
  [2, 'dos']
]);

// 合并两个Map对象时，如果有重复的键值，则后面的会覆盖前面的。
// 展开运算符本质上是将Map对象转换成数组。
let merged = new Map([...first, ...second]);

console.log(merged.get(1)); // uno
console.log(merged.get(2)); // dos
console.log(merged.get(3)); // three
```
Map对象也能与数组合并：
```js
let first = new Map([
  [1, 'one'],
  [2, 'two'],
  [3, 'three'],
]);

let second = new Map([
  [1, 'uno'],
  [2, 'dos']
]);

// Map对象同数组进行合并时，如果有重复的键值，则后面的会覆盖前面的。
let merged = new Map([...first, ...second, [1, 'eins']]);

console.log(merged.get(1)); // eins
console.log(merged.get(2)); // dos##
console.log(merged.get(3)); // three
```
请注意！为Map设置对象属性也是可以的，但是可能引起大量的混乱。所以尽量不要这样使用。

## 箭头函数
箭头函数表达式的语法比函数表达式更简洁，并且没有自己的this，arguments，super或new.target。箭头函数表达式更适用于那些本来需要匿名函数的地方，并且它不能用作构造函数。
### 语法
```js
(param1, param2, …, paramN) => { statements }
(param1, param2, …, paramN) => expression
//相当于：(param1, param2, …, paramN) =>{ return expression; }

// 当只有一个参数时，圆括号是可选的：
(singleParam) => { statements }
singleParam => { statements }

// 没有参数的函数应该写成一对圆括号。
() => { statements }

//加括号的函数体返回对象字面量表达式：
params => ({foo: bar})

//支持剩余参数和默认参数
(param1, param2, ...rest) => { statements }
(param1 = defaultValue1, param2, …, paramN = defaultValueN) => {
statements }

//同样支持参数列表解构
let f = ([a, b] = [1, 2], {x: c} = {x: a + b}) => a + b + c;
f();  // 6
```