#### 数组的基础结构
> 数组也是对象数据类型 `'typeof [] -> object'`

> 数组也有属性名，只不过属性名是数字，我们把数字属性名称之为他的索引：数组是以数字作为索引，索引从零开始，有一个length属性代表数组的长度

> 类数组：类似于数组,但是不是数组
> 1、通过getElementsByTagName获取的元素集合也是类数组
> 2、函数中的实参集合arguments也是类数组
> ...

`循环数组中的每一项`
```javascript
Array.prototype.aa = 100;

var ary = [12, 23, 34];
//=> for循环操作
for(var i = 0; i < ary.length; i++){
  console.log(ary[i])
}
//=> for in循环
for(var key in ary){
  // key:属性名（数组中的属性名是索引）
  console.log(ary[key]);
}
console.log(ary);
// => for循环只能遍历到数组私有的一些属性，而for in 循环可以把一些自定义公共属性也能遍历到
```

#### 数组中的常用方法
> 数组中有很多常用的方法，`console.log(Array.prototype)`
> 1、方法是的以一个作用
> 2、方法的形参
> 3、方法的返回值
> 4、通过此方法，原来的数组是否
  **实现数组的 增加 修改 删除**
  // => 增加
	// 1、push：向数组的末尾追加新内容
	// *		参数一到多个，任何数据类型都可以，想要给数组末尾追加什么，直接传递到push方法中即可，传递多个用逗号隔开
	// *		返回值：新增后数组的长度
	// *		原有数组改变了

	// 2、向数组开头追加新内容
	// * 	unshift
	// *	参数：需要追加的内容（可以是任何数据类型的值）
	// *	返回值：新增后数组的长度
	// * 	原来的数组改变了

	// 3、向数组的末尾追加新内容
	// *	把数组当作一个普通的对象，使用对象键值对操作，给其设置新的属性(索引)
	// *	ary[ary.length] = xxx; 向数组的末尾追加了新的内容

	// => 删除
	// 1、pop：删除数组最后一项
	// *	参数：无
	// * 	返回值：被删除的那一项内容
	// *  原有的数组改变了

	// 2、shift：删除数组第一项
	// *	参数：无
	// *	返回值：被删除的那一项的内容
	//使用shift删除第一项之后，后面每一项的索引都要向前进一位（导致后面项的索引发生改变）

	// 3、把数组当作普通对象操作
	// delete 删除：delete ary[索引] 删除指定索引这项(当前项被删除后，其他项的索引不会被改变;当前数组的length也不会改变；)
	//
	// ary.length--: 删除数组最后一项

	// =>splice：数组中内置的方法，可以实现数组的增加、修改、删除
	// * 	splice实现删除
	// * 	splice(n,m) :从索引n开始删除m个(m不写是删除到数组的末尾)
	// *	返回值：被删除的内容（以一个新数组保存）
	// *	原有数组改变
	//	->	splice(0) 清空数组
	//	->	splice() 一项也没删除，返回一个空的数组
	//	->  splice(0,1) 删除第一项
	//	->  splice(ary.length-1,1) 删除最后一项

	// *	splice实现修改
	// *	splice(n,m,x)：在原有删除的基础上用x代替删除的内容

	// *	splice实现增加
	// *	splice(n,0,x):在修改的基础上我们一项都不删除，把x插入到索引n的前面
	// *	返回值：空数组 []
	// -> splice(0,0,x):向数组开头追加新内容
	// -> splice(ary.length,0,x):向数组末尾增加新元素


  #### 数组查询
  ```javascript
  /**
   * slice:数组的查询
   * 参数：slice(n,m)从索引n开始找到索引为m处(不包含m)
   * 返回值：把找到的部分以一个新数组返回
   * 原来的数组不变
   *
   * -> slice(n) 从索引n开始找到末尾
   * -> slice() // slice()数组克隆，克隆一份和原来数组一模一样的新数组
   * slice() 支持负数索引，如果传递的索引为负数，浏览器解释的时候按照 总长度+负数索引 来处理的
   */
  ```

  `将两个数组进行拼接`
  ```javascript
  /**
   * concat: 将多个数组拼接到一起
   * 参数：要拼接的内容(把内容放在原数组后面)，可以是一个数组，也可以是一些数据值
   * 返回值: 返回的是拼接后的新数组
   * 原有数组不变
   * // DEBUG:
   * -> concat() 什么都没有拼接，相当于把原有的数组克隆一份一模一样的新数组出来
   */
  ```

  #### 把数组转化为字符串方法
  ```javascript
  /**
   * 1、tostring ： 实现把数组转化为字符串（转化后的字符串以逗号分割每一项）
   *   参数：无
   *   返回值:转化的字符串
   *   原有数组不变
   */

  /**
   * 2、join：把数组按照指定的分割符转换为字符串，和字符串中的split相对应
   *   参数：指定的连接符
   *   返回值：转化后的字符串
   *   原数组不变
   */
  ```

```javascript
//=> 已知数组中的每一项都是数字，想实现数组求和，我们如何实现？
// 1、循环实现
var total = null;
for(var i = 0; i < ary.length; i++){
  total+=ary[i];
}
console.log(total);

//  2、利用join
var total = eval(ary.join('+'));// -> evel:把字符串变为JS表达式执行
```

`实现数组中的每一项的排序和排列`
```javascript
/**
 * 1、reverse：把数组中每一项倒过来排序
 *   参数：无
 *   返回值：排序后的数组
 *   原有数组改变
 */

/**
 * 2、sort:实现数组的排序
 *   参数：无/回调函数
 *   返回值：排序后的新数组
 *   原有数组改变
 *
   - 1)、不传参数的情况下：可以给10以下的数字进行升序排列，但是超过10的就无法处理了(多位数只识别第一位)
   - 2)、ary.sort(function(a,b){
           return a - b; // -> 升序
           return b - a; // -> 降序
       })
 */
```

`验证数组中是否包含某一项`
```javascript
/**
 *  indexOf() / lastIndexOf:获取当前数组中的第一次或者最后一次出现的位置
 *    数组中的这两个方法在IE6~8下不兼容
 *    字符串中的这两个方法兼容所有浏览器
 * 如果当前数组中并没有这一项，返回的索引是-1，我们根据这一点可以验证数组中是否包含这一项
 */
if(ary.indexOf(12) > -1) {
  //->数组中包含12
}

Array.prototype.myIndexOf = function (value) {
  var result = -1;
  for(var i=0;i<this.length;i++){
    if(value === this[i]){
      result = i;
      break;
    }
  }

  return result;
}
```

#### 遍历数组的方法
```javascript
//=> 以下方法在ie6-8中不兼容
/**
 * forEach：便利数组中的每一项
 */

ary.forEach(function(value,index){
  //=>数组有多少项，当前回调函数执行多少次：每一次传递进来的Value就是当前遍历这一项的值，index就是遍历这一项的索引
});


/**
 * map:遍历数组的每一项，在forEach的基础上，可以修改每一项的值
 */

ary.map(function(value,index){
  //=> 数组有多少项，当前回调函数执行多少次，每一次传递进来的value就是当前遍历这一项的值，index就是遍历这一项的索引
  return xxx; //=>RETURN后面返回的结果就是把当前遍历的这一项修改为XXX
});

* filter
* find
* reduce
* every
* ...

```

#### 数组去重
> 方案一：
> 遍历数组的每一项，拿每一项和它后面的项依次比较，如果相同了，则把他相同的这一项在原数组中删除即可
```javascript
for(var i = 0; i < ary.length - 1; i++){
  var cur = ary[i];
  for(var j = i+1; j < ary.length;){
    cur === ary[j] ? ary.splice(j,1) : j++ ;
  }
}
console.log(ary);
```
> 数组塌陷问题：我们使用splice删除数组中的某一项后,删除这一项后面的某一项的索引都要前进一位(在原有索引上减一);此时如果我们j++，循环操作的值累加了，我们通过最新j获取的元素不是紧挨删除的这一项的元素，而是跳过一项获取的元素
```javascript
for(var i = 0; i < ary.length - 1; i++){
  var cur = ary[i];
  for(var j = i+1; j < ary.length;j++){
    if(cur === ary[j]){
      ary.splice(j, 1);
      j--;
      //=>先让j--，然后再让j++,相当于没加没减，此时j还是原有索引，在获取的时候就是删除这一项后面紧挨着的这一项
    }
  }
}
```

```javascript
for(var i = 0; i < ary.length - 1; i++){
  var cur = ary[i];
  for(var j = i+1; j < ary.length;j++){
    cur === ary[j] ? ary.splice(j,1) : j++ ;
  }
}
```

> 方案二：
> 利用indexOf来验证当前数组中是否包含某一项，包含把当前项删除掉(不兼容IE6~8)
```javascript
var ary = [1,2,12,4,5,6,7,1,34,5,6,7,1,2,34,5,7,7,8,5,23,66,3,2,6,2];

for(var i = 0; i < ary.length; i++) {
  var cur = ary[i];  //=> 当前项
  var curNextAry = ary.slice(i+1); //=> 把当前项后面的那些值以一个新数组返回，我们需要比较的是后面的这些项对应的新数组
  if(curNextAry.indexOf(cur) > -1){
    //=>后面项组成的数组中包含当前这一项(当前项是重复的)，我们把当前项这一项删除即可
    ary.splice(i,1);
    i--;
  }
}
console.log(ary);
```

> 方案三
> 遍历数组中的每一项，把每一项作为新对象的属性名和属性值存储起来，例如：当前项是1，对象中存储{1:1}
>
> 在每一次向对象存储之前，首先看一下原有对象中是否包含了这个属性(`typeof obj[xxx] === undefined 说明当前对象中没有xxx这个属性`)，如果有了这个属性说明数组中的当前项是重复的(1、在原有的数组中删除这一项，2、不在像对象中存储这个结果)，如果不存在(把当前项作为对象的属性名和属性值存储进去即可)

```javascript
for (var i = 0; i < ary.length; i++ ) {
  var cur = ary[i];
  if(typeof obj[cur] !== 'undefined'){
    //=>对象中已经存在改属性：证明当前项是数组中的重复项
    ary.splice(i,1);
    i--;
    continue;
  }
  obj[cur] = cur; //=> obj[1] = 1;   {1:1} 存储
}


for (var i = 0; i < ary.length; i++ ) {
  var cur = ary[i];
  if(typeof obj[cur] !== 'undefined'){
    // ary.splice(i,1); //=>使用splice会导致后面的索引向前进一位，如果后面有很多项，消耗性能很大
    // i--;

    //=>思路：我们把最后一项拿过来替换当前要删除的这一项，然后再把最后一项删除
    ary[i] = ary[ary.length - 1];
    ary.length--;
    i--;//=> 虽然索引是对的，但是当前项的值被改变了，所以还是要i--重新对当前项在进行一次判断
    continue;
  }
  obj[cur] = cur;
}
```

```javascript
Array.prototype.myUnique = function myUnique() {
  var obj = {};
  for(var i = 0; i < this.length; i++ ){
    var item = this[i];
    if(typeof obj[item] !== 'undefined'){
      this[i] = this[this.length - 1];
      this.length--;
      i--;
      continue;
    }
    obj[item] = item;
  }
  obj = null;
  return this;
}
```

> 扩展思路：
> 首先给数组进行排序，然后相邻的两项比较，相同的话把最后一项在数组中去掉=>相邻比较法
> ...
