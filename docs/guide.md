## 指南

本文档主要用于记录一些平时在浏览文章时，看到的正则，并试图理解它，知道表达式是如何实现匹配的。对我来说，正则是个晦涩难懂的东西，
即便知晓了它的语法，也很难运用起来。所以想要先通过学会看，学会理解，学会用，到最后变成学会自己写。

一些文档：

[javascript正则表达式语法](http://www.runoob.com/js/js-regexp.html)


[在线正则表达式测试](http://tool.oschina.net/regex/)

### 表示方式

有两种表示方式

```js
var patt1 = new RegExp('e', 'g');
// RegExp 对象有 3 个方法：test()、exec() 以及 compile()。
// test() 方法检索字符串中的指定值。返回值是 true 或 false。
// exec() 方法检索字符串中的指定值。返回值是被找到的值。如果没有发现匹配，则返回 null。
// compile可以重新指定正则实例的规则与修饰符。 patt1.compile('d', 'i')
var patt2 = /ABC\-001/g;
```

### 支持正则的String方法

> 除了RegExp对象具有支持正则表达式的方法外，字符串String对象也具有可以支持正则表达式作为参数进行匹配筛选的的方法。

#### replace()

```js
var str = 'i see you See you';
var pattern = /you/;
str.replace(pattern,'*'); // -> i see * See you
// replace回调
const str = '2016/10/20';
const pattern = new RegExp('(\d+)(\/)', 'g');
let data = str.replace(pattern, (result, $1, $2) => {
  console.log(result, $1, $2); 
  // 两个result 2016/ 10/, 四个$ $1: 2016 $2: /   $1: 10 $2: /,replace掉result，变成$1+'.',即2016/变成2016. 10/变成10.
  return `${$1}.`;
});

// 假设想要replaceAll，使用这个函数模式就比较好实现
const str = '2016/10/20';
const pattern = new RegExp('\/', 'g');
data = str.replace(pattern, (result) => {
  return '.';
});
```

#### match()

> match 根据匹配规则pattern匹配指定的字符串str，如果匹配成功则返回一个数组格式的结果用于存放匹配文本有关的信息，如果没有匹配到则返回null。

```js
const str = '2016/10/20';
const pattern = new RegExp('\/', 'g');
str.match(pattern); // ['/', '/']
'2016'.match(pattern); // null
```

#### split()

```js
var str = 'hello world';
str.split(/\o/g); // ['hell', ' w', 'rld'], 使用o分隔成了三个元素
```

#### search()

> 根绝匹配规则pattern在字符串中检索指定的结果，如果检索到则返回该结果首字母在原字符中的索引，否则返回-1。其功能类似于indexOf,只是indexOf并不支持正则匹配。

```js
var str = 'hello world';
str.search(/\o/g); // 4
```

> 注意：该方法忽略全局修饰符g，也不支持lastIndex也就是意味着它不能被多次调用，一旦检索到结果，便会停止检索。

先说到这吧，具体的应用和表达式会在后面的文档中详细介绍。