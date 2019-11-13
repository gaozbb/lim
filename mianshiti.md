### 两行代码的PHP面试题
请问，输出什么，为什么？
~~~
<?php

$str='php';
$str['name']=array('dogstar');

var_dump($str);
~~~

这道面试题下面说，如果能答对，至少说明两点
* 你是一个细心的人
* 对PHP语言的理解非常到位

网友的答案很多，回答最多的答案就是，输出一个数组，即：array('dogstar')。
因为在他们认为，把字符串当做数组使用，会把变量转换一个数组类型，所以得出这个结果。

首先，看第一行代码
~~~
<?php

$str='php';
~~~
把字符串赋值给了变量$str

看第二行代码
~~~
<?php

$str['name']=array('dogstar');
~~~

别急看代码，首先看代码之前我们回顾一下基础知识！
php的基本数据类型都有哪些？
String字符串，Integer整型，FLoat浮点型，Boolean布尔型，Array数组，Object对象，Resource资源值，Null空值

看第二行代码之前看一个简单的代码
~~~
$arr=array();

$arr[0] = 'A';
$arr['x'] = 'B';
$arr[1] = 'C';
$arr['y']= 'D';
$arr[] = 'E';			//没有下标
~~~
问：最后E字母对应的数组下标是什么？

PHP数组的下标类型，PHP官方文档有记载，http://php.net/manual/zh/language.types.array.php
~~~
可以用 array() 语言结构来新建一个数组。它接受任意数量用逗号分隔的 键（key） => 值（value）对。

array(  key =>  value
     , ...
     )
// 键（key）可是是一个整数 integer 或字符串 string
// 值（value）可以是任意类型的值
~~~
读取关键信息`// 键（key）可是是一个整数 integer 或字符串 string`
就是说，PHP数组的下标由两种类型，一种是整数，一种是字符串

输出一下下面代码
~~~
$a = 'PHP';

echo $a[0],"<br>";
echo $a[1],"<br>";
echo $a[5],"<br>";
~~~
php中的字符串可以当做一个数组的形式


~~~
<?php

$str['name'] = array('dogstar');
~~~
$str不是一个字符串，是一个数组。
* PHP字符串可以通过下标操作，但是有效的是0、1、2这种数字
* PHP下标由两种类型，可以是整数或者是字符串


看面试题之前，看一下字符串转整数的规则
~~~
<?php

echo intval('123'),"<br>";
echo intval('asd'),"<br>";
echo intval('123asd'),"<br>";
echo intval('asd123'),"<br>";
echo intval('1as2d3'),"<br>";
~~~

php转换整型的规则，官方链接http://php.net/manual/zh/language.types.string.php#language.types.string.conversion
~~~
该字符串的开始部分决定了它的值。如果该字符串以合法的数值开始，则使用该数值。否则其值为
   0（零）。合法数值由可选的正负号，后面跟着一个或多个数字（可能有小数点），再跟着可选的指数部分。指数部分由
   'e' 或 'E' 后面跟着一个或多个数字构成。
~~~
![](https://static.oschina.net/uploads/space/2017/0930/163239_ucmk_256338.png)

简单来说，从第一个开始，一直连续的有效部分都会转换成整数


再看这道题
~~~
<?php
$str['name']

转换整数，即
<?php
intval('name');
~~~
结果很容易得出，字符串"name"会转换成0

现在看一下整体的题
~~~
<?php
$str = 'php';
$str['name']=array('dogstar');
var_dump($str);

变成了
<?php
$str = 'php';
$str['0']=array('dogstar');
var_dump($str);
~~~

下面进行php的数组转换成字符串
~~~
<?php
echo strval(array('dogstar'));			//结果为？
~~~

随意题目简化成了
~~~
<?php
// $str['name'] = array('dogstar');
// $str[0] = array('dogstar');
$str[0] = 'Array'; 
var_dump($str);
~~~
所以打印出字符串Array的0下标，会打印出A，答案：A