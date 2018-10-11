# JavaScript基础拾遗之一 —— 类型

JavaScript中分两类数据类型，原始数据类型和对象数据类型。原始数据类型包括：数字、字符串和布尔值，还有两种特殊的原始值null和undefined。对象数据类型包括：Object，Function，Array等.



## 1.数字

JavaScript中不区分整数和浮点数值，所有数字都用浮点数值表示，用64位浮点格式表示，范围类似C#中double数字类型。

### 1.1 整型

`1` `0` `10000`

### 1.2 浮点型

`0.1`

`3.14` 

`.3333333 //0.3333`

`3.14e32 //3.14 × 10³²`

`3.14E-32 //3.14 × 10﹣³²`

### 1.3 十六进制

仅支持16进制，不支持8进制写法

`0xff //255`

### 1.4 Infinity、-Infinity、NaN、-0

`Infinity //无穷大 Number.MAX_VALUE + 1 / Number.POSITIVE_INFINITY`

`-Infinity //负无穷大 -Number.MAX_VALUE - 1 / Number.NEGATIVE_INFINITY` 

`NaN //Not a number ,0/0 零除零是没有意义的`

`-0  //-1 ÷ Infinity` 

## 2.字符串
JavaScript中所有字符都是16位的，通常是用Unicode字符集中的字符。
是由单引号或双引号括起来的字符序列。

`""`
`"hello"`
`'hello'`
`'name="gaygayboy"'`
`"I'm hero"`
`fuck\nworld`
`fuck \
work`
### 2.1 字符串转义

反斜杠（\）后加一个字符就不再表示原来的含义，比如
`\n` // 换行符 \u000A
`\r` // 回车符 
`\"` // "
`\'` // '
`\\` // \
反斜杠加一个字符u再加十六进制编码，表示Unicode的某些编码
`\u03c3` \\π

### 2.2 字符串操作

使用 + 进行连接 `'hello'+' '+'world'`=>` 'hello world'`

`var str = 'hello,world'` 

`str.charAt(0)` => 'l'   //查找第一个字符

`str.substring(1,4)` => "ello" //截取2~4位字符串

`str.slice(1,4)` => "ello"  //同上

`str.slice(-3)` => "rld" //截取最后三位

`str.indexOf("l")` => 2 //字符l 首次出现的位置

`str.indexOf("l",3)` => 3 //字符l在位置3之后首次出现的位置

`str.lastIndexOf("l")` => 10 //字符l最后出现的位置

`str.split(",")` => ["hello","world"] // 分拆成数组

`str.replace("h","H")` => "Hello world" //替换

`str.toUpperCase()` => "HELLO WORLD" //转成大写


## 3.布尔值

保留字true 、false

任意值都可以转为布尔值，以下几个会被转为false

`undefined`
`null`
`0`
`-0`
`NaN`
`""`
除此之后所有值都为true

## 4.undefined、null
null表示空值，使用`typeof null`显示null为object类型，null是null对象中的唯一成员。
可表示数字，对象和字符串为“无值”的
undefined表示未定义的值，一般指示值没有初始化，或者属性值未定义。

## 5.对象

JavaScript中简单类型包括数字、字符串、布尔值、undefined和null。其他的所有的值都是对象。JavaScript中类型分为不可变的原始值和可变的引用对象，相对于C#中的值类型和引用类型。简单类型都是不可变额原始值类型，object，数组，日期，函数，包括正则表达式都是对象。以下例子说明值类型和引用类型区别：

```javascript
var a = "test";
var b = "test";
a === b //true
```

```javascript
var a = {x: 0}
var b = {x: 0}
a === b //false
```

```javascript
var a = [0,1,2]
var b = a;
a === b //true
```
当进行对象比较的时候，JavaScript比较的是引用地址，所以相同对象值不同引用地址比较是false。
我们比较对象值是否相等的时候，可遍历对象属性值进行比较：
```javascript
function equal(a, b){ //仅适合当两个对象的属性顺序相同的时候。
    if(!a || !b) return false; // 其中一个为 null则为false
    return JSON.stringify(a) === JSON.stringify(b); //对比生成的字符串
}
```

对象比较也可以用hash方法进行比较，深度比较还需考虑对象类型等因素。参考 [Stack Overflow](https://stackoverflow.com/questions/1068834/object-comparison-in-javascript)
值得注意的是，JavaScript中所有函数的参数都是按值传递的。也就是说把外部的值复制到内部参数，如果外部类型的值是基本类型，那么就直接复制值到参数上， 如果外部的值是引用类型，那么就把引用复制到参数上。
```javascript
function add(num){
    num += 1;
    return num;
}

var val = 10;
var result = add(val);

console.log(val); //输出10
console.log(result); //输出11
```

```javascript
function setName(obj){
    obj.name = "Xiao Ming";
}

var obj = {};

setName(obj);

console.log(obj.name); //输出 Xiao Ming
```