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
