# ECMAScript  第五章 引用类型

> 引用类型的值（对象）是引用类型的一个实例。在 ECMAScript 中，引用类型是一种数据结构，用于将数据和功能组织在一起。
>
> 对象是某个特定引用类型的实例。新对象是使用new操作符后跟一个构造函数来创建的。构造函数本身就是一个函数

#### 5.1 Object 类型

> 到目前为止，我们看到的大多数引用类型的值都是 Object 类型的实例；而且，Object 也是ECMAScript中 使用最多的一个类型。

> 创建 Object 实例的方式有两种。第一种是使用 new 操作符后跟 Object 构造函数，第二种方式是使用**对象字面量**表示法。

>在通过对象字面量定义对象时，不会调用 Object 构造函数。Firefox2及更早的版本除外

```javascript
//第一种方式创建Object实例
var person = new Object();
person.name = "wwh";
person.age = 24;

//第二种方式创建Object实例(推荐使用，代码量少，且能够给人封装数据的感觉)
var person = {
    name: "wwh",
    age: 24
};

```

> 访问对象属性时有两种方式，第一种是使用点表示法，第二种方式是使用方括号表示法。一般推荐使用点表示法，除非特殊情况（变量、属性名中包含会导致语法错误的字符等）

```javascript

var person = {
    name: "wwh",
    age: 24,
    "exceptional case":	"特殊情况"
};

console.log(person["name"]);	// >wwh
console.log(person.name);	// >wwh

console.log(person["exceptional case"]);	// >"特殊情况"
console.log(person.exceptional case);	// 语法错误

var a = "name";
console.log(person[a]);	// >wwh


```

#### 5.2 Array 类型

> Array 特性：
>
> ​	1、ECMAScript 数组是数据的有序列表;
>
> ​	2、ECMAScript 数组的每一项可以保存任意数据类型的数据;
>
> ​	3、ECMAScript 数组的大小是可以动态调整的，会随着数据的添加自动增长。

> 创建数组的方式：
>
> ​	1、使用 Array 构造函数
>
> ​	2、使用数组字面量表示法

>在通过数组字面量定义对象时，不会调用 Array 构造函数。Firefox3及更早的版本除外

```javascript
var colors = new Array();	// 创建一个空的数组
var colors = new Array(20);	// 创建一个长度为20的数组
var colors = new Array("red", "blue", "green");	// 创建一个长度为3的数组
// Tip: 在使用 Array 构造函数时也可以省略new操作符。不过能不省就尽量别省.
var colors = Array();

var colors = ["red", "blue", "green"]; // 创建一个长度为3的数组
var colors = []; // 创建一个空的数组
var colors = [1, 2, ]; // 不要这样写,不同浏览器出现的结果不一样
var colors = [, , , ]; // 不要这样写,不同浏览器出现的结果不一样
```

> 在读取和设置数组中的元素时，可以通过方括号和下标来访问。数组的长度保存在其 length 属性中。

```javascript
var colors = ["red", "blue", "green"]; // 创建一个长度为3的数组
console.log(colors[0]);	// 打印第1个元素
colors[2] = "black";	// 修改第3个元素
colors[3] = "brown";	// 新增第4个元素

console.log(colors.length);	// 打印数组的长度
colors.length = 2	// 移除数组中第2个元素后面的所有元素
colors.length = 5	// 新增3个值为undefined的元素
```

###### 5.2.1 检测数组

> ECMAScript5 新增了 Array.isArray() 方法。这个方法的目的是最终确定某个值到底是不是数组，而不管它是在哪个全局环境中创建的。（解决自ECMAScript3 中不同框架里面存在不同的 Array 构造函数）

```javascript
if (Array.isArray(value)) {
    // 对数组进行操作
}
```

###### 5.2.2 转换方法

> toLocalString() 、toString()、 valueOf()。
>
> valueOf(): 返回的还是数组本身
>
> toString(): 返回数组每一项的toString()方法拼接而成的一个以逗号分隔的字符串
>
>  toLocalString(): 返回数组每一项的toLocalString()方法拼接而成的一个以逗号分隔的字符串
>
> join(): 可以使用不同的分隔符构架字符串

```javascript
var parson1 = {
    toLocaleString: function() {
        return "wwh"
    },
    toString: function() {
        return "wwh"
    }
}

var parson2 = {
    toLocaleString: function() {
        return "heihei"
    },
    toString: function() {
        return "haha"
    }
}

var peopel = [parson1, parson2];
console.log(peopel);	
/*
[ { toLocaleString: [Function: toLocaleString],
    toString: [Function: toString] },
  { toLocaleString: [Function: toLocaleString],
    toString: [Function: toString] } ]
*/
alert(peopel); // >wwh,haha
console.log(peopel.toString());	// >wwh,haha
console.log(peopel.toLocaleString());	// >wwh,heihei

var colors = ["red", "blue", "green"];
console.log(colors.join(','));	// >red,blue,green
console.log(colors.join('|'));	// >red|blue|green
```

###### 5.2.3 栈方法

> 栈： 一种LIFO（Last-In-Frist-Out, 后进先出）的数据结构。
>
> push():  可以接受任意数量的参数，把它们逐个添加到数组末尾，并返回修改后数组的长度。
>
> pop(): 从数组末尾移除最后一项，减少数组的长度，然后返回移除的项。

```javascript
var colors = ["red", "blue", "green"];
colors.push("black");
console.log(colors.length);	// >4	
var item = colors.pop();
console.log(colors.length);	// >3
console.log(item);	// >black
```

###### 5.2.4 队列方法

> 队列： 一种FIFO（Frist-In-Frist-Out, 先进先出）的数据结构
>
> shift(): 从数组的第一项，减少数组的长度，然后返回移除的项。
>
> unshift():  可以接受任意数量的参数，把它们逐个添加到数组开头，并返回修改后数组的长度。

``` javascript
var colors = ["red", "blue", "green"];
colors.unshift("black");
var item = colors.shift();
console.log(colors.length);	// >3
console.log(item);	// >red
//Tip: 可以用unshift()和pop()实现反向队列
```

###### 5.2.5 重排序方法

> reserve(): 反转数组中元素的顺序
>
> sort(): 重排序，默认升序排列；**即便数组元素全部都是数值类型，此方法依然会将所有元素先转换成字符串再进行升序排序。**

```javascript
var values = [0, 1, 5, 10, 15];
console.log(values.reverse()); // 返回反转后的新数组 [15, 10, 5, 1, 0]
console.log(values.sort()); // 返回排序后的新数组 [0, 1, 10, 15, 5]

// 为了解决使用sort()会转换成字符串后再比较的问题，sort()方法可以传入一个比较函数。
function compareMaxToMin(value1, value2) {
    return value2 - value1
}

function compareMinToMax(value1, value2) {
    return value1 - value2
}

console.log(values.sort(compareMinToMax)); // 返回排序后的新数组 [0, 1, 5, 10, 15]

console.log(values.sort(compareMaxToMin)); // 返回排序后的新数组 [15, 10, 5, 1, 0]
```

###### 5.2.6 操作方法

>concat(): 该方法会创建当前数组的一个副本, 然后将接收到的参数添加到这个副本的末尾, 最后返回新构建的数组.
>
>slice(): 该方法能够基于当前数组中的一个或多个项, 创建一个新数组. 该方法可以接收一个或者两个参数, 即要返回项的起始位置和结束位置. 在只有一个参数时, 该方法返回从参数指定位置到数组结尾的所有元素. 该方法不会影响原始数组
>
>splice(): 该方法可以向数组中删除、插入和替换元素. 该方法始终都会返回一个数组, 该数组中包含从原始数组中删除的项(如果没有删除任何项, 则返回一个空数组)

```javascript
var colors = ["red", "blue", "green"];

//concat
var colors2 = colors.concat("yellow", ["black", "brown"]);
console.log(colors);  // >"red", "blue", "green"
console.log(colors2); // >"red", "blue", "green", "yellow", "black", "brown"

//slice
var colors3 = colors.slice(1);
var colors4 = colors.slice(1, 2);
console.log(colors3);  // >"blue", "green"
console.log(colors4); // >"blue"

//splice
var colors5 = colors.splice(0, 1);
var colors6 = colors.splice(1, 0, "yellow", "orange");
var colors7 = colors.splice(1, 1, "red", "purple");
console.log(colors5);  // >["red"]
console.log(colors6); // >[]
console.log(colors7);  // >["yellow"]
```

###### 5.2.7 位置方法

> indexOf(): 查询元素第一次出现的下标（从前往后查）, 接收两个参数: 1、需要查询的元素,2、查找起点的下标 （可选，默认为0）
>
> lastIndexOf(): 查询元素最后一次出现的下标（从后往前查）, 接收两个参数: 1、需要查询的元素,2、查找起点的下标 （可选，默认为0）

```javascript
var values = [0, 1, 5, 10, 15, 25, 15, 10, 5, 1, 0];
console.log(values.indexOf(5));			// >2
console.log(values.indexOf(5, 3));		// >8
console.log(values.lastIndexOf(5));		// >8
console.log(values.lastIndexOf(5, 3));	// >2
```

###### 5.2.8 迭代方法

> every(): 对数组中的每一项运行给定函数, 如果该函数对每一项都返回true, 则返回true
>
> filter(): 对数组中的每一项运行给定函数, 返回该函数会返回true的项组成的数组
>
> forEache(): 对数组中的每一项运行给定函数, 没有返回值
>
> map(): 对数组中的每一项运行给定函数, 返回每次函数调用的结果组成的数组
>
> some(): 对数组中的每一项运行给定函数, 如果该函数对任意一项返回true, 则返回true

```javascript
var values = [0, 1, 5, 10, 15, 25, 15, 10, 5, 1, 0];
var everyResult = values.every(function(item, index, array) {
    return item  >2;
});
console.log(everyResult);	// >false

var someResult = values.some(function(item, index, array) {
    return item  >2;
})
console.log(someResult);	// >true

var filterResult = values.filter(function(item, index, array) {
    return item > 2;
})
console.log(filterResult);	// >[5, 10, 15, 25, 15, 10, 5]

var mapResult = values.map(function(item, index, array) {
    return item * 2;
})
console.log(mapResult);		// >[0, 2, 10, 20, 30, 50, 30, 20, 10, 2, 0]

values.forEach(function(item, index, array) {
    //do some thing
});
```

###### 5.2.9 并归方法

> 并归方法不会影响原数组。
>
> reduce(): 迭代数组的所有项（从第一项开始逐个遍历到最后），然后返回一个最终的返回值。**（可用于求和）**
>
> reduceRight(): 迭代数组的所有项（从最后一项开始逐个遍历到第一项），然后返回一个最终的返回值。**（可用于求和）**
>
> 这两个方法都接收两个参数：一个在每一项上调用的函数和作为并归基础的初始值（可选）。
>
> 给reduce()和reduceRight()的函数接收4个参数：前一个值、当前值、索引值和数组对象。
>
> 
>
> Tip: 这两个函数的区别是从什么方向开始对数组进行遍历, 其他完全一样



``` javascript
var values = [0, 1, 5, 10, 15, 25, 15, 10, 5, 1, 0];
var reduceSum = values.reduce(function(prev, cur, index, array) {
    return prev + cur;
})
var reduceRightSum = values.reduceRight(function(prev, cur, index, array) {
    return prev + cur;
})
console.log(reduceSum);	// >87
console.log(reduceRightSum);	// >87
```

#### 5.3 Date 类型

> Date类型使用自UTC（Coordinated Universal Time, 国际协调时间）1970年01月01日零时开始经过的毫秒数来保存日期。在使用这种数据存储格式的条件下，Date类型保存的日期能够精确到1970年01月01日之前或之后的285616年。

```javascript
// 创建日期对象, 使用 new 操作符和 Date 构造函数即可
var now = new Date();	// 不传递参数时, 会自动获取当前时间
var someDate1 = new Date(Date.parse("May 25, 2004"));
var someDate2 = new Date("May 25, 2004");
// someDate1 等价于 someDate2

```

###### 5.3.1 继承的方法

> 与其他的引用类型一样，Date 类型也重写了 tocalString() 、toString() 和 valueOf() 方法；Date类型的  tocalString() 方法会按照与浏览器设置的地区相适应的格式返回日期和时间。

###### 5.3.2 日期格式化方法

> toDateString() ------- 以特定的于实现的格式显示星期几、年月日。
>
> toTimeString() ------- 以特定的于实现的格式显示时分秒和时区。
>
> toLocaleDateString() ------- 以特定于地区的格式显示星期几、年月日。
>
> toLocalTimeString() ------- 以特定于实现的格式显示时分秒。
>
> toUTCString() ------- 以特定于实现的格式完整的UTC日期。

###### 5.3.3 日期/时间组件方法

> getTime() ------ 返回表示日期的毫秒数，与valueOf()方法返回的值相同
> setTime(毫秒) ------ 以毫秒数设置日期，会改变整个日期
> getFullYear() ------ 取得四位数的年份
> getUTCFullYear() ------ 返回UTC日期的4位数年份
> setFullYear(年) ------ 设置日期年份，传入的年份值必须是四位数
> setUTCFullYear(年) ------ 设置UTC日期年份，传入的年份值必须是四位数
> getMonth() ------ 返回日期中的月份，0表示1月，11表示12月
> getUTCMonth()  ------ 返回UTC日期中的月份，0表示1月，11表示12月
> setMonth(月) ------ 设置日期的月份，传入的月份值必须大于0，超过11则增加年份
> setUTCMonth(月)  ------ 设置UTC日期的月份，传入的月份值必须大于0，超过11则增加年份
> getDate() ------ 返回日期月份中的天数（1到31）
> getUTCDate() ------ 返回UTC日期月份中的天数（1到31）
> setDate(日) ------ 设置日期月份中的天数，如果传入的值超过了该月中应有的天数，则增加月份
> setUTCDate(日) ------ 设置UTC日期月份中的天数，如果传入的值超过了该月中应有的天数，则增加月份
> getDay() ------ 返回日期中星期的星期几（0表示星期日，6表示星期六）
> getUTCDay() ------ 返回UTC日期中星期的星期几（0表示星期日，6表示星期六）
> getHours() ------ 返回日期中的小时数（0到23）
> getUTCHours()  ------ 返回UTC日期中的小时数（0到23）
> setHours(时) ------ 设置日期中的小时数，传入的值超过了23则增加月份中的天数
> setUTCHours(时) ------ 设置UTC日期中的小时数，传入的值超过了23则增加月份中的天数
> getMinutes() ------ 返回日期中的分钟数（0到59）
> getUTCMinutes() ------ 返回UTC日期中的分钟数（0到59）
> setMinutes(分) ------ 设置日期中的分钟数，传入的值超过59则增加小时数
> setUTCMinutes(分) ------ 设置UTC日期中的分钟数，传入的值超过59则增加小时数
> getSeconds() ------ 返回日期中的 秒数（0到59）
> getUTCSeconds() ------ 返回UTC日期中的 秒数（0到59）
> setSeconds(秒) ------ 设置日期中的秒数，传入的值超过59则增加分钟数
> setUTCSeconds(秒) ------ 设置UTC日期中的秒数，传入的值超过59则增加分钟数\
> getMilliseconds() ------ 返回日期中的毫秒数
> getUTCMilliseconds() ------ 返回UTC日期中的毫秒数
> setMilliseconds(毫秒) ------ 设置日期中的毫秒数
> setUTCMilliseconds(毫秒) ------ 设置UTC日期中的毫秒数
> getTimezoneOffset() ------ 返回本地时间与UTC时间相差的毫秒数。

#### 5.4 RegExp 类型

> ECMAScript 通过 RegExp 类型来支持正则表达式。使用下面类似 Perl 的语法，就可以创建一个正则表达式: var expression = / pattern / flags;
>
> 其中模式（pattern）部分可以是任何简单或复杂的正则表达式。每个正则表达式都可以带有一或多个标志（flags），用以标明正则表达式的行为。正则表达式的匹配模式支持下列三个标志。
>
> 1、g : 全局模式，即模式将被应用于所有字符串
>
> 2、i：表示不区分大小写模式
>
> 3、m : 表示多行模式，在达到文本末尾时还会继续查找下一行中是否存在与模式相匹配的项

```javascript
/*
* 匹配字符串中所有"at"的实例
*/
var pattern1 = /at/g;

/*
* 匹配第一个"bat"或"cat", 不区分大小写
*/
var pattern2 = /[bc]at/i;

/*
* 匹配所有以".at"结尾的3个字符的组合, 不区分大小写
*/
var pattern1 = /.at/gi;

```

> **模式中使用的所有元字符都必须转义。正则表达式中的元字符包括: " { [ ( \ ^ $ | ? * + . ) ] } "  **

```javascript
var re = null;
for (var i = 0; i < 5; i++) {
    re = /cat/g;
    re.test("catastrophe")
}
for (var i = 0; i < 5; i++) {
    re = new RegExp("cat", "g");
    re.test("catastrophe")
}
```

###### 5.4.1 RegExp 实例属性

> RegExp 的每个实例都具有下列属性，通过这些属性可以取得有关模式的各种信息
>
>  1、**global**：布尔值，表示是否设置了 g 标志。
>
>  2、**ignoreCase**：布尔值，表示是否设置了 i 标志。
>
>  3、**lastIndex**：整数，表示开始搜索下一个匹配项的字符位置，从0开始。
>
>  4、**multiline**：布尔值，表示是否设置了 m 标志。
>
>  5、**source**：正则表达式的字符串表示，按照字面量形式而非传入构造函数中的字符串模式返回。

```javascript
var pattern1=/\[bc\]at/i;
console.log(pattern1.global);         	// >false
console.log(pattern1.ignoreCase);  		// >true
console.log(pattern1.multiline);     	// >false
console.log(pattern1.lastIndex);    	// >0
console.log(pattern1.source);        	// >"\[bc\]at"

var pattern2 = new RegExp("\\[bc\\]at","i");
console.log(pattern2.global);         	// >false
console.log(pattern2.ignoreCase);   	// >true
console.log(pattern2.multiline);      	// >false
console.log(pattern2.lastIndex);     	// >0
console.log(pattern2.source);         	// >"\[bc\]at"

//尽管第一个模式使用的是字面量, 第二个模式使用了 RegExp 构造函数, 但它们的 source 属性是相同的. 可见, source保存的是规范形式的字符串, 记字面量形式所用的字符串.
```

###### 5.4.2 RegExp 实例方法

> exec(): 接受一个参数，即要应用模式的字符串，然后返回包含第一个匹配项信息的数组。
>
> test(): 接受一个字符串参数。在模式与该参数匹配的情况下返回true；否则，返回false。

```javascript
//exec() 
var textString = "mom and dad and baby";
var pattern = /mom(and dad(and baby)?)?/gi;
var matches = pattern.exec(textString);
console.log(matches.index);   // >0
console.log(matches.input);   // >"mom and dad and baby"
console.log(matches[0]);     // >"mom and dad and baby"
console.log(matches[1]);     // >"and dad and baby"
console.log(matches[2]);     // >"and baby"

//test()
var phone = '18333336035';
var phoneReg = /^[1][3,4,5,7,8][0-9]{9}$/;
if (phoneReg.test(phone)) {
    console.log("正确的手机号");
}

```

###### 5.4.3 RegExp 构造函数属性

|   长属性名   | 短属性名 |                             说明                             |
| :----------: | :------: | :----------------------------------------------------------: |
|    input     |    $_    |         最近一次要匹配的字符串。opera未实现这个属性          |
|  lastMatch   |    $&    |            最近一次地匹配项，opera未实现这个属性             |
|  lastParen   |    $+    |          最近一次匹配的捕获组，opera未实现这个属性           |
| leftContext  |    &`    |               input字符串中lastMatch之前的文本               |
|  Multiline   |    $*    | 布尔值，表示是否所有表达式都使用多行模式；所有浏览器都不再实现该属性 |
| rightContext |    $’    |               input字符串中lastMatch之后的文本               |

```javascript
var text = 'this has been a short summer';
// 匹配任何一个字符后跟hort, 而且把第一个字符放在了一个捕获组中;
var pattern = /(.)hort/g;
if (pattern.test(text)) {
    console.log(RegExp);
    console.log(RegExp.input);     		// RegExp.$_
    console.log(RegExp.lastMatch);   	// RegExp.["$&"]
    console.log(RegExp.leftContext);   	// RegExp.["&`"]
    console.log(RegExp.rightContext);   // RegExp.["$'"]
    console.log(RegExp.lastParen);   	// RegExp.["$+"]
    console.log(RegExp.multiline);   	// RegExp.["$* "]
}
```

###### 5.4.4 模式的局限性

> 尽管 ECMAScript 中的正则表达式功能还是比较完备的，但仍然缺少某些语言所支持的高级正则表达式特性。下面是 ECMAScript 正则表达式不支持的特性。
>
> 1、匹配字符串开始和结尾的 \A 和 \Z 锚
>
> 2、向后查找
>
> 3、并集和交集
>
> 4、原子组
>
> 5、Unicode 支持
>
> 6、命名的捕获
>
> 7、s（single, 单行）和 x （free-spacing, 无间隔）匹配模式
>
> 8、条件匹配
>
> 9、正则表达式注释

#### 5.5 Function 类型

###### 5.5.1 没有重载（深入理解）

> 将函数名想象为指针，并结合 ECMAScript 中一切皆对象的思想，也有助于理解为什么 ECMAScript 中没有函数重载的概念。

```javascript
function sum(num) {
    return num + 100;
}

function sum(num) {
    return num + 200;
}

var result = sum(100); // >300

//以上代码等价于

var sum = function(num) {
    return num + 100;
}
sum = function(num) {
    return num + 200;
}
var result = sum(100); // >300
```

> 结合以上代码，可以发现在创建第二个函数时，实际上覆盖了引用第一个函数的变量 sum。

###### 5.5.2 函数声明与函数表达式

> 函数声明与函数表达式的区别：
>
> ​	1、解析器会优先读取函数声明，并使其在执行任何代码之前可以访问
>
> ​	2、解析器解析函数表达式时，必须等到执行到函数表达式的代码行，才会被解释执行

```javascript
console.log(sum(10, 10));	// >20
function sum(num1, num2) {
    return num1 + num2;
}

console.log(sum(10, 10));	// >sum is not a function (Chrome 87.0.4280.88)
var sum = function (num1, num2) {
    return num1 + num2;
}

```

###### 5.5.3 作为值的函数

> 因为 ECMAScript 中的函数名本身就是变量， 所以函数也可以作为值来使用。也就是说，不仅可以像传递参数一样把一个函数传递给另一个函数，而且可以将一个函数作为另一个函数的结果返回。

```javascript
function callSomeFunction(someFunction, someArgument) {
    return someFunction(someArgument);
} 

function add10(num) {
    return num + 10;
}

var result1 = callSomeFunction(add10, 10);
console.log(result1);	// >20

function getGreeting(name) {
    return 'Hello, ' + name
}

var result2 = callSomeFunction(getGreeting, 'wwh'),
console.log(result2);	// >Hello, wwh

```

> 这里的 callSomeFunction() 函数是通用的，即无论第一个参数中传递进来的是什么函数，它都会返回执行第一个参数后的结果。<font color=red>在访问函数指针而不执行函数时，必须去掉函数名后面的圆括号</font>。 



> 当然，我们也可以从一个函数中返回另一个函数。

```javascript
function createComparisonFunction(propertyName) {
    return function(object1, object2) {
        var value1 = object1[propertyName];
        var value2 = object2[propertyName];
        if (value1 < value2) {
            return -1;
        } else if (value1 > value2) {
            return 1;
        } else {
            return 0;
        }

    }
}

var data = [{name: 'zjq', age: 28}, {name: 'wwh', age: 25}];
data.sort(createComparisonFunction('name'));
console.log(data[0].name)	// >wwh
```

###### 5.5.4 函数内部属性

> 在函数内部，有两个特殊的对象： arguments 和 this 。其中， arguments 在第三章介绍过，它是一个保存了所有传入的参数的对象，arguments 还有一个名叫 callee 的属性，改属性是一个指针，指向拥有这个 arguments 对象的函数



```javascript
function factorial(num) {
    if (num <= 1) {
        return 1;
    } else {
        return num * factorial(num - 1)	// 等价于 return num * arguments.callee(num - 1)
    }
}

// arguments.callee 可以解除递归与函数名之间的耦合
```

```javascript
var factorial = function (num) {
    if (num <= 1) {
        return 1;
    } else {
        return num * arguments.callee(num - 1)
    }
}

var trueFactorial = factorial;
factorial = function() {
    return 0;
}
console.log(trueFactorial(5));	// >120
console.log(factorial(5));	// >0
```



> 函数内部的另一个特殊对象是this，this 引用的是函数据以执行的环境对象----或者也可以说是this值（当在网页的全局作用域中调用函数时，this对象引用的就是window）

```javascript
window.color = 'red';
var o = {color: 'blue'};
function sayColor() {
    console.log(this.color)
}
sayColor();		// >red
o.sayColor = sayColor;
o.sayColor();	// >blue
```



###### 5.5.5 函数属性和方法

> ESMAScript 中的函数是对象，因此函数也有属性和方法。每个函数都包含两个属性: length 和 prototype 。其中 length 表示函数希望接收的命名参数的个数，prototype 是保存它们所有实例方法的真正存在。ESMAScript 5  中，prototype 属性是不可枚举的，因此使用 for-in 无法发现

> 每个函数都包含两个非继承而来的方法： apply() 和 call() 
>
> apply(): 接收两个参数，一个是其中运行函数的作用域，另一个参数是数组。其中，第二个参数可以是Array实例，也可以是 arguments 对象。
>
> call(): 与apply() 方法的作用相同，第一个参数是this， 其余参数都是直接传递给函数的。在使用call() 方法是，传递给函数的参数必须逐个列举出来。



```javascript
//apply

function sum(num1, num2) {
    return num1 + num2;
}

function applySum1(num1, num2) {
    return sum.apply(this, arguments);
}

function applySum2(num1, num2) {
    return sum.apply(this, [num1, num2]);
}
```

```java
//call

function sum(num1, num2) {
    return num1 + num2;
}

function callSum(num1, num2) {
    return sum.call(this, num1, num2);
}
```

```javascript
//bind

window.color = 'red';
var o = {color: 'blue'};
function sayColor() {
    console.log(this.color);
}
var objectSayColor = sayColor.bind(o);
objectSayColor(); 	// >blue
```

#### 5.6 基本包装类型

> 为了便于操作基本类型值，ECMAScript提供了3个特殊的引用类型： Boolean、Number和String

#### 5.6.1Boolean类型

> 随便写两个字