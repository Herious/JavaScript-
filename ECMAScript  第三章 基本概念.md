# ECMAScript  第三章 基本概念

#### 3.1 语法

**3.1.1 区分大小写**

> Javascript 中的一切（变量、函数名和操作符）都区分大小写

**3.1.2 标识符**

> 第一个字符必须是字母、下划线（_）或一个美元符号（$）

> 其他字母可以是字母、下划线、美元符号或数字

<font color=red>Tip: 字母可以包含扩展的ASCII或Unicode字母字符，但是不推荐这样做</font>

**3.1.3 注释**

> // 单行注释

> /*多行（块级）
>
> *注释
>
> */

**3.1.4 严格模式**

> ECMAScript 5 引入了严格模式的概念，启动严格模式可以在代码块前面加上 “use strict”。支持严格模式的浏览器包括 IE10+、Firefox 4+、Safari 5.1+、 Opera 12+ 和Chrome

**3.1.5 语句**

> ECMAScript 中的语句以一个分号结尾；如果省略分号，则由解析器确定语句的结尾

```javascript
var sum = a + b  //及时没有分号也是有效语句----不推荐
var diff = a - b; //有效语句----推荐
```

> 代码块, 以左花括号（{）开头，右花括号（}）结尾

```javascript
if (test) {
    test = false;
    alert(test);
}
```

> 虽然条件控住语句只在执行多条语句时才要求使用代码块，但最好始终在控制语句中使用代码块----即使代码块中只有一条语句，例如：

```javascript
if (test)       //有效但容易出错, 不推荐新手使用
    alert(test); 

test && alert(test); 

if (test) {     //推荐使用
    alert(test);
}
```

#### 3.2 关键字和保留字

> ECMA-262 描述了一组具有特殊用途的**关键字**，这些关键字可用于表示控制语句的开始或结束，或者用于执行特定的操作，<font color=red>不可用作标识符</font>以下是 ECMAScript 的全部关键字（带*号的是第五版新增的关键字）：
>
> break  case  catch  continue  debugger*  default  delete  do  else  finally  for  function  if  in instanceof  new  return  switch  this  throw  try  typeof  var  void  while  with

> ECMA-262 描述了另外一组不能用来做标识符的**保留字**。以下是ECMA-262第三版定义的全部保留字：
>
> abstract  boolean  byte  char  class  const  debugger  double  enum  export  extends  final  float  goto  implements  import  int  inteaface  long  native  packge  private  protected  public  short  static  super  synchronized  throws  transient  volatile

> 第五版把在非严格模式下运行的保留字缩减为下列这些：
>
> class  const  enum  export  extends  import  super  

> 在严格模式下，第五版还对以下保留字施加了限制：
>
> implements  interface  let  packge  private  protected  public  static  yield

<font color=#FF9900>Tip: 第五版关键字和保留字可以用来作为对象的属性名。但最好不要使用关键字和保留字作为对象的属性名。</font>

<font color=red>Tip: 除了上面列出的保留字和关键字， ECMA-262 第五版对 eval 和 arguments 施加了限制。在严格模式下，这两个名字也不能作为标识符或属性名，否则会抛出错误</font>

#### 3.3 变量

> ECMAScript 的变量是松散类型的，可以用来保存任何类型的数据。定义变量时要使用var操作符，后跟变量名

```javascript
var message  //该代码定义了一个名为message的变量，该变量可以保存任何值，未初始化的变量会默认为undefined

var message = "hello"  //该代码定义一个message的变量，并为其赋值为"hello"
message = 100 //有效，但不推荐
```

<font color=#FF9900>注意: 用 var 操作符定义的变量将成为定义该变量的作用域中的局部变量</font>

```javascript
function foo() {
    var message = "hello"; //局部变量
}
foo()
alert(message); //Uncaught ReferenceError: message is not defined
```

可以省略 var 来创建一个全局变量。<font color=red>但不推荐这样做，因为在局部作用域中定义的全局变量很难维护</font>

```javascript
function foo() {
    message = "hello"; //局部变量
}
foo()
alert(message); //"hello"
```

可以一条语句定义多个变量，只需要把每个变量用逗号隔开：

```javascript
var message = "hello",
    name = "wwh",
    age = "24"
```

<font color=red>在严格模式下，不能定义 eval 或 arguments 的变量</font>

#### 3.4 数据类型

- 简单数据类型（也称基本数据类型）: Undefined、Null、Boolean、Nubber和String
- 复杂数据类型: Object

**3.4.1 typeof 操作符** 

> 检测给定变量的数据类型，对一个值使用typeof操作符可能返回下列某个字符串:
>
> - "undefined" —— 未定义
> - "boolean" —— 布尔值
> - "string" —— 字符串
> - "number" —— 数值
> - "object" —— 对象或者null
> - "function" —— 函数

```javascript
var message = "some string";
alert(typeof message);  //"string"
alert(typeof(message)); //"string"
alert(typeof 96);  //"number"
```

**3.4.2 Undefined类型**

> Undefined 类型只有一个值，即特殊的 undefined 。在使用 var 声明变量单未对其加以初始化时，这个值就是 undefined。没有必要使用 undefined 的值显式初始化变量。不过，包含undefined 值的变量与未定义的变量还是不一样的。对未初始化的变量和未声明的变量使用typeof 操作符时，都会返回 undefined。

```javascript
var message;
console.log(message == undefined); //true

var message = undefined;
console.log(message == undefined);  //true

var message;
console.log(message);  //"undefined"
console.log(age);  //Uncaught ReferenceError: age is not defined

var message;
console.log(typeof message);  //"undefined"
console.log(typeof age);  //"undefined"

```

**3.4.3 Null 类型**

> Null 类型只有一个值，即特殊的 null 。从逻辑角度来看，null 值表示一个空指针，而这也是使用typeof 操作符检测 null 时会返回 "Object" 的原因。undefined 值是派生自 Null 的，因此ECMA-262 规定对它们的相等性测试要返回 true 。

```javascript
var car = null;
console.log(typeof car);  //"Object"

console.log(null == undefined);  //true
```

**3.4.4 Boolean 类型**

>  Boolean 类型只有两个值： true 和 false 
>
> 该数据类型常用语条件控制语句，各种数据类型及其对应的转换规则如下：

| 数据类型  |       转化为true的值        | 转化为false的值 |
| :-------: | :-------------------------: | :-------------: |
|  Boolean  |            true             |      false      |
|  String   |       任何非空字符串        |       ""        |
|  Number   | 任何非0数字值（包括无穷大） |     0和NaN      |
|  Object   |          任何对象           |      null       |
| Undefined |   not applicable (不适用)   |    undefined    |

```javascript
var message = "wwh";
if (message) {
   console.log("coooooool");
}
```

**3.4.5 Number类型**

###### 1 浮点数值 ######

> 该类型使用IEEE754格式来表示整数和浮点数值，<font color=red>鉴于JavaScript中数值的保存方式，可以保存 +0 和 -0 并且它们是相等的</font>。支持科学计数法。

```JavaScript
var num = 3.125e7    //等于31250000
```

> 默认情况下那些小数点后面带有 6 个 0 以上的浮点数值转换为以 e 表示法表示的数值（例如， 0.0000003会被转换为3e-7）

> 浮点数值的最高精度是17位小数，但在进行算数计算时，其精度远远不如整数。例如 0.1 + 0.2 的结果不是 0.3， 而是0.30000000000000004。<font color=red>关于浮点数值计算会产生舍入误差的问题，有一点需要明确：这是使用基于IEEE754数值的浮点计算的通病。其他使用相同数值格式的语言也存在这个问题</font>

###### 2 数值范围 ######

> 由于内存的限制，ECMAScript 不能保存所有的数值。ECMAScript 能够表示的最小数值保存在 Number.MIN_VALUS 中——在大多数浏览器中， 这个值是 5e-324；能够表示的最大数值保存在 Number.MAX_VALUS 中——在大多数浏览器中， 这个值是 1.7976931348623157e+308 。如果某次计算超出了 JavaScript 数值范围的值，那么这个值会自动转换成特殊的 Infinity 值。并且无法参与以后的计算。

###### 3 NaN ######

> NaN，即非数值（Not a Number）是一个特殊的值。这个数值用来表示一个本来要返回数值的操作未返回数值的情况。
>
> NaN 本身有两个非同寻常的特点：
>
> ​    1、任何涉及 NaN 的操作都会返回 NaN
>
> ​	2、NaN 与任何值都不相等，包括 NaN 本身
>
> 检验一个值能否被转换成数值

```javascript
console.log(isNaN(NaN));	//true
console.log(isNaN(10));		//false 
console.log(isNaN("10"));	//false 
console.log(isNaN("blue"));	//true (不能转换为数值)
console.log(isNaN(true));	//false (可以被转换成数值1)
```

###### 4 数值转换 ######

> 1、Number（）: 可用于任何数据类型
>
> 2、parseInt（）:  将字符串转换成整数类型
>
> 3、parseFloat（）： 将字符串转换成浮点数类型

**3.4.6 String类型**

> 字符串的特点：一旦被创建，就不可变

> 转换为字符串.toString（）方法

```javascript
var age = 25;
var ageAsString = age.toString();	//字符串"25"
var found = true;
var foundAsString = found.toString(); //字符串"true"
```

<font color=red>Tip: 如果值是 null，则返回 "null",  如果值是 undefined， 则返回 "undefined"</font>

**3.4.7 Object类型**

> ECMAScript 中的对象其实就是一组数据和功能的集合。对象可以通过执行new操作符后跟要创建的对象类型的名称来创建。

```javascript
var o = new Object(); //推荐
var o = new Object;	//有效，但不推荐
```

#### 3.5 操作符 ####

**3.5.1 一元操作符 **

> 只能操作一个值的操作符叫做一元操作符。（++， --）

```javascript
var num = 25;
--num;	//24
++num; 	//25
```

**3.5.2 位操作符 **

> 位操作符用于最基本的层次上，即按内存中表示数值的位来操作数值。ECMAScript 中所有的数值都已 IEEE-754 64位格式存储，但位操作符并不直接操作64位的值，而是将64的值转换成32的整数，然后再进行操作，最后再将结果转换成64位。

###### 1 按位非（NOT） ######

> 按位非操作符由一个波浪线（~）表示。执行按位非的结果就是返回数值的反码。

```javascript
var num1 = 25;		//二进制00000000000000000000000000011001
var num2 = ~num1;	//二进制11111111111111111111111111100110
console.log(num2);	// -26
```

```javascript
var num1 = 25;		
var num2 = -num1 - 1;
console.log(num2);	// -26
```

<font color=#FF9900>Tip: 虽然以上两个代码的结果一样， 但是按位非是在数值表示的最底层进行操作， 因此速度更快。</font>

###### 2 按位与（AND）

> 按位与操作符由一个和号字符 ( & ) 表示，按位与操作只在两个数值的对应位都是1时才返回1，任何一位是0，结果都是0。

```javascript
var result = 25 & 3
console.log(result)	// 1
```

> 底层操作如下：
>
> ​	25 = 0000 0000 0000 0000 0000 0000 0001 1001
>
> ​	  3 = 0000 0000 0000 0000 0000 0000 0000 0011
>
> ​	——————————————————————
>
> AND = 0000 0000 0000 0000 0000 0000 0000 0001

###### 3 按位或（OR）

> 按位或操作符由一个竖线符号（|）表示，按位与操作在一个位是1时就返回1，只有在两个位都为0的时候才返回0。

```javascript
var result = 25 | 3;
console.log(result);	// 27

//可用于对小数取整(只保留整数部分,舍弃所有小数点后面的数字)
var result = 0 | 1.5555;	//1
var result = 0 | 1.3555;	//1

//四舍五入
console.log(0 | (1.3555 + 0.5));	//1
console.log(0 | (1.5555 + 0.5));	//2

//向上取整
function ceil(m, n) {
    return 0 | ((m + n - 1) / n)
}
console.log(0 | (4 + 2)/3);	//2

```

> 底层操作如下：
>
> ​	25 = 0000 0000 0000 0000 0000 0000 0001 1001
>
> ​	  3 = 0000 0000 0000 0000 0000 0000 0000 0011
>
> ​	——————————————————————
>
>    OR =   0000 0000 0000 0000 0000 0000 0001 1011

###### 4 按位异或（XOR）

> 按位或操作符由一个插入符号（^）表示，按位与操作在只有一个位是1时才返回1，如果对应的两位都是1或者都是0, 则返回0。

```javascript
var result = 25 ^ 3;
console.log(result);	// 26
```

> 底层操作如下：
>
> ​	25 = 0000 0000 0000 0000 0000 0000 0001 1001
>
> ​	  3 = 0000 0000 0000 0000 0000 0000 0000 0011
>
> ​	——————————————————————
>
>   XOR = 0000 0000 0000 0000 0000 0000 0001 1010

###### 5 左移

> 左移操作符由两个小于号（<<）表示， 这个操作符会将数值的所有位向左移动指定的位数。

```javascript
var age = 25;	// 等于二进制的11001
var newAge = age << 2;	// 二进制的1100100等于100
```

###### 6 有符号右移

> 有符号的右移操作符由两个大于号（>>）表示， 这个操作符会将数值的所有位向右移动指定的位数，但会保留符号位

```javascript
var age = 100;	// 等于二进制的1100100
var newAge = 100 >> 2;	// 二进制的11001等于25
```

###### 7 无符号右移

> 有符号的右移操作符由三个大于号（>>>）表示， 这个操作符会将数值的所有位向右移动指定的位数，不保留符号位

```javascript
var age = 100;	// 等于二进制的1100100
var newAge = 100 >>> 2;	// 二进制的11001等于25

var num = -64;	//二进制的1111 11111111 1111 1111 1111 1100 0000
var newNum = num >>> 4;	//二进制的0000 1111 11111111 1111 1111 1111 1100, 即268435452
```

**3.5.3 布尔操作符 **

> - 1、逻辑非，用一个感叹号（！）表示
> - 2、逻辑与，用两个和号（&&）表示
> - 3、逻辑或，用两个竖线（||）表示

<font color=red>Tip: 如果与的第二个操作数是对象，则只有第一个操作数求值结果为true时，才会返回该对象</font>

<font color=red>Tip: 如果或的第一个操作数求值结果为true时，就不会对第二个操作数求值</font>

```javascript
console.log(!false);	//true

var age = false;
var newAge = age && heiHeiHei; //heiHeiHei不会被执行

var age = true;
var newAge = age && heiHeiHei; //heiHeiHei会被执行, 并且会抛出错误

var name = false;
var newName = name|| heiHeiHei; //heiHeiHei会被执行, 并且会抛出错误

var name = true;
var newName = name || heiHeiHei; //heiHeiHei不会被执行
```

**3.5.4 乘性操作符 **

> ECMAScript 定义了3个乘性操作符： 乘法、除法、求模（取余）。如果参与乘性操作符的某个操作值不是数值，后台会使用Number（）转型函数将其转换为数值，也就是说，空字符串会被当成0， 布尔值 true 会被当成 1。

> 乘法（*）
>
> var result = 96 * 25;
>
> 在特殊值的情况下，遵循以下特殊的规则：
>
> ​	1、如果操作数都是数值，执行常规乘法运算，如果乘积超过 ECMAScript 数值的表示范围，则返回 Infinity 或者 -Infinity
>
> ​	2、如果有一个操作数是 NaN，则返回 NaN
>
> ​	3、如果是 Infinity 与 0 相乘， 则返回 NaN
>
> ​	4、如果是 Infinity 与非 0 相乘， 则返回 Infinity 或者 -Infinity ，取决于有符号操作数的符号
>
> ​	5、如果是 Infinity 与 Infinity 相乘， 则返回 Infinity
>
> ​	6、如果有一个操作数不是数值， 则将其转换成Number（）

> 除法（/）
>
> var result = 96 * 25;

> 求模（%）
>
> var result = 96 % 25；

**3.5.5 加性操作符 **

ECMAScript 定义了2个加性操作符： 加法、减法。

> 加法（+）
>
> var result = 96 + 25;
>
> 如果两个操作数都是数值，执行常规的加法计算，然后根据下列规则返回结果：
>
> ​	1、如果有一个操作数是 NaN，则返回 NaN
>
> ​	2、如果是 Infinity 与 Infinity 相加， 则返回 Infinity
>
> ​	3、如果是 -Infinity 与 -Infinity 相加， 则返回 -Infinity
>
> ​	4、如果是 Infinity 与 -Infinity 相加， 则返回 NaN
>
> 不过，如果有一个操作数是字符串，那么就应用如下规则：
>
> ​	1、如果两个操作数都是字符串，则将它们拼接起来
>
> ​	2、如果只有一个操作数是字符串，则将另一个操作数转换为字符串，再执行拼接

> 减法（-）
>
> var result = 96 - 25;

**3.5.6 关系操作符 **

> 小于（<）、大于（>）、小于等于（<=）、大于等于（>=）

**3.5.7 相等操作符 **

> 相等（==）、不相等（!=）、全等（===）、不全等（!==）

```javascript
var result1 = ("55" == 55);		//true, 转换后相等
var result2 = ("55" != 55);		//false, 转换后相等
var result3 = ("55" === 55);	//false, 类型不同
var result4 = ("55" !== 55);	//true, 类型不同
```

**3.5.8 条件操作符 **

```javascript
//variable = boolean_expression ? true_value : false_value
var max = (num1 > num2) ? num1 : num2;
```

> 在上面的例子中，如果 num1 大于 num2， 则将 num1 的值赋值给 max， 否则将 num2 的值赋值给 max

**3.5.9 赋值操作符 **

> 简单的赋值操作符由等于号（=）表示，其作用就是将右边的值赋给左边的变量。

```javascript
var age = 25;
var name = "wwh";
```

**3.5.10 逗号操作符 **

> 使用逗号操作符可以在一条语句中执行多个操作	

```javascript
var num1 = 1, num2 = 2, num3 = 3;
```

> 除此之外，逗号操作符还可以用于赋值。在用于赋值时，逗号操作符总会返回表达式中的最后一项。

```javascript
var num = (5, 4, 2, 9, 25); // num的值为25
```

#### 3.6 语句

**3.6.1 if 语句**

```javascript
/*
if (condition) {
    statement1;
} else {
    statement2;
}

if (condition1) {
    statement1;
} else if(condition2) {
    statement2;
} else {
    statement3;
}
*/
var author = "wwh";
if (author == "wwh") {
    console.log("heiheihei");
} else (
	console.log("bukaixn");
)
```

**3.6.2 do-while 语句**

> do-while 语句是一种后测试循环语句，即只有在循环体中的代码被执行完之后，才会测试出口条件。<font color="red">所以代码块至少要被执行一次</font>。

``` javascript
var i = 25;
do {
    i += 2;
} while (i < 30);
console.log(i)	//在该循环中, 只要变量i的值小于10, 循环就会一直继续下去
```

**3.6.3 while 语句**

> while 语句属于前测试循环语句，也就是说，在循环体的代码被执行钱就会对出口条件求值。

```javascript
var i = 25;
while (i < 30) {
    i += 2;
}
```

**3.6.4 for 语句**

> for 语句也是一种前测试循环语句，但它具有执行之前初始化变量和定义循环后要执行的代码的能力，以下是 fot 语句的语法：
>
> for (initalization; expression; post-loop-expression) statment

```javascript
for (var i = 0; i < 10; i++) {
    console.log(i);
}
```

**3.6.5 for-in 语句**

> for-in 语句是一种精准的迭代语句， 可以用来枚举对象的属性。以下是for-in 语句的语法：
>
> for (property in expression) statment

```javascript
for (var propName in window) {
    console.log(propName);
}
```

**3.6.6 label 语句**

> 使用 label 语句可以在代码中添加标签，以便将来使用。以下是 label 语句的语法：
>
> label：statment

```javascript
start: for (var i = 0; i < 10; i++) {
    console.log(i);
}
```

**3.6.7 break 和 continue 语句**

> break 和 continue 语句用于在循环中精确的控制代码的执行。其中，break语句会立即退出循环，强制执行循环后面的语句。而 continue 表示立即退出当前循环，进入到下一次循环。

```javascript
//break
var num = 0;
for (var i = 0; i < 10; i++) {
    if (i % 5 == 0) {
      break;
    };
    num++;
}
console.log(num); //4
```

```javascript
//continue
var num = 0;
for (var i = 0; i < 10; i++) {
    if (i % 5 == 0) {
      continue;
    };
    num++;
}
console.log(num); //8
```

```javascript
//break
var num = 0;
outermost: 
for (var i = 0; i < 10; i++) {
    for (var j = 0; j < 10; j++) {
      if (i == 5 && j == 5) {
        break outermost;
      };
      num++;
    }

}
console.log(num); //55
```

```javascript
//continue
var num = 0;
outermost: 
for (var i = 0; i < 10; i++) {
    for (var j = 0; j < 10; j++) {
      if (i == 5 && j == 5) {
        continue outermost;
      };
      num++;
    }

}
console.log(num); //95
```

**3.6.8 with 语句**

> <font color="red">由于大量使用with语句会导致性能下降，同时也会给代码调试造成困难，因此在开发大型应用程序时，不建议使用with语句</font>

**3.6.9 switch 语句**

```javascript
swith(i) {
    case 25:
    case 35:
    	console.log("青年");
    case 45:
    case 55:
    	console.log("中年");
    case 65:
    case 75:
    	console.log("老年");
}
```

> <font color="red">Tip：switch 语句在比较值时使用的是全等操作符，因此不会发生类型转换</font>

#### 3.7 函数

> 函数对任何语言来说都是一个核心的概念。通过函数可以封装任意多条语句，而且可以在任何地方、任何时候调用执行。ESCMScript 中的函数使用 function 关键字来声明，后跟一组参数以及函数体。函数的基本语法如下：
>
> function functionName (arg0, arg1, ... , argN) {
>
> ​	statements
>
> }

```javascript
//函数示例
function sayWwh(name, message) {
    console.log("Hello " + name + ": " + message);
}

sayWwh("wwh", "cooooooooool");
```

> 函数可以使用return语句后跟要返回的值来实现返回值。<font color=#FF9900>return语句后面的语句不会被执行</font>

```javascript
function add(num1, num2) {
    return num1 + num2;
    console.log("该语句不会被执行");
}
```

> <font color="red">Tip：严格模式下，对函数有一些限制：</font>
>
> - <font color="red">不能把函数命名为 eval 或 arguments；</font>
> - <font color="red">不能把参数命名为 eval 或 arguments；</font>
> - <font color="red">不能出现两个命名参数同名的情况；</font>

**3.7.1 理解参数**

> ECMAScript 函数的参数与大多数其他语言中的函数参数有所不同，ECMAScript 不介意传递进来多少个参数，也不在乎传进来的是什么数据类型。即便你定义的函数只接收两个参数，在调用的时候也未必一定要传递两个参数。可以传递一个、三个甚至不传递参数。ECMAScript  中的参数在内部是用一个数组表示的，函数接收的始终是这个数组，而不关心数组中包含哪些参数（如果有参数的话）

> arguments 对象只是与数组类似（它并不是 Array 的实例），因为可以使用方括号语法访问他的每一个元素（即第一个元素是arguments [0], 第二个元素是arguments[1], 以此类推）

```javascript
function sayWwh() {
    console.log("Hello " + arguments[0] + ": " + arguments[1]);
}

sayWwh("wwh", "cooooooooool");
```

**3.7.2 没有重载**

> ECMAScript  函数不能像传统意义上那样实现重载。如果在 ECMAScript  中定义了两个名字相同的函数，则该名字只属于后定义的函数。

```javascript
function add(num1, num2) {
    return num1 + num2;
}

function add(num1, num2) {
    return num1 + num2 + 100;
}

add(100, 100) //300
```

#### 3.8 小结

> - ECMAScript  中的基本数据类型包括Undefined、Null、Boolean、Number和String
> - ECMAScript  没有为整数和浮点数值分别定义不同的数据类型，Number 类型可用于表示所有的数值
> - ECMAScript  也有一种复杂的数据类型，即 Object 类型，该类型是这门语言中所有对象的基础类型
> - 严格模式为这门语言中容易出错的地方施加了限制
> - ECMAScript  提供了算术操作符、布尔操作符、关系操作符及赋值操作符
> - ECMAScript  函数不能重载
> - 可以向 ECMAScript  函数传递任意个参数，并且可以通过 arguments 对象来访问这些参数
> - ECMAScript  中没有函数签名的概念
> - 未指定返回值的函数返回的是一个特殊值 undefined
> - 无需指定函数的返回值，因为任意 ECMAScript  函数都可以在任何时候返回任何值

