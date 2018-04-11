##   JS中的函数
> 函数是指一段在一起的、可以做某一件事情的程序。也叫子程序（OOP中的）方法。
> 函数是实现某一个功能的方法


### 创建函数
```javascript
function [函数名](){
  // => [函数体]
  // 实现功能的具体JS代码
}

```

### 执行函数
```javascript
函数名(); // => 把创建的函数执行，而且这个函数可以执行很多次
函数名(); // => 第二次执行
...
每一次执行都相当于把函数体中实现功能的代码重伏执行了一遍
```

> 在正常的项目中，我们一般都会把实现一个具体功能的代码封装在函数中：
> 1、如果当前这个功能需要在页面中执行多次，不封装成函数，每一次想实现这个功能，都需要把代码重新写一遍，浪费时间；而封装在一个函数中，以后想多次实现这个功能，我们就没必要在重新的写代码了，只需要把函数重新执行即可，提高了开发效率。
> 2、封装在一个函数中，页面中就基本上很难出现重复一样的代码了，减少了页面中代码的冗余度，提高了代码的重复利用率：`低耦合高内聚`
>
> 我没呢把以上的特点称为`函数封装`(OOP面向对象编程思想，需要我们掌握的就是类的继承、封装、多态)


### JS中函数的核心原理
> 函数作为JS中引用数据类型中的一种，也是按照引用地址来操作的
```javascript
var obj = {
  name:"珠峰",
  age:8
}
function sum () {
  var total = 1 + 1;
  total *=20;
  console.log(total.toFixed(2));
}
sum();
```
`创建函数`
- 首先会在当前作用域中声名一个函数名(声明的函数名和var声明的变量名是一样的操作:var sum; function sum; 这两个名字算重复了)
- 浏览器首先会开辟一个新的内存空间(分配一个十六进制地址)，把函数体中写好的代码当作普通字符串存储在这个空间当中(创建一个函数如果不执行，函数没有意义)
- 把内存空间的地址赋值给之前声明的那个函数名

`函数执行`
> 目的：把之前存储的实现具体功能的JS代码执行
  - 函数执行，浏览器会为其开辟一个新的`私有作用域`(只能执行函数中之前编写的JS代码)
  - 形参赋值(先跳过)
  - 私有作用域中的变量提升(先跳过)
  - 把之前创建的时候存储的JS代码字符串拿到私有作用域中，然后把他们变为JS表达式从下到下执行
  - 私有作用是否销毁的问题(先跳过)

`闭包`
> 函数执行的时候会形成一个私有作用域，让里面的私有变量和外界互不影响(相互不干扰、外面的无法获取里面的变量值)，此时我们可以理解为私有作用域把私有变量保护起来，我们把这个保护机制称之为`闭包`

`栈内存`
> 作用域(全局作用域，私有作用域)：提供一个供JS代码执行的环境

`堆内存`
> 所有的引用数据类型，他们需要存储的内容都在堆内存中(相对于一个创库，目的存储信息)
> - 对象会把键值对存储起来
> - 函数会把代码当作键值对存储起来


### 函数中形参和实参
> 形参： 相当于生产洗衣机的时候提供的入口，需要用户执行函数的时候把需要的值传递进来，形参是个变量用来存储和接收这些值
> 实参：用户执行的时候传递给形参的具体值
```javascript
//=> 随便求出两个数的和
function sum(a,b){ // a,b 就是形参变量(类似var了一下)
  var total = a + b;
  total *= 10;
  total = total.toFixed(2);
  console.log(total);
}
sum(10, 20); // =>300.00 10和20是实参， a=10,b=20
sum(10);// => a=10,b=undefined 定义了形参但是执行的时候没有传递实参，默认的实参就是undefined
```

```
function sum(a,b,c,d){
  // => 如果有一个值没有传递的话，我们为了保证结果不是NAN，我么为其设置一个默认的值:0
  a = a || 0;
  b = b || 0;
  /* 扩展： 逻辑或，逻辑与方法 */
  // if(c===undefined){
  //   c = 0
  // }
  // if(typeof d === "undefined"){
  //   d = 0
  // }
  typeof c === "undefined" ? c = 0 : null;
  typeof d === "undefined" ? d = 0 : null;
  //=> 容错处理
  var total = a + b + c + d;
  total *= 10;
  total = total.toFixed(2);
  console.log(total);
}

sum(10);
```

### arguments 实参集合
> 当我们不知道用户具体要传递几个值的时候(传递几个值都行)此时我们无法设置形参的个数，遇到此类的需要用到函数内置的实参集合: arguments
> 1、arguments只有函数才有
> 2、不管执行函数的时候是否传递实参arguments天生就存在，没有传递实参ARG是个空的集合，传递了ARG中包含了所有传递的实参值
> 3、不管是否设置了形参，ARG中始终存储了所有的实参信息
> 4、arguments是一个类数组集合
  > 1. 以数字作为索引(属性值),从零开始
  > arguments[0] 第一个实参信息
  > arguments[2] 第三个实参信息
  > arguments[n] 第n+1个实参信息
  > 2. 有一个length的属性，存储的是当前几个的长度(当前传递实参的个数)
  > arguments.length
  > arguments['length']
  >
  > arguments.callee：存储的是当前函数本身
  > arguments.callee.caller: 存储的是当前函数在哪执行的(宿主函数)，在全局作用域下执行的,结果是null

  ```
  function sum() {
    console.log(arguments.callee.caller); //=> fn
  }

  function fn(){
    sum();
    sum(10,20,"珠峰",{name:"孙"});
  }
  fn();
  ```

  > 任意数求和
  ```
  function sum(){
    var total = null;
    for(var i = 0; i < arguments.length; i++) {
      var cur = Number(arguments[i]);
      !isNaN(cur) ? total += cur : null;
    }
    console.log(total);
  }
  ```

### JS中的返回值 `return`
> 返回值是函数提供的一个出口：我们如果想在外面使用函数私有的信息，那么就需要通过return，把这些信息返回出来供外面使用
```javascript
function sum(){
  var total = null;
  ...
  return total;  // RETURN后面跟着的都是值(返回的都是值):此处不是把total变量返回，而是把total存储的值返回 <==> RETURN 60;
}
console.log(sum(10,20,23));
//=>sum:代表的是函数本身
//=>sum():让函数先执行，代表的是当前函数返回结果(RETURN后面是啥，相当于函数返回的是啥)
```

```
function sum () {
  var total = 0;
  return;
  console.log(total);//=>在函数体中遇到RETURN后，RETURN后面的代码都不执行了
}

console.log(sum());//=>如果函数中没有写RETURN或者RETURN后面啥也没有，默认返回的结果就是undefined
```

> 任意数求和完整版
```
function sum(){
  var total = null;
  for(var i = 0; i < arguments.length; i++) {
    var cur = Number(arguments[i]);
    !isNaN(cur) ? total += cur : null;
  }
  return total;
}
var total = sum(10,20,30);//=>外面是全局下的TOTAL和函数中的TOTAL没有必然的联系
console.log(total.toFixed(2));
```

### JS中的匿名函数
> 没有名字的函数
> - 函数表达式
> - 自执行表达式
```javascript
oBox.onclick = function () {
  //=> 把一个没有名字(有名字也无所谓)的函数作为值复制给一个变量或者一个元素的某个事件等:·函数表达式·
}
```

```javascript
(function(n){
  //=> 创建函数和执行函数放在一起了，创建完成后立即执行:·函数表达式·
  //=> n 是形参 n=10;
})(12);

//=> 一下都是自执行函数,符号只是控制语法规范
~function(){}
-function(){}
+function(){}
!function(){}
```
