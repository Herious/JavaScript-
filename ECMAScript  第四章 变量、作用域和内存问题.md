# ECMAScript  第四章 变量、作用域和内存问题

#### 4.1 基本类型和引用类型的值

> 基本类型值： 简单的数据段
>
> 引用类型值： 可能由多个值构成的对象
>
> <font color=#FF9900>Tip: JavaScript 不允许直接访问内存中的位置，当复制保存着对象的某个变量时，操作的是对象的引用。但在为对象添加属性时，操作的是实际的对象。</font>

**4.1.1 动态的属性**

> 定义基本类型值和引用类型值的方式是类似的： 创建一个变量并为该变量赋值。对于引用类型的值，我们可以为其添加属性和方法，也可以改变和删除其属性和方法。但是，我们不能给基本类型的值添加属性，尽管这样做不会导致任何错误。

```javascript
//引用类型值
var person = new Object();
person.name = "wwh";
console.log(person.name); //"wwh"

//基本类型值
var name = "wwh";
name.age = 27;
console.log(name.age); //undefined

```

**4.1.2 复制变量值**

> 在从一个变量向另一个变量复制基本类型值和引用类型值时，如果一个变量向另一个变量复制基本类型值，会在变量对象向创建一个新值，然后把该值复制到为新变量分配的位置上。当从一个变量向另一个变量复制引用类型的值时，同时也会将存储在变量中的值复制一份到为新变量分配的空间中，不同的是，这个值的副本实际上是一个指针，而这个指针指向存储在堆中的一个对象。复制操作结束后，两个变量实际上引用的是同一个对象。因此，改变其中一个变量，就会影响另一个变量。

> 复制基本类型值
>
> ​																		复制前的变量对象:
>
> |      |                 |
> | :--: | :-------------: |
> |      |                 |
> | num1 | 5 (Number 类型) |
>
> ​																		复制后的变量对象：
>
> |      |                 |
> | :--: | :-------------: |
> | num2 | 5 (Number 类型) |
> | num1 | 5 (Number 类型) |
>
> 

> 引用类型值
>
> ![1019087-20161118103316420-2010187687](C:\Users\Administrator\Desktop\1019087-20161118103316420-2010187687.png)



```javascript
var num1 = 5;
var num2 = num1;

var obj1 = new Object();
var obj2 = obj1;
obj1.name = "wwh";
console.log(obj2.name); //"wwh"
```

**4.1.3 传递参数**

> ECMAScript 中所有函数的参数都是按值传递的。在向参数传递基本类型的值是，被传递的值会复制给一个局部变量。在向参数传递引用类型的值时，会把这个值在内存中的地址复制给一个局部变量。

```javascript
function addTen(num) {
    num += 10;
    return num;
}
var count = 20;
var result= = addTen(count);
console.log(count);		//20,没有变化
console.log(result);	//30
```

```javascript
function setName(obj) {
    obj.name = "wwh";
}
var person = new Object();
serName(person);
console.log(person.name);	//"wwh"
```

```javascript
function setName(obj) {
    obj.name = "wwh";
    obj = new Object();	//这个变量引用的是一个局部对象, 会在函数执行完毕时销毁。
    obj.name = "hhh";
}
var person = new Object();
serName(person);
console.log(person.name);	//"wwh"
```

**4.1.4 类型检测**

> typrof 操作符是确定一个变量是字符串、数值、布尔值，还是undefined的最佳工具。如果变量值是一个对象或 null， 则 typeof 操作符会返回 "object"。

```javascript
var un;
var obj = new Object();
console.log(typeof "wwh");	//string
console.log(typeof 25);	//number
console.log(typeof true);	//boolean
console.log(typeof un);	//undefined
console.log(typeof null);	//object
console.log(typeof obj);	//object
```

> instanceof 操作符，
>
> 语法： result = variable instanceof constructor
>
> 用于检测变量值是什么类型的对象。可以用来判断某个构造函数的 prototype 属性是否存在另外一个要检测对象的原型链上。也就是说用来判断 constructor.prototype 是否存在于参数 variable 的原型链上

```javascript
function obj1(){}
function obj2(){}
     
var objTest1 = new obj1();
console.info(objTest1 instanceof obj1)//true
console.info(objTest1 instanceof obj2)//false
 
obj1.prototype = {};  //修改了obj1.prototype
var objTest2 = new obj1();
console.info(objTest2 instanceof obj1)//true
console.info(objTest1 instanceof obj1)//false, obj1.prototype指向了空

```

#### 4.2 执行环境及作用域

> 局部变量和全局变量
>
> 函数可以访问该函数下的局部变量和全局变量
>
> 函数外部不能访问函数内部的变量

```javascript
var globalVariable = "全局变量";
function foo() {
    var fooVariable = "foo函数下的局部变量";
    function fooChild() {
        var fooChildVariable = "fooChild函数下的局部变量";
        //此处可以访问 globalVariable、fooVariable 和 fooChildVariable
        console.log(fooVariable);	//"foo函数下的局部变量"
    }
    console.log(globalVariable);	//"全局变量"
    //此处只能访问 globalVariable 和 fooVariable
}
console.log(globalVariable);	//"全局变量"
console.log(fooVariable);	//报错 ReferenceError: fooVariable is not defined
//此处只能访问 globalVariable
```

**4.2.1 延长作用域链**

> 延长作用域的方法有以下两种：
>
> ​	try-catch 语句中的 catch 块
>
> ​	with 语句

```javascript
function buildUrl() {
    var qs = "?wwh=cool";
    with(location) {
        var url = href + qs;
    }
    return url;
}
```

**4.2.2 没有块级作用域**

```javascript
if (true) {
    var color = "blue";
}
console.log(color);	//"blue"

for (var i = 0; i < 10; i++) {
    doSomething(i);
}
console.log(i);	//10
```



> 对于有=块级作用域的语言来说，for 语句初始化的变量的表达式所定义的变量，只会存在于循环的环境之中。而对于 JavaScript 来说，由 for 语句创建的变量 i 即使在 for 循环执行结束后，也依然会存在与循环外部的执行环境中。

#### 4.3 垃圾收集

> JavaScript 具有自动垃圾收集机制，也就是说，执行的环境会负责管理代码执行过程中使用的内存。浏览器实现垃圾收集通常有两个策略：标记清除、引用计数

**4.3.1 标记清除**

> JavaScript 中最常用的垃圾收集方式是标记清除。当变量进入环境（例如，在函数中声明一个变量）时，就将这个变量标记为"进入环境"。当变量离开环境时，则将其标记为"离开环境"。
>
> 垃圾收集器在运行是会给存储在内存中的所有变量都加上标记。然后，它会去掉环境中的变量以及被环境中的变量引用的变量的标记。而在此之后被加上标记的变量将被视为准备删除的变量，原因是环境中的变量已经无法访问到这些变量了。最后垃圾收集器完成内存清除工作，销毁那些带标记的值并回收它们所占用的内存空间。

**4.3.2 引用计数**

> 另一种不太常见的垃圾收集策略叫做引用计数。引用计数的含义是跟踪记录每个值被引用的次数。当声明了一个变量并将一个引用类型值赋给该变量是，则这个值的引用次数就是1。如果同一个值又被赋给另一个变量，则该值的引用次数减1。当这个值变成0时，就可以将其占用的内存空间回收回来。
>
> <font color=red>Tip: 有个较为严重的问题 循环引用</font>

**4.3.3 性能问题**

> 垃圾收集器是周期性运行的，而且如果为变量分配的内存数量很可观，那么回收工作量也是相当大的。

**4.3.4 管理内存**

> 确保占用最少的内存可以让页面获得较好的性能。优化内存占用的最佳方式，就是为执行的代码中只保存必要的数据。一旦数据不再有用，就将其值设置为 null 来释放引用----这个做法叫做**解除引用**，以便垃圾收集器下次运行是将其回收。

```javascript
function createPerson(name) {
    var localPerson = new Object();
    localPerson.name = name;
    return localPerson
}
var globalPerson = createPerson("wwh");
//主动解除globalPerson的引用
globalPerson = null;
```

**4.4 小结**

> - JavaScript 变量可以用来保存两种类型的值：基本类型值和引用类型值
> - 基本类型值在内存中占据固定大小的空间。因此被保存在栈内存中
> - 从一个变量向另一个变量复制基本类型的值，会创建这个值的一个副本
> - 引用类型的值是对象，保存在堆内存中
> - 包含引用类型值的变量实际包含的并不是对象本身，而是一个指向该对象的指针
> - 从一个变量向另一个变量复制引用类型的值，复制的其实是指针，因此两个变量最终都指向同一个对象
> - 确定一个是哪种基本类型可以使用typeof，而确定一个值是哪种引用类型可以使用 instanceof 操作符
> - 全局环境只能访问在全局环境中定义的变量和函数
> - JavaScript 具有自动垃圾收集机制
> - 引用计数算法在遇到循环引用是会产生问题

