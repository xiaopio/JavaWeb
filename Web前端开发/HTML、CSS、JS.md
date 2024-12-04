# HTML

超文本标记语言

超文本：超越了文本的限制

标记语言：由标签构成的语言



## 水平分割线

```html
<hr>
```

## 表格

```html
<style>
    td {
        text-align: center; /* 单元格内容居中展示 */
    }
</style>
```

```html
<table border="1px" cellspacing="0"  width="600px">
    定义表格中的行，一个<tr>表示一行
    <tr>
        表头单元格，具有加粗居中效果
        <th>序号</th>
        <th>品牌Logo</th>
        <th>品牌名称</th>
        <th>企业名称</th>
    </tr>
    <tr>
        普通单元格
        <td>1</td>
        <td> <img src="img/huawei.jpg" width="100px"> </td>
        <td>华为</td>
        <td>华为技术有限公司</td>
    </tr>
    <tr>
        <td>2</td>
        <td> <img src="img/alibaba.jpg"  width="100px"> </td>
        <td>阿里</td>
        <td>阿里巴巴集团控股有限公司</td>
    </tr>
</table>
```

## 表单

```html
  <!-- form表单属性：
     action：表单提交url，往何处提交数据
    method：表单提交方式
     	get：在url后面拼接表单数据，比如：?username=Tom&age=12，url长度有限制，默认模式
      	post：在消息体（请求体）中传递，参数大小无限制-->
  <form action="" method="post">
    用户名：<input type="text" name="username">
    年龄：<input type="text" name="age">
    <input type="submit" value="提交">
  </form>
```

**注意**：表单项必须有name属性才可以提交

### 表单项

```java
<input>：表单项，通过type属性控制输入格式
<select>：定义下拉列表，<option>定义列表项
<textarea>文本域
```

<form action="" method="post">
    姓名：<input type="text" name="name"><br><br>
    密码：<input type="password" name="password"><br><br>
    性别：<label for=""><input type="radio" name="gender" value="1">男</label>
    <label for=""><input type="radio" name="gender" value="0">女</label><br><br>
    爱好：<label for=""><input type="checkbox" name="hobby" value="java">Java</label>
    <label for=""><input type="checkbox" name="hobby" value="game">Game</label>
    <label for=""><input type="checkbox" name="hobby" value="sing">Sing</label><br><br>
    图像：<input type="file" name="image" id=""><br><br>
    生日：<input type="date" name="birthday" id=""><br><br>
    时间：<input type="time" name="time" id=""><br><br>
    日期时间：<input type="datetime-local" name="datetime-local" id=""><br><br>
    邮箱：<input type="email" name="email" id=""><br><br>
    年龄：<input type="number" name="age" id=""><br><br>
    学历：<select name="degree" id="">
    <option value="">----------请选择----------</option>
    <option value="1">大专</option>
    <option value="2">本科</option>
    <option value="3">硕士</option>
    <option value="4">博士</option>
    </select><br><br>
    描述：<textarea name="description" cols="30" rows="10" id=""></textarea> <br><br>
    <!-- 表单常见按钮 -->
    <input type="button" value="按钮">
    <input type="reset" value="重置">
    <input type="submit" value="提交">
    <br>
</form>

# CSS

叠层样式表，用于控制网页的样式

 CSS样式：

​    行内样式：直接写在标签的style属性中（不推荐）

​    内嵌样式：写在style标签中（可以写在页面任何位置，但通常约定写在head标签中）

​    外联样式：写在一个单独的.css文件中（需要通过link标签在网页中引入）

颜色表示：

​	关键字：red

​	rgb表示法：rgb(255,0,0)

​	十六进制：#ff0000

颜色属性：

​	color

盒子模型：

内容区域（content）、内边距区域（padding）、边框区域（border）、外边距区域（margin）

### CSS选择器

选择标签用的

#### 基础选择器

##### 标签选择器

写上标签名

##### 类选择器

结构需要用class属性来调用class类的意思

##### id选择器

*样式#定义，结构id调用，只能调用一次，别人切勿使用*

类选择器：可以多次使用

id选择器：只能使用一次

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>CSS样式</title>
  <style>
    /* 选择器 {样式} */
    /* 给谁修改样式 {改什么样式} */
    /* 标签选择器：标签名 {} */
    p {
      color: red;
      /* 修改文字大小 */
      font-size: 20px;
    }
    div {
      color: pink;
    }
    /* 类选择器：样式点定义 结构类（class）调用 一个或多个 开发最常用 */
    .red {
      color: red;
    }
    .font35 {
      font-size: 35px;
    }
    .box {
      width: 100px;
      height: 100px;
    }
    .div-red {
      background-color: red;
    }
    .div-yellow {
      background-color: yellow;
    }
    .div-green {
      background-color: green;
    }
    /* id选择器：样式#定义，结构id调用，只能调用一次，别人切勿使用 */
    #pink {
      color: pink;
    }
  </style>
</head>
<body>
  <p>体验CSS语法规范</p>
  <div>女生</div>
  <ul>
    <li class="red">第一行</li>
    <li>第二行</li>
    <li>第三行</li>
    <li>第四行</li>
  </ul>
  <div class="div-red box"></div>
  <div class="div-yellow box"></div>
  <div class="div-green box"></div>
  <div class="red font35">刘德华</div>
  <div id="pink">吴彦祖</div>
</body>
</html>
```

##### 通配符选择器

 *{属性1： 属性值1 ... } 选择所有标签

### 字体属性

##### 字体

```
font-family: 'Microsoft Yahei';
```

##### 文字大小

```
font-size: 16px;
```

标题比较特殊，需要单独调整大小

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>CSS样式</title>
  <style>
    h2 {
      font-family: 'Microsoft Yahei';
      /* font-weight: normal; */
      font-weight: 400;
    }
    p {
      font-family: 'Courier New', Courier, monospace;
      font-size: 16px;
    }
    .bold {
      /* font-weight: bold; */
      /* 700后面不要跟数字，等价于bold加粗效果 */
      /* 实际开发中更常用数字 表示加粗或变细 */
      font-weight: 700;
    }
  </style>
</head>
<body>
  <h2>Hello World</h2>
  <p>体验</p>
  <p class="bold">CSS</p>
  <p>语法</p>
  <p>规范</p>
</body>
</html>
```

##### 文字样式

```
/* 斜体 */
font-style: italic;
```

更多时候要使用斜体字，使用em、i标签，要变为正常样式时设置

```
font-style: normal;
```

##### 复合属性

字体大小*font-size*和字体*font-family*不能省略

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>CSS样式</title>
  <style>
    div {
      /* font-style: italic;
      font-weight: 700;
      font-size: 16px;
      font-family: 'Microsoft Yahei'; */
      /* 复合属性：简写方式 节约代码 */
      /* font: font-style font-weight font-size/font-height font-family */
      font: italic 700 16px 'Microsoft Yahei';
    }
  </style>
</head>
<body>
  <div>马踏飞燕</div>
</body>
</html>
```

### 文本属性

##### 文本颜色

```
color: red;
color: #ff0000;
color: rgb(255, 0, 0) 或 rgb(100%, 0%, 0%)
```

##### 文本对齐

```
text-align: center;
text-align: left;
text-align: right;
```

##### 装饰文本

```
/* 上划线 */
text-decoration: overline;
/* 删除线 */
text-decoration: line-through;
/* 下划线 */
text-decoration: underline;
/* 取消下划线 */
text-decoration: none;
```

##### 文本缩进

```
/* 文本的首行缩进 缩进多少距离 */
text-indent: 20px;
/* 当前元素两个文字大小 */
text-indent: 2em;
```

##### 行间距

行高

```
line-height: 16px;
```

### CSS的引入方式

##### 内部样式表（内嵌样式表）

html页面内，style标签中 嵌入式引用

##### 行内样式表 

在元素标签内部的style属性中设置CSS样式，适合于修改简单样式

##### 外部样式表

单独写一个CSS文件，link标签引入html页面中

```
<link rel="stylesheet" href="../css/style.css">
```

# JavaScript

JavaScript：一门跨平台、面向对象的脚本语言。用来控制网页行为，它能使网页可交互

## js引入方式

```
内部脚本：将JS代码定义在HTML页面中

​	JS代码必须放置在<script></script>标签之间

​	在HTML文档中，可以在任意位置，放置任意数量的<script>

​	一般会把脚本放置于<body>元素的底部，可改善显示速度

外部脚本：将JS代码定义在外部JS文件中，然后引入到HTML页面中
```

## js基础语法

### 书写语法

```
区分大小写
每行结尾的分号可有可无
注释：
​	单行：//
​	多行：/*	*/
大括号表示代码块
// 判断
if(count == 3){
	alert(count);
}
```

### 输出语句

```html
// 弹出警告框
window.alert("HELLO");
// 写入html页面中
document.write("Hello");
// 浏览器控制台输出
console.log("hello");
```

### 变量

```
JavaScript中用**var**关键字（variable的缩写）来声明变量

JavaScript是一门弱类型语言，变量**可以存放不同类型的值**

变量名需要遵循如下规则：

    组成字符可以是任何字母、数字、下划线或美元符号

    数字不能开头

    建议使用驼峰命名
```

```js
// var a = 10;
// a = "张三";
// alert(a);
// 特点1：作用域比较大，是全局变量
// 特点2：可以重复定义
{
    var x =1;
    var x = "b";
    alert(x);
}
{
    var x = "a";
    alert(x);
}
// ES6新增了let关键字来定义变量。用法类似var，但是所声明的变量，只在let关键字所在的代码块内有效，且不允许重复声明。
// ES6新增了const关键字，用来声明一个只读的常量，一旦声明，常量的值就不能改变。
```

#### var let const

```js
// var a = 10;
// a = "张三";
// alert(a);
// 特点1：作用域比较大，是全局变量
// 特点2：可以重复定义
// {
//     var x =1;
//     var x = "b";
//     alert(x);
// }
// {
//     var x = "a";
//     alert(x);
// }
// ES6新增了let关键字来定义变量。用法类似var，但是所声明的变量，只在let关键字所在的代码块内有效，且不允许重复声明。
// ES6新增了const关键字，用来声明一个只读的常量，一旦声明，常量的值就不能改变。
{
    // let：局部变量，不能重复定义
    let a = 10;
    // Cannot redeclare block-scoped variable 'a'.
    // let a = "A";
    a = "张三";
    alert(a);
}
// 没有拿到
// alert(a);
// const：常量，不能改变
const pi = 3.14;
// pi = 3.1415;
// Uncaught TypeError: Assignment to constant variable.
console(c);
```

### 数据类型

JavaScript中分为：原始类型 和 引用类型

```
原始类型
	number：数字（整数、小数、NaN(Not a Number)）
	string：字符串，单双引皆可
	boolean：布尔。true、false
	null：对象为空	类型：object
	undefined：当声明的变量未初始化时，该变量的默认值为undefined
```

使用typeof运算符可以获取数据类型：

```js
var a  = 10;
alert(typeof a);
```

#### 基本运算符

唯一特殊：===全等

== 会进行类型转换	===不会进行类型转换

#### 类型转换


```js
// 12
alert(parseInt("12"));
// 12
alert(parseInt("12A34"));
// NaN
alert(parseInt("A45"));
```


```js
// 类型转换--其他类型转换为boolean
if(0){
    alert("0转换为false")
}
if(NaN){
    alert("NaN转换为false")
}
if(-1){
    alert("除0和NaN其他转换为true")
}
if(""){
    alert("空字符串为false，其他都是true")
}
if(null){
    alert("null转化为false")
}
if(undefined){
    alert("undefined转化为false")
}
```
### 流程控制

if...else	...

## js函数

函数（方法）被设计为执行特定任务的代码块

JavaScript函数通过function关键字进行定义，语法为：

function functionName(参数1,参数2...){

​	// 要执行的代码

}

注意：

​	形式参数不需要类型。因为JavaScript是弱类型语言

​	返回值也不许要定义类型，可以在函数内部直接使用return返回即可

调用：函数名（实际参数列表）

```js
// 定义函数
function add(a,b){
    return a + b;
}
// 调用函数
var result =  add(10,20);
// number 30
alert(result);
alert(typeof(result));
```

```js
// 第二种定义方式    
var add = function(a,b){
    return a + b;
}
var result = add(10, 20);
alert(result);
```

细节：调用时传入参数个数超过定义个数，不会报错，定义几个传递几个

## js对象

### 基础对象

#### Array

var 数组名 = new Array(元素列表);

var 数组名 = [元素列表];

```js
// 定义
var arr1 = new Array(1, 2, 3, 4);
var arr2 = [1, 2, 3, 4];
// 访问
console.log(arr1[0]);
console.log(arr1[1]);
```

```js
// 特点：长度可变
var arr = [1, 2, 3, 4];
arr[10] = 50;
// 50
console.log(arr[10]);
// undefined
console.log(arr[9]);
// undefined
console.log(arr[8]);
arr[8] = true;
arr[9] = "A";
// [1, 2, 3, 4, empty × 4, true, 'A', 50]
console.log(arr);
```

遍历数组

```js
var arr = [1, 2, 3, 4];
for (let i = 0; i < arr.length; i++) {
        console.log(arr[i]);        
}
```

```js
// forEach中要传递函数，每遍历一个数，调用一次函数
var arr = [1, 2, 3, 4];
arr.forEach(function(e){
    console.log(e)
})
// 简化
// 箭头函数：
// 		(...) => {...}
arr.forEach((e) => {
    console.log(e)
})
```

区别：

for：遍历数组中所有元素

forEach：遍历数组中有值的元素

push：添加元素

```js
arr.push(5);
arr.push(6);
```

splice：删除元素

参数一：起始索引

参数二：删除元素个数

```js
var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
arr.splice(2,2);
arr.forEach((e) => {
    // 1 2 5 6 7 8 9
    console.log(e);
})      
```

#### String

var 变量名 = new String("...");

var 变量名 = "...";

属性：

​	length字符串长度

方法：

​	charAt()	返回在指定位置的字符

​	indexOf()	检索字符串

​	trim()	去除字符串两边的空格

​	substring()	提取字符串中两个指定的索引号之间的字符

```js
var str1 = new String("Hello String"); 
var str2 = "  Hello String  "; 
console.log(str1);
console.log(str2);
// length
console.log(str1.length);
console.log(str2.length);
// charAt()
console.log(str1.charAt(0));
// indexOf
console.log(str1.indexOf("lo"));
var s = str2.trim();
console.log(s);
// substring(start, end) --- 开始索引，结束索引（含头不含尾）
// Hello
console.log(s.substring(0,5))
```

### JavaScript自定义对象

定义格式：

​	var 对象名 = {

​			属性名1：属性值1，

​			属性名2：属性值2，

​			属性名3：属性值3，

​			属性名4：属性值4，

​			属性名5：属性值5，

​			函数名称：function(参数列表){}

}；

调用格式：

​	对象名.属性名；

​	对象名.函数名()；

```js
// 自定义对象
var user = {
    name:"Tom",
    age:10,
    gender:"male",
    // eat:function(){
    //     alert("用膳~");
    // }
    eat(){
        alert("用膳~");
    }
}
alert(user.name);
user.eat();
```

#### JSON

json是通过Javascript对象标记法书写的文本

用于网络数据传输

#### 基础语法

定义：

​	var 变量名 =  ‘{"key1" : value1, "key2" : value2}’ ;

示例：

​	var 变量名 =  ‘{"name" : “张三”, "age" : 18,“address”:["北京"，“上海”，“西安”]}’ ;

value的数据类型：
	数字（整数或浮点数）

​	字符串（在双引号中）

​	逻辑值（true或false）

​	数组（在方括号中）

​	对象（在花括号中）

​	null

JSON字符串转为JS对象

var jsObject = JSON.parse(userStr);

JS对象转为JSON字符串

var jsonStr = JSON.stringify(jsObject);

```js
var jsonStr = '{"name":"张三", "age":18 , "addr":["北京", "上海", "西安"]}';
var obj = JSON.parse(jsonStr);
alert(obj.name);
```



### 浏览器对象模型BOM

#### BOM

```js
// 获取window对象
window.alert("Hello BOM");
alert("Hello BOM window");

// 方法：
// confirm - 对话框
var flag =  confirm("您确认删除该记录吗？");
// true确定 false取消
alert(flag);

// 定时器 - setInterval -- 周期性的执行某一个函数
var i = 0;
setInterval(function() {
    i++;
    console.log("定时器执行了"+ i + "次"); 
}, 2000);

// 定时器 - setTimeout -- 延迟一定时间只执行一次
setTimeout(function(){
    alert("延时结束");
},3000)

// location
// 获取浏览器地址栏
alert(location.href);

location.href = "https://www.baidu.com/";
```



### 文档对象模型DOM

#### DOM

将标记语言的各个组成部分封装成对应的对象：

​	Document：整个文档对象

​	Element：元素对象

​	Attribute：属性对象

​	Text：文本对象

​	Comment：注释对象

JavaScript通过DOM，都HTML进行操作：

​	改变HTML元素的内容

​	改变HTML元素的样式（CSS）

​	对HTML DOM事件做出反应

​	添加和删除HTML元素

```js
<body>
    <div style="font-size: 30px;text-align: center;" id="tb1">课程表</div>
    <table width="800px" border="1" cellspacing="0" align="center">
        <tbody>
            <tr>
                <th>学号</th>
                <th>姓名</th>
                <th>分数</th>
                <th>评语</th>
            </tr>
            <tr align="center" class="data">
                <td>001</td>
                <td>张三</td>
                <td>90</td>
                <td>优秀</td>
            </tr>
            <tr align="center" class="data">
                <td>002</td>
                <td>李四</td>
                <td>80</td>
                <td>良好</td>
            </tr>
            <tr align="center" class="data">
                <td>003</td>
                <td>王五</td>
                <td>70</td>
                <td>一般</td>
            </tr>
            <tr align="center" class="data">
                <td>004</td>
                <td>赵六</td>
                <td>60</td>
                <td>及格</td>
            </tr>
        </tbody>
    </table>
    <br>
    <div style="text-align: center;">
        <input id="bt1" type="button" value="改变标题内容" onclick="fn1()">
        <input id="bt2" type="button" value="改变标题颜色" onclick="fn2()">
        <input id="bt3" type="button" value="删除最后一个" onclick="fn3()">
    </div>
</body>
<script>
    function fn1 (){
        document.getElementById('tb1').innerHTML="学员成绩表"
    }
    function fn2(){
        document.getElementById('tb1').style = "font-size: 30px;text-align: center;color:red;"
    }
    function fn3(){
        var trs = document.getElementsByClassName('data');
            trs[trs.length-1].remove();
    }
</script>
```

```js
// 1.获取Element对象
// 2.获取元素-根据ID获取
// [object HTMLImageElement]
var img =  document.getElementById('h1');
alert(img);

// 根据标签获取 - div
var divs =    document.getElementsByTagName('div');
for (let i = 0; i < divs.length; i++) {
    alert(divs[i]);

}

// 根据name属性获取
var ins=   document.getElementsByName('hobby');
for (let i = 0; i < ins.length; i++) {
    alert(ins[i]);

}

// 根据class属性获取
var divs =  document.getElementsByClassName('cls');
for (let i = 0; i < divs.length; i++) {
    alert(divs[i]);

}
```

DOM操作对元素内容进行更改

```js
   var divs = document.getElementsByClassName('cls');
   var  div1 = divs[0];
   div1.innerHTML = "河南科技大学开元校区"
```

DOM操作小案例

```js
<body>
    <img id="h1" src="../img/huawei.jpg" alt="华为" /><br /><br />
        <div class="cls">河南科技大学</div>
<br />
            <div class="cls">信息工程学院</div>
<br />
<input type="checkbox" name="hobby" />电影
<input type="checkbox" name="hobby" />旅游
<input type="checkbox" name="hobby" />游戏
</body>
<script>
    
// 更换logo
var img = document.getElementById('h1');
img.src = '../img/alibaba.jpg';

// 将所有的div标签的内容后面添加上：very good（红色字体）
var divs = document.getElementsByTagName('div');
for (let i = 0; i < divs.length; i++) {
    divs[i].innerHTML += '<font color = "red"> very good</font>';
}

// 使所有的复选框处于选中状态
var ins = document.getElementsByName('hobby');
for (let i = 0; i < ins.length; i++) {
    ins[i].checked = true;
}
</script>
```

## js事件监听

#### 事件绑定

方式一：通过HTML标签中的事件属性进行绑定

方式二：通过DOM元素属性绑定

```js
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>事件监听</title>
</head>
<body>
    <input type="button" value="按钮1" id="bt1" onclick="fn1()">
    <input type="button" value="按钮2" id="bt2">
</body>
<script>
    function fn1(){
        alert("按钮1被点击了");
    }
    document.getElementById('bt2').onclick = function(){
        alert("按钮2被点击了");
    }
</script>
```



#### 常见事件

onclick

onblur

onfocus

onload

onsubmit

onkeydown

onmouseover

onmouseout

#### 案例