### JS中一些关于字符串的知识

在JS中所有由单引号或者双引号包起来的都是字符串，每个字符串都是由零或多个字符组成

````javascript
var str="hlx";
str.length->字符串长度
str[0]-> 'h'
str [str.length-1]->'x'
str[100]->undefined


字符串中的每一个字符都有一个自己对应位置的索引，也有类似于数组一样的length代表自己的长度。

//=>循环遍历字符串，输出每一项
for (var i=o;i<str.length;i++){
    console.log(str[i]);
 }
`````
### 关于字符串中常用的方法

<!--more-->

字符串是基本的数据类型，字符串的每一次操作都是值直接进行操作，不像数组一样是基于空间地址来操作的，所以不存在原有字符串是否改变这一说，肯定都是不变的
**`charAt/charCodeAt`**
作用：charAt根据索引获取指定位置的字符，charCodeAt不仅仅获取字，它获取的是字符对应的Unicode编码值（ASCII码值）
参数：索引
返回：字符或者对应编码
***indexOf/lastindexOf****
基于这两个方法，可以获取字符在字符串中第一次或者最后一次出现位置的索引，不包含这个字符返回-1，所以可以基于这两个方法，验证当前字符串中是否包含某个字符

```
var str='hlxshibaba';
if(str.indexOf('@')>-1){
    //=>如果条件成立说明包含@符号
}
```
**`slice`**
作用：str.slice(n,m)从索引n开始找到索引为m处（不包含m），把找到的字符当作新字符串返回
**`substring`**
和slice语法一样，唯一区别在于slice支持负数索引，而substring不支持
**`substr`**
也是字符串的截取方法
语法：str.substr(n,m)，从索引n开始截取m个字符
**`toUpperCase/toLowerCase`**
实现字母的大小写转换，toUpperCase转换为大写，toLowerCase转换为小写
**`split`**
和数组中的join相对应，数组中的join是把数组中的每一项按照指定的连接符变为字符串，而split是把字符串按照指定的分割符，拆分成数组中的每一项
**`replace`**
作用：替换字符串中的原有字符
参数：原有的字符和要替换的新字符
返回：替换后的字符串

```javascrip
var str='hlxshibaba';
str=str.replace('hlx','何林虓')；
```
### 真实项目中的需求
`1.时间字符串的格式化`
>有一个时间字符串“2019-8-12 14:22:8”，我们想基于这个字符串获取到“08月12日 14时22分”
### URL地址问号传参解析
>有一个URL地址“http://www.hlxshibaba.com/stu/?lx=1&name=AA&sex=man”地址问号后面的类容是我们需要解析出来的参数信息
>{
>lx:1，
>name:'AA',
>sex:'man'
>}


### JS中的数学函数Math
Math称为数学函数，但他属于对象类型
```javascript
typeof Math =>"object"
```
之所以叫做数学函数，是因为Math这个对象中提供了很多数字的方法
#### Math中提供的常用方法
**`取绝对值`**：取绝对值
**`ceil/floor`**：向上（变大）或者向下（变小）取整
**`round`**:四舍五入
**`sqrt`**:开平方
**`pow`**:取幂（N的M次方）
**`max/min`**:获取最大值或者最小值
**`PI`**:获取圆周率
**`random`**:获取0-1之间的随机小数
`Math.round(Math.random()*(m-n)+n)`:获取n-m之间的随机整数

### 函数以及函数的返回值
函数在执行的时候，都会形成一个新的作用域（私有的栈内存），目的是：
1.把原有的堆内存中的字符串变为js表达 式执行
2.保护里面的私有变量不受外界的干扰（和外界隔离开）
我们把函数执行的这种保护机制称作‘闭包’
函数的入口：形参
函数的出口：返回值 return
（return返回的永远是一个值，并不是一个变量）
```javascript
function fn(n,m){
    var total=0;
    total=n+m;
    return total;
}
fn(1,2)//代表函数的执行，同时还代表函数执行后返回的值
//如果没有return，则函数执行的结果为undefined
fn(1)//n=1,m=undefined
//如果有一个参数没有则会返回NaN
```
##### arguments及任意数求和
任意数求和：不管传多少实参值进来，我们都可以求和
形参有局限性：我们需要知道用户执行的时候传递实参数量，顺序等，才可以使用形参变量定义对应的入口
arguments：函数内置的实参集合（内置：天生就存在的机制，不管你是否设置了形参，是否传递了实参，arguments都有）它是一个类数组，不是数组，不可以直接使用数组中的方法，ARG存储的是传递进来的所有实参，所以被称作‘实参集合’
### 实名函数和匿名函数
实名函数：有函数名
匿名函数：没有函数名
    -函数表达式：把函数当作值赋给变量或者元素的事件
    -自执行函数：创建和执行一起完成的
//=>函数表达式
```javascript
var fn=function(){
};
oBox.onclick=function(){
};
```
//=>自执行函数
```javascript
(function(i){
})(10);     //i：是形参 10：是实参
~function(){
}();
!function(){
}();
+function(){
}();
```
### DOM树
>dom树
>        当浏览器加载HTML页面的时候，首先就是dom结构的计算，计算出来的dom结构就是dom树（把页面中的HTML标签像树结构一样分析出之间的层级关系）。
>        dom树描述了标签和标签之间的关系（节点间的关系），我们只要知道任何一个标签，都可以依据DOM中提供的属性和方法，获取到页面中任意一个标签或者节点。
#### 在JS中获取DOM元素的方法
**`getElementById`**
>通过元素的ID获取指定的元素对象，使用的时候都是document.getElementById('')
>此处的document时限定了获取元素的范围，我们把它称为‘上下文（context）’
>1.getElementById的上下文只能是document
>2.如果页面中的ID重复了，我们基于这个方法只能获取到第一个元素，后面相同的ID无法获取
>3.在IE6-7中，会把表单元素（input...）的name属性值当作Id来使用(建议：不要让name和ID的属性值有冲突)


**`getElementByTagName`**
>'[context].getElementByTagName()'在指定的上下文中，根据标签名获取到一组元素集合（HTMLCollection）
>1.获取的元素集合是一个**类数组**，不能直接使用数组的方法，就算只有一个也需要[0]来使用
>2.他会把当前上下文中，子孙的层级标签都获取到
>3.基于这个方法获取到的结果永远是一个集合，如果像操作集合中具体的某一项，需要基于索引获取到才可以


**`getElementByClassName`**
>'[context].getElementByClassName()'在指定的上下文中，基于元素的样式类名（class=‘XXX’）获取到一定的元素集合
>1.在真实项目中，我们经常是基于样式类来给元素设置样式，所以在JS中，我们也常会经常基于样式类来获取元素，但是此方法在IE6-8不兼容


**`getElementByName`**
>'doucument.getElementByName()'它的上下文也只能是document，在整个文档中，基于元素的name属性值获取一组节点集合（也是一个类数组）
>1.在IE浏览器中，只对表单元素的name属性起作用（正常来说：我们的项目中只会给表单元素设置name，给非表单元素设置name是一个不太符合规范的操作）

**`querySelector`**
>'[context].querySelector()'在指定的上下文中基于选择器（类似于CSS选择器）获取指定的元素对象（获取的是一个元素，哪怕匹配了多个，也只获取第一个）

**`querySelectorAll`**
>'[context].querySelectorAll()'我们获取到选择器匹配到的所有元素，结果是一个节点集合
>1.querySelector/querySelectorAll都是不兼容IE6-8浏览器的（不考虑兼容的情况下，我们能用其他方式获取，就用其他方式，尽量不要使用这个方法，此方法性能消耗太大）

**`docuemnt.head`**
>获取HEAD元素对象

**`document.body`**
>获取BODY元素对象

**`document.documentElement`**
>获取HTML元素对象

```javascript
//=>获取浏览器一屏幕的宽度和高度（兼容所有浏览器）
document.documentElement.clientWidth||document.body.clientWidth
document.documentElement.clientHeight||document.body.clientHeight
```

### 节点（node）
>在一个HTML文档中出现的所有东西都是节点
>-元素节点（HTML标签）
>-文本节点（文字内容）
>-注释节点（注释内容）
>-文档节点（document）
>-....

每一种类型的节点都会有一些属性区分自己的特征和特性
-nodeType：节点类型
-nodeName:节点名称
-nodeValue：节点值
`元素节点`
nodeType：1
nodeName：大写标签名
nodeValue：null
`文本节点`
nodeType：3
nodeName：‘#text’
nodeValue：文本内容
`注释节点`
nodeType：8
nodeName：‘#common’
nodeValue：注释内容
`文档节点`
nodeType：9
nodeName：‘#document’
nodeValue：null

### 描述节点之间关系的属性
**`parentNode`**
>获取当前节点唯一的父亲节点

**`childNodes`**
>获取当前元素的所有子节点
>-子节点：只获取儿子级别的
>-所有：包含元素节点，文本节点等

**`children`**
>获取当前元素所有的元素子节点
>
>在IE6-8中会把注释节点也当作元素节点获取到，所以兼容性不好

**`previousSibling`**
>获取当前节点的上一个哥哥节点（获取的可能是元素也可能是文本等）
>
>previousElementSibling:获取上一个哥哥元素节点（不兼容IE6-8）
>

**`nextSibling`**
>获取当前节点的下一个弟弟节点
>
>nextElementSibling:下一个弟弟元素节点

**`firstChild`**
>获取当前元素的第一个子节点（可能是元素或者文本）
>
>firstElementChild

**`lastChild`**
>获取当前元素的最后一个子节点（可能是元素或者文本）
>
>lastElementChild

---------------------------------------------
需求一：获取当前元素的所有元素子节点
>基于children不兼容IE低版本浏览器（会把注释当作元素节点）

需求二：获取当前元素的上一个哥哥元素节点
>previousSibling:上一个哥哥节点
>previousElementSibling：上一个哥哥元素节点（但是不兼容）


### 关于DOM的增删改
**`creatElement`**
>创建一个元素标签（元素对象）
>‘document.createElement([‘标签名’])’

**`appendChild`**
>把一个对象插入到指定容器的末尾
>‘[container].appendChild({newELe})’


**`insertBefore`**
>把一个元素对象插入到指定容器中的某一个标签之前
>‘[container].insertBefore([newEle],[oldEle])’

**`cloneNode`**
>把某一个节点进行克隆
>‘[curEle].cloneNode()’:浅克隆，只克隆当前标签
>‘[curEle].cloneNode(true)’：深克隆，当前标签以及内容

**`removeChild`**
>在指定容器当中删除某一个元素
>'[contaimer].removeChild([curEle])'

**`set/get/removeAttribute`**
>设置/获取/删除 当前元素的某一个自定义属性
>box.setAttribute('mycolor','red'); //=>设置
>box.getAttribute('mycolor');  //=>获取
>box.removeAttribute('mycolor')  //=>删除

两种修改方式
>第一种是基于对象键值对操做方式，修改当前元素对象的堆内存空间来完成
>第二种是直接修改页面中HTML标签的结构来完成（此种办法设置的自定义属性可以在结构上呈现出来）
>基于setAttribute设置的自定义属性值都是字符串

需求：解析一个URL字符串问号传参和HASH值部分




###  NODE基础概念
1.node并不是一门语言，它是一个工具或者环境，渲染和解析JS
2.在node环境中把JS代码执行
    -REPL命令（read-evaluate-print-loop：输入-求值-输出-循环）
    -基于node xxx.js命令执行
    -基于WB这类编辑工具直接执行
    

### NPM模块管理
安装完成NODE后，基本自带npm模块管理器
我们需要一个第三方模块，插件，类库，框架等，需要提前下载安装才可以使用
- 百度搜索，找到下载地址，然后下载（资源混乱，不好搜索，广告多）
- 也可以基于NPM等第三方包管理器下载（yarn/bower...都是第三方模块管理器）

1.npm下载的资源都是在https://www.npmjs.com/中下载的
`npm install XXX`:把资源或者第三方模块下载到当前目录下
`npm install XXX -g(--global)`:把资源或者第三方模块安装到全局环境下（目的：以后可以基于命令来操作一些事情）

2.解决下载慢的问题
**`基于nrm切换到国内下载器（一般是淘宝镜像）`**
首先安装nrm，而且把他安装到全局环境下
>npm install nrm -g
>安装完成后，我们可以使用nrm命令
>- nrm ls 查看当前可用源（带星号是当前使用源）
>-nrm use XXX 使用某个源
>**`基于yarn来安装管理`**
>首先安装yarn，安装到全局，然后基于yarn安装我们需要的模块
>npm install yarn -g
>基于yarn安装只能安装到本地，不能安装到全局
>yarn add XXX
>yarn remove xxx
>**`基于cnpm淘宝镜像来处理`**

3.解决安装版本的问题
>首先查看当前模块的历史版本信息
>npm view jquery >
>`jquery.version.json`：把当前模块的历史信息输出到具体的某个文件中（文件名自己随便取
>
>安装指定的版本
>`yarn add jquery@1.11.3` ：yarn和npm都是这样指定安装版本的

### github
>一个提供代码管理的公共平台，上面有各种的组件/类库/插件/框架/供人使用研究
>在github中我们可以创建仓库来管理自己的项目文件，而github支持开发者通过git操作，把本地的项目推送到指定的仓库中，他还提供静态web页面的发布

>git是一个分布式代码版本管理控制系统
>- 记录当前产品代码的所有版本信息（历史修改信息），而且方便回退到某一个具体的版本
>- 方便团队协作开发，能够检测代码冲突，合并代码等

#### git工作原理
当我们在本地创建一个git仓库后，我们可以基于这个仓库管理我们的代码
**`git的工作流程`**
>每个git仓库都分为三个区域
>- 工作区：编辑代码的地方
>- 暂存区：临时存储要生成版本代码的地方
>- 历史区：储存的是生成的每一个版本的代码

**`从工作区到暂存区`**
>`$ git status`
>查看代码或者文件的状态（当前处于哪个区域）：红色（当前处于工作区，还未提交到暂存区），绿色（当前处于暂存区，还未提交到历史区），如果没有文件，代表三个区域代码已经同步，历史版本也在历史区生成了
>`$git add . /$ git add -A`
>把当前工作区中所有最新修改的文件，都提交到暂存区

**`暂存区到历史区`**
>`$git commit`
>这样执行后，会弹出一个提交文本的输入界面，需要我们编写本次提交的当前版本的备注信息
>先按i进入插入模式
>输入备注信息
>按esc
>输入“:wq”保存退出
>`git commit -m '自己需要编写的东西'`
>一次性解决，不需要进入输入界面

`$git log`
>查看版本信息，提交记录

`$git diff`
>工作区和暂存区比较

`$git diff master`
>工作区和历史区比较

`$git diff --cached`
>暂存区和历史区比较


### git和GitHub同步
1.让本地的git仓库和远程仓库建立关联
`$git remote -v`
查看所有的关联信息
`$git remote add xxx(名字) [远程仓库git地址]`
建立关联
`$git remote remove xxx(名字) [远程仓库git地址]`
移除关联

我们远程仓库关联在一起的名字默认是origin，也可以自己修改
2.把本地的信息推送到远程的仓库上，或者从远程仓库上拉取信息到本地仓库(就是信息的同步)
在推送之前，我们都应该先拉取
`$git pull origin(自己设置的名字) master`
从远程仓库的master分支拉取最新的信息
`$git push origin master`
把本地的信息推送到远程仓库的master分支下
如果名字是origin，分支走的也是master，后面的可以不写直接执行`$git pull/git push`

`git clone (远程仓库地址) (本地仓库名字)`
直接将远程仓库复制到本地

在github上面仓库的settings>collaborators处可以设置将你的仓库共享给某人

### 变量提升机制
>**`变量提升`**
>当栈内存（作用域）形成，js代码自上而下执行之前，浏览器首先会把所有带‘var/function’关键词的进行提前‘声明’或者‘定义’
>=>声明（declare）：var a （默认值是undefined）
>=>定义（defined）：a =12 （定义其实就是赋值操作）
>【变量提升阶段】
>=>带‘var’的只声明未定义
>=>带‘function’的声明和赋值都完成了
>
>变量提升只发生在当前作用域（列如：开始加载页面的时候只对全局作用域下的进行提升，因为此时函数中存储的都是字符串而已）
>在全局作用域下声明的函数或者变量是‘全局变量’，同理，在私有作用域下声明的变量是‘私有变量’【带var/function的才是声明】
>在私有作用域中先进行形参赋值然后就会变量提升

#### 只对等号左边进行变量提升

```javascript
/*
	变量提升：
		var fn； =>只对等号左边进行变量提升
		sum = AAAFFF111;
*/
fn(); //报错：Uncaught TypeError:fn is not a function
sum();//=>2
//匿名函数之函数表达式
var fn=function(){
    console.log(1);
};//代码执行到此处会把值赋给fn
fn(); //=> 1
//普通函数
function sum(){
    console.log(2);
}
```

#### 重名问题的处理

```javascript
/*
	1.带var和function关键字声明相同的名字也算是重名（其实是一个fn，只是存储值的类型不一样）
*/
var fn=12;
function fn(){
    
}
```

```javascript
/*
	2.关于重名问题的处理：如果名字重复了，不会重新的声明，但是会重新定义（重新赋值）[不管是变量提升还是代码执行阶段都是如此]
	变量提升：
	fn = ...(1)
	   = ...(2)
	   =只处理等号左边，没有赋值
	   = ...(3)
	   = ...(4)
*/
fn();	 //=>4
function fn(){console.log(1);}
fn();	//=>4
function fn(){console.log(2);}
fn();	//=>4
var fn=100;
fn() //=>报错Uncaught TypeError:fn is not a function
function fn(){console.log(3);}
fn()
function fn(){console.log(4);}
fn()
```



#### 带var和不带的区别

>在全局作用域下声明一个变量，也相当于给WINDOW全局对象设置了一个属性，变量的值就是属性值（私有作用域中声明的私有变量和WINDOW没啥关系）

带var的
```JavaScript
console.log(a); //=>undefined
console.log(window.a); //=>undefined
console.log('a' in window); //=>true 在变量提升阶段，全局作用域中声明了一个变量a，此时就已经把a当作属性值赋给window了，只不过此时还未给a赋值，默认值为undefined 
var a=12; //=>全局变量值修改，window的属性值也修改
console.log(a) //=>12 全局变量
console.log(window.a) //=>12 window的属性值
a =13；
console.log(window.a) //=>13;
window.a=14
console.log(a); //=>14
//全局变量和window中的属性存在映射关系
```
不带var，本质是window下的一个属性
```javascript
//console.log(a); //=>报错a is not undefined
console.log(window.a); //=>undefined
console.log('a' in window); //=>false
a=12;
console.log(a); //=>12
console.log(window.a); //=>12
```

练习题

```javascript
console.log(a,b); //=>undefined undefined
var a=12;
var b=12;
 function fn(){
     console.log(a,b); //=>undefined 12
     var a=b=13;  //这里的b是全局作用域下的b
     console.log(a,b); //=>13 13
 }
fn();
console.log(a,b) //=>12 13
```

### ES6中let创建的变量不存在变量提升

在es6中基于let/Const等方式创建变量或者函数，不存在变量提升机制

切断了全局变量和WINDOW属性的映射机制

```javascript
console.log(a); //报错：a is not undefined
let a=12;
console.log(window.a); //undefined
console.log(a);//12
```

在相同的作用域中，基于let不能声明相同名字的变量（不管用什么方式在当前作用于下声明了变量，再次使用let创建都会报错）

```javascript
var a=12;
let a=13; //=>报错：Identifier 'a' has already been declared
```

虽然没有了变量提升机制，但是在当前作用域代码自上而下执行之前，浏览器会做一个重复性检测（语法检测）：自上而下查找当前作用于下所有变量，一旦发现有重复的，直接抛出异常，代码也不会在执行了（虽然没有把变量提前声明定义，但是浏览器已经记住了，当前作用域下有哪些变量）

```javascript
var a=12;
console.log(a); //不会输出，直接报错
let a=13;
```

### 暂时性死区

在代码块内，使用let命令声明变量之前，该变量是不可用的,称为“暂时性死区”（temporal dead zone，简称 TDZ）

```javascript
if (true) {
  // TDZ开始
  tmp = 'abc'; // ReferenceError
  console.log(tmp); // ReferenceError
  let tmp; // TDZ结束
  console.log(tmp); // undefined
  tmp = 123;
  console.log(tmp); // 123
}
```

所以typeof不在是一个安全的操作了

```javascript
typeof x;//ReferenceError
let x;
```

#### 关于私有作用变量的一点练习

```javascript
var a = 12,
    b = 13,
    c = 14;
function fn(a) {
    console.log(a, b, c);// 12 undefined 14 (a是传递的参数，c是全局的)
    var b = c = a = 20; //（b是私有的）
    console.log(a, b, c); //20 20 20
}
fn(a);
console.log(a, b, c); //12 13 20  
```

```javascript
var ary=[12,23];
function fn(ary){
    console.log(ary); //=>12,23
    ary[0]=100;
    ary=[100];
    ary[0]=0;
    console.log(ary);//=>0
}
fn(ary);
console.log(ary); //=>100,23
```

### JS中的堆内存和栈内存

堆内存：存储引用数据类型值（对象：键值对，函数：代码字符串）

栈内存：提供JS代码执行的环境和存储基本类型值

[堆内存释放]：让所有引用堆内存空间地址的变量赋值为null即可（没有变量占用这个堆内存了，浏览器会在空闲的时候把他释放掉）

[栈内存释放]：一般情况下，当函数执行完毕，所形成的私有作用域（栈内存）都会自动释放掉（在栈内存中存储的值也会释放掉），但是也有特殊不被销毁的情况：

​	1.函数执行完成，当前形成的占内存中，某些内容被栈内存以外的变量占用了，此时栈内存不能释放（一旦释放，外面找不到原有的内容了）

​	2.全局栈内存只有在页面关闭的时候才会被释放掉

​	.........

​	如果当前栈内存没有被释放掉，那么之前在栈内存中存储的基本值也不会被释放，能够一直保存下来



### 闭包作用

函数执行形成一个私有作用域，保护里面的私有变量不受外界干扰

目前开发者认为的闭包是：形成一个不销毁的私有作用域（私有栈内存）才是闭包

```javascript
//闭包：柯理化函数
function fn(){
    return function(){
        
    }
}
var f=fn();
//闭包：惰性函数
var utils=(function(){
    return {
        
    }
})();
```

真实项目中为了保证JS的性能（堆栈内存的性能优化），应该尽可能的减少闭包的使用（不销毁的对栈内存是耗性能的）

1.闭包具有保护作用：保护私有变量不受外界干扰

2.闭包具有保护作用：形成不销毁的栈内存，把一些值保存下来，方便后面的调取使用

所有的事件绑定都是异步编程（同步编程：一件事一件事的做，当前这件事没完成，下一个任务不能处理/异步编程：当前这件事没有彻底完成，不再等待，继续执行下面的任务）

## 面向对象编程（Object Oriented Programming）

### 单例设计模式（Singleton Pattern）

1.表现形式：

```javascript
var obj={
    xxx:xxx;
    ....
};
```

在单例设计模型中，Obj不仅是对象名，他被称为“命名空间[NameSpace]”,把描述事物的属性存放到命名空间中，多个命名空间是独立分开的，互不冲突

2.作用

把描述同一件事物的属性和特征进行“分组，归类”（存储在同一个堆内存空间中），因此避免了全局变量之间的冲突和污染

3.单例设计模式命名的由来

每一个命名空间都是JS中Object这个内置基类的实例，而实例之间是相互独立互不干扰的，所以我们称他为“单例：单独的实例”

```javascript
//高级的单例模式
/*
 *1.在给命名空间赋值的时候，不是直接赋值一个对象，而是先执行匿名函数，形成一个私有作用域AA（不销毁的栈内存），在AA中创建一个堆内存，把堆内存地址赋值给命名空间
 *2.这种模式的好处：我们完全可以在AA中创造很多内容（变量or函数），哪些需要供外面调取使用的，我们暴露到返回的对象中（模块化实现的一种思想）
*/
varnameSpace=(function(){
    functon fn(){
        
    }
    function sum(){
        
    } 
    return {
        fn:fn
    	sum:sum
    }
})();
```

测试：

```javascript
var n=2;
var obj={
    n:3,
    fn:(functong(n){
        n*=2;
        this.n+=2
        var n=5;
        return function(m){
    			this.n*=2
    			console.log(m+(++n));
			}
        })(n)
}
var fn=obj.fn;
fn(3);
obj.fn(3);
console.log(n,obj.n);
```

### 工厂模式(Factory Pattern)

定义一个创建对象的接口，让其子类自己决定实例化哪一个工厂类，工厂模式使其创建过程延迟到子类进行

1.把实现相同功能的代码进行“封装”，以此来实现“批量生产”（后期想要实现这个功能，我们只需要执行函数即可）

2.“低耦合高内聚”：减少页面中的冗余代码，提高代码的重复使用率*

### 面向对象

[面向对象]：JS/JAVA/PHP/C#/Ruby/python/c++...

[面向过程]：C

面向对象编程，需要我们掌握：“对象，类，实例”的概念

​	对象：万物皆对象

​	类：对象的具体细分（按照功能特点进行分类）

​	实例：类中的具体的一个事物（拿出类别中的具体一个实例进行研究，那么当前类别下的其他实例也具备这些特点和特征）

整个js就是基于面向对象开发和设计出来的语言，我们学习和实战的时候也要按照面向对象的思想去体会和理解

### 构造函数

##### 基于构造函数创建自定义类（constructor）

1.在普通函数执行的基础上“new xxx（）”，这样就不是普通函数执行了，而是构造函数执行，当前的函数名称之为"类名",接收的返回结果是当前类的一个实例

2.自己创建的类名首单词首字母尽量大写

3.构造函数设计模式执行，主要用于组件，类库插件，框架等的封装，平时编写业务逻辑时一般不会这样处理

```javascript
function Fn(){
    
}
var f=new Fn();//此时f就是当前fn的实例
var f2=new Fn();//此时f2也是Fn的一个实例，互不影响

var obj1={}; //obj1是object的一个实例
var obj2={}; //obj2是object的一个实例
```

JS中创建值有两种方式

​	1.字面量表达式

​	2.构造函数模式

```javascript
var obj={}; //=>字面量方式
var obj=new Object(); //=>构造函数模式
//不管是哪一种方式创造出来的都是Object类的实例，而实例之间是独立分开的，所以var xxx={} 这种模式就是JS中的单例模式
```

基本数据类型基于两种不同的模式创建出来的值是不一样的

基于字面量方式创建出来的值是基本类型值

基于构造函数创建出来的值是引用类型

```javascript
var num1=12;
var num2=new Number(12);
console.log(typeof num1);//   	'number'
console.log(typeof num2);//		'Object'
//num2是数字类的实例，num1也是数字类的实例，他只是js表达数字的方式之一，都可以使用数字类提供的属性和方法
```

```javascript
function Fn(name,age){
    var n=10;//n只是私有作用域的一个私有变量，不会在创建的实例中出现
    this.name=name;
    this.age=age+n;
}
Fn();//普通函数执行：1.形成一个私有作用域2.形参赋值3.变量提升4.代码执行5.栈内存释放或者保留
var f=new Fn('hlx',20);
/*构造函数执行：1.像普通函数执行一样，形成一个私有作用域（栈内存），形参赋值 和 变量提升（私有变量）
2.[构造函数独有]在Js代码自上而下执行之前，首先在当前形成的私有栈中创建一个对象（创建一个堆内存：暂时不存储任何东西），并且让函数中的执行主体（this）指向这个新的堆内存（this===创建的对象）
3.代码自上而下执行
4.[构造函数独有]代码执行完成，把之前创建的堆内存地址返回（浏览器默认返回）
*/
//开始创建的对象就是Fn这个类的一个实例，最后浏览器会将这个对象返回，供外面接收
```

```javascript
/*构造函数执行，不写return，浏览器会默认返回创建的实例，但是如果我们自己写了return：
	1.return写的如果是一个基本值，返回的结果依然是类的实例，没有受到影响
	2.如果返回的是引用值，则会把默认返回的实例覆盖，此时接收到的结果就不再是当前类的实例了
*/
function Fn(){
    var n=10;
    this.m=n;
    return 'haha';
}
var f=new Fn();
console.log(f); //还是一个实例
function Fn(){
    var n=10;
    this.m=n;
    return {name：'haha'};
}
var f=new Fn();
console.log(f); //{name :haha}
```

### 原型链设计模式

原型（prototyoe），原型链（\_proto\_）

引用类型：

[函数]：普通函数，类（所有的类：内置类，自己创建的类）

[对象]：普通的对象，数组，正则，Math，Date，实例是对象类型的（除了基本字面量创建的值），prototype的值也是对象类型的，函数也是对象类型的

1.所有的函数数据类型都天生带一个属性：prototype（原型），这个属性的值是一个对象，浏览器会默认给他开辟一个堆内存

2.在浏览器给prototype开辟的堆内存中有一个天生自带的属性：constructor，这个属性存储的值是当前函数本身（实例对象没有constructor属性，实例中读取的是原型链上的xxx.prototype.constructor）

3.每一个对象都有一个\_proto\_的属性，这个属性指向当前实例所属类的prototype（如果不能确定它是谁的实例，都是Object的实例）

原型链：它是一种基于\_\_proto\_\_向上查找的机制，当我们操作实例的某个属性和方法的时候，首先找自己空间中私有的属性或者方法1.找到了则结束查找。2.没找到，则基于\_\_proto\_\_找到所属类的prototype，如果找到则使用共有的，如果没找到，则基于原型上的\_\_proto\_\_继续向上查找，一直找到Object.prototype的原型为止，如果还没有，则操作的属性或者方法不存在!



#### 练习题

```javascript
**1**
console.log(a); 
var a=12; 
function fn(){
    console.log(a); 
    var a=13;   
}
fn();   
console.log(a);
/*
 A、undefined  12 13             
 B、undefined undefined 12 //=>right  
 C、undefined undefined 13         
 D、有程序报错
 */


**2**
console.log(a); 
var a=12;
function fn(){
    console.log(a);
    a=13;
}
fn();
console.log(a);
/*
 1 A、undefined  12 13     //=>right        
 B、undefined undefined 12   
 C、undefined undefined 13         
 D、有程序报错
*/


**3**
console.log(a);
a=12;
function fn(){
    console.log(a);
    a=13;   
}
fn();
console.log(a);
/*
 A、undefined  12 13             
 B、undefined undefined 12   
 C、undefined undefined 13         
 D、有程序报错 			//=>right 第一行报错
*/


**4**
var foo=1; 
function bar(){
    if(!foo){ //！undefined =>true
        var foo=10; 
    }
    console.log(foo); 
}
bar();
/*
 A、1     
 B、10     //=>right
 C、undefined                   
 D、报错
*/


**5**
var n=0; 
function a(){
    var n=10; 
    function b(){
        n++; 
        console.log(n); 
    }
    b();
    return b; 
}
var c=a();
c(); 
console.log(n);
/*
A、1 1 1   
B、11 11 0  
C、11 12 0  //=> right
D、11 12 12
*/


**6**
var a=10,b=11,c=12;
function test(a){
     a=1;
     var b=2;
     c=3;
}
test(10);
console.log(a);  
console.log(b);   
console.log(c);

/*
A、1 11 3   
B、10 11 12  
C、1 2 3   
D、10 11 3		//right
*/


**7**
if(!("a" in window)){
   var a=1;
}
console.log(a);
/*
A、1   
B、undefined   	//right
C、报错   
D、以上答案都不对
*/
    

**8**
var a=4;
function b(x,y,a) {    
     console.log(a); 
    //arguments:函数内置的实参集合，不管是否设置形参，传递的实参值在这个集合中都存在
    /*arguments
      {
      	0:1
      	1:2
      	2:3
      	length:3
      	callee；函数本身
      	....
      }
       js的非严格模式下，函数中的形参变量和arguments存在映射机制（相互影响）
       arguments[2]=10;改变之后形参也会改变
     */
     arguments[2]=10;        
     console.log(a); 
}
a=b(1,2,3);   //=>a=b的执行结果 =>a=undefined[b函数中没有设置return，所以默认函数返回值为undefined]
console.log(a); 
/*
A、3  3  4   
B、3  10  4   
C、3  10  10   
D、3  10  undefined   //right
*/


**9**
var foo='hello'; 
(function(foo){
   console.log(foo);
   var foo=foo||'world';
   console.log(foo);
})(foo);//把foo的值当作实参传给函数的形参
console.log(foo);

/*
 A、hello hello hello   //=>right
 B、undefined world  hello   
 C、hello world world   
 D、以上答案都不正确
*/
/*逻辑与&& 和 逻辑或||
  1.在赋值操作中，我们有时候也会用他们
  var a=1||2;//=>首先验证1的真假，如果为真，则把1赋值给a，如果为假则把2赋值给a。
  var x=a||b;//=>只判断a的真假，若为真，则x=a，若为假，则x=b
  
  var b=1&&2;//=>首先判断1的真假，若为真，则b=2，若为假，则b=1
  2.当逻辑与和逻辑或混合在一起时，逻辑与的优先级高于逻辑或
*/

**10**
var a=9; 
function fn(){ 
    a=0;       
    return function(b){ 
       return b+a++; 
    }    
}
var f=fn();
console.log(f(5));
console.log(fn()(5));
console.log(f(5));
console.log(a);
/*
 A、6 6 7 2   
 B、5 6 7 3   
 C、5 5 6 3   
 D、以上答案都不正确  //=>right  5 5 6 2
*/


**11**
var ary=[1,2,3,4];
function fn(ary){
    ary[0]=0;    //在没有给私有的ary重新指向新的地址之前，所操作的数组都是全局的数组
    ary=[0];	//将私有的ary指向新的地址
    ary[0]=100;    
    return ary; 
}
var res=fn(ary);   	//将全局下的ary地址传给了函数
console.log(ary);    //[0,2,3,4]
console.log(res);	 //[100]


**12**
function fn(i) {
    return function (n) {
        console.log(n + (i++));
    }
}
var f = fn(10);
f(20);   		//30
fn(20)(40);		//60
fn(30)(50);		//80
f(30);			//41


**13**
var i = 10;
function fn() {
    return function (n) {
        console.log(n + (++i));
    }
}
var f = fn();
f(20);  	//31
fn()(20);	//32
fn()(30);	//43
f(30);		//44


**14**
var num = 10;
var obj = {num: 20};
//obj.fn此时是自执行函数的返回值
obj.fn = (function (num) {
    this.num = num * 3;		//在非严格模式下，自执行函数的this没有主体，this此时是window
    num++;		
    return function (n) {
        this.num += n;
        num++;
        console.log(num);
    }
})(obj.num);
var fn = obj.fn;
fn(5);  // 22
obj.fn(10);	//23
console.log(num, obj.num); //65 30


**15**
function Fn() {
    this.x = 100;
	this.y = 200;
    this.getX = function () {
    	console.log(this.x);
    }
}
Fn.prototype.getX = function () {
    console.log(this.x);
};
Fn.prototype.getY = function () {
    console.log(this.y);
};
var f1 = new Fn;
var f2 = new Fn;
console.log(f1.getX === f2.getX);	//false
console.log(f1.getY === f2.getY);	//true，f1中找不到会通过__proto__向上找
console.log(f1.__proto__.getY === Fn.prototype.getY);	//true
console.log(f1.__proto__.getX === f2.getX);				//false
console.log(f1.getX === Fn.prototype.getX);				//false
console.log(f1.constructor);							//fn
console.log(Fn.prototype.__proto__.constructor);		//object
f1.getX();												//100
f1.__proto__.getX();									//undefined
f2.getY();												//200
Fn.prototype.getY();									//undefined


**16**
    1、以下代码的功能是要实现为5个input按钮循环绑定click点击事件，绑定完成后点击1、2、3、4、5五个按钮分别会alert输出0、1、2、3、4五个字符。（腾讯）

请问如下代码是否能实现？//不能
如果不能实现那么现在的效果是什么样的？//随便点击哪一个都是输出5
应该做怎样的修改才能达到我们想要的效果，并说明原理？/*因为事件绑定是异步编程，当点击触发的时候循环早已经结束，方法执行产生的私有作用域，用到变量i，不会有私有的变量，按照“作用域链”的查找机制，找到的是全局作用域下的i（此时的i是执行完成后的i=5），可以运用
1.自定义属性
2.闭包
for(var i=0;i<l;i++){
	inputs[i].onclick=(function(i){
		return function(){
			alert(i);
		}
	})(i);
}
3.ES6
使用let创建变量会形成块级作用域
for(let i=0;i<l;i++){
	inputs[i].onclick=function(){
		alert(i);
	}
}
*/
<div id="btnBox">
    <input type="button" value="button_1" />
    <input type="button" value="button_2" />
    <input type="button" value="button_3" />
    <input type="button" value="button_4" />
    <input type="button" value="button_5" />
</div>
<script type="text/javascript">
    var btnBox=document.getElementById('btnBox'),
        inputs=btnBox.getElementsByTagName('input');
    var l=inputs.length;
    for(var i=0;i<l;i++){
        inputs[i].onclick=function(){
            alert(i);
        }
    }
</script>



**17**
/*1.元素绑定事件，方法中的this是当前操作的元素
  2.方法名前面是否有点，点前面是谁this就是谁，若没有this就是window（严格模式下是undefined）
  3.构造函数执行，方法体中的this是当前类的一个实例
  	
*/
var fullName='language';
var obj={
    fullName='javascript',
    prop:{
        getFullName:function(){
            return this.fullName;
        }
    }
};
console.log(obj.prop.getFullName());	//=>this:obj.prop => this.fullname=obj.prop.fullname => undefined
var test=obj.prop.getFullName;			
console.log(test());	//window.fullname =>language
var name='window';
var Tom={
    name:"Tom",
    show:function(){
        console.log(this.name);
    },
    wait:function(){
        var fun=this.show;//  this.show=>tom.show
        fun();//this: window  =>  window.name
    }
};
Tom.wait(); 	//window


**18**
function Foo() {
    getName = function () {
        console.log(1);
    };
	return this;
}
Foo.getName = function () {
    console.log(2);
};
Foo.prototype.getName = function () {
    console.log(3);
};
var getName = function () {
    console.log(4);
};
function getName() {
    console.log(5);
}
Foo.getName(); 
getName();
Foo().getName();
getName(); 
new Foo.getName();
new Foo().getName();
new new Foo().getName();


**19**
function fun(){
    this.a=0;
    this.b=function(){
        alert(this.a);
    }
}
fun.prototype={
    b:function(){
    	 this.a=20;
        alert(this.a);
    },
    c:function(){
        this.a=30;
        alert(this.a)
    }
}
var my_fun=new fun();
my_fun.b();				//0
my_fun.c();				//30


**20**
//如何实现数组去重？
function unique(ary){
    var obj={};
    //[12,13,12,12,45,56,13,56]依次遍历数组中的每一项，让每一项的值作为对象的属性名和属性值（属性值存什么都可以），每一次存储之前验证当前对象中是否已经存在该属性了（in/hasOwnProperty/属性值不是undefined...）,如果有这个属性了说明当前项在数组中已经存在了，我们把当前项在原有数组中移除即可，若不存在则存储到对象中
    for(var i=0;i<ary.length;i++){
        var item=ary[i];
        if(obj.hasOwnProperty(item)){
            //obj中有这个属性
            /*方案一
            ary.splice(i,1);
            i--;
            continue;
            */
            /*优化一：
            不使用splice删除数组（如果后面有很多项，每一项会向前移动，比较消耗性能）
              解决：用最后一项替换当前项，然后删除最后一项(会改变原有数组顺序)
              ary[i]=ary[ary.lenngth-1];
              ary.pop();
              i--;
              continue;
            */
            
        }
        obj[item]=item;
    }
    obj=null;//优化二：obj没用了，我们手动将他释放掉，节约内存
    return ary;
}


```

### 函数的三种角色

1.普通的函数

​	->堆栈内存的释放

​	->作用域链

2.类

​	->prototype：原型

​	->__proto\_\_：原型链

​	->实例

3.普通对象

​	->和普通的一个OBJ没啥区别，就是对键值对的增删查改

```javascript
function Fn(){
    var n=10;
    this.m=100;
}
Fn.prototype.aa=function (){
  console.log('aa');  
};
Fn.bb=function (){
  console.log('bb');  
}; 
//普通函数
Fn(); //=>this ：window 有一个私有变量n和原型以及属性bb没有关系

//=>构造函数执行
var f= new Fn(); //=>this:f
console.log(f.n);//=>undefined  n是私有变量和实例没有关系
console.log(f.m);//=> 100 实例的私有属性
f.aa();//=>实例通过__proto__找到Fn.prototype上的方法
console.log(f.bb);//=> undefined ：bb是把Fn当作普通的对象设置的属性，和实例没有关系

//=>普通对象
Fn.bb();

```

```javascript
/*1*/function Foo() {
    getName = function () {
        console.log(1);
    };
    return this;
}
/*2*/Foo.getName = function BBB() {
    console.log(2);
};
/*3*/Foo.prototype.getName = function AAA() {
    console.log(3);
};
/*4*/var getName = function () {
    console.log(4);
};
/*5*/function getName() {
    console.log(5);
}
foo.gatName();       //=>2  把Foo当作一个对象，找Foo的私有方法执行
getName();			//=>4  变量提升阶段会将getName()输出的值设置为5（第5步），但是当代码从上到下执行的时候，第4步会将getName的重新定义，所以当后面调用的时候getName()输出4
foo().getName();  	//先把Foo当作普通函数执行，执行的返回结果再调用getName执行。Foo当作函数执行，由于Foo中没有变量提升和形参赋值，所以其中的getName属性，就是全局作用域下的getName，将其赋予新的值，即输出1.然后返回this，此时的this就是window，然后调用window.getName(),输出1.
getName(); 		//此时再调用全局下的getName输出1
new Foo.getName();	//A:(Foo.getName) =>new A() =>2
new Foo().getName();	//B:(new Foo())=>B.getName()  =>3
new new Foo().getName();	//c:(new Foo())=>new c[Foo的实例].getName()=>D:(c.getName)=>new D()	=>3(先计算new Foo()创建一个实例f，然后new f.getName，再把这个函数new一下，最后相当于把f.getName当作一个类，返回这个类的实例)

```

function的三个方法：call，apply，bind（三个方法都是用来改变某一个函数中this关键字的指向的）

**`call：`**

1.[fn].call([this],[param]...)

​	fn.call:当前实例通过原型链的查找机制，找到function.prototype上的call方法=>function call() {}

​	fn.call():把找到的call方法执行

​	当call方法执行的时候，内部处理了一些事情

​		=>首先把要操作函数中的this关键字变为call方法第一个传递的实参值

​		=>把call方法第二个以及以后的实参获取到

​		=>把要操作的函数执行，并且把第二个以后的传递进来的实参传给函数

```javascript
window.name='helinxiao';
let fn=function(){
  	console.log(this.name);	  
};
let obj={
  	name:'OBJ',
    fn:fn;
};
let oo={
    name:'OO'
};
fn();//=>this:window  'helinxiao'
obj.fn();//=>this:obj  'OBJ'
fn.call(oo);//=>this:oo 'OO'
fn.call(obj);//=>this:obj 'OBJ'

```

```javascript
let sum=function(a,b){
    console.log(this); //=>opt
};
let opt={n:20};
sum.call(opt,20,30);//=>call执行call中的this是sum把this（call中的）关键字替换为opt，把this（call中的）执行，把20，30分别传递给a，b//=>sum中的this是opt a=20 b=30


//练习
function fn1(){console.log(1);}
function fn2(){console.log(2);}
fn1.call(fn2);		//=>1  找到fn1中的this替换为fn2，但是fn1中没有this，所以还是执行fn1
fn1.call.call(fn2);	//=>2  fn1.call：A，首先执行A.call（fn2）将A中的this变为fn2再让A执行，A执行此时A中的this是fn2，让fn2中的this变为undefined，因为执行fn1.call的时候没有传递参数，然后让fn2执行
fnuction.prototype.call(fn1); //this：function.prototype   让function.prototype中的this变为fn1，然后让function.prototype执行，f.p是一个空函数，执行没有任何的输出。
function.prototype.call.call(fn1);//1

```

`call中的细节`：

​	1.在非严格模式下，如果参数不传，或者第一个参数是null/undefined，this都指向window

​	2.在严格模式下，第一个参数是谁，this就指向谁（包括null/undefined），不传this也是undefined

**`apply：`**

​	和call基本一模一样，唯一的区别在于传递参数的方式不同，apply需要将传递的参数放到一个数组中去。

fn.apply(obj,[10,20]);

**`bind：`**

​	和call基本一模一样，唯一的区别在于是立即执行还是等待执行

​	fn.call(obj,10,20); //改变fn中的this，并且立即执行。

​	fn.bind(obj,10,20);//改变fn中的this，此时的fn并没有执行（不兼容IE6~8）

**练习**

```javascript
//需求一求最大值
let ary=[12,13,14,132,45,64,75];
/*方法一：排序
	let max=ary.sort(function(a,b){
		return b-a;
	})()[0];
*/
/*方法二：数组遍历
	let max=ary[0];
	for (var i=1;i<ary.length;i++){
		if(max<ary[i]){
			max=ary[i];
		}
	}

*/
/*方法三：基于Math.max
	console.log(Math.max(ary));//=>NaN =>Math.max是获取一堆数中的最大值，需要我们把比较的数一个个的传进去=>Math,max(12,13,14),但是此时传递的是一个数组=>Math.max([12,13,14])这样只传递了一个值。
	1.eval：把字符串转换为JS表达式
	 eval（“1+2”）=>3
	2.括号表达式（小括号的引用）
	 用小括号包起来，里面有很多项（每一项用逗号分开），最后只获取最后一项的内容（但是会把其他的项都过一遍）
	 (function(){
	 	console.log(1);
	 },function(){
	 	console.log(2);
	 })() //=>2
	 
	 let a= 1==1?(12,13,14):null;
	 console.log(a); //14
	 括号表达式会改变this
	 
	 基于eval转换字符串为表达式
	 console.log(eval("Math.max"+"("+"ary.tostring()"+")"))
*/
/*基于apply
	console.log(Math.max.apply(null,ary));
	利用了apply的一个特征：虽然放的是一个数组，但是执行方法的时候，也是把数组中的每一项一个个的传递给函数
*/
/*基于ES6的展开运算符
	let max=Math.max(...ary);
	console.log(max);
*/

```

##### ES6的解构赋值

按照一个数据值的结构，快速解析获取到其中的内容

​	1.真实项目中一般都是针对于数组或者对象进行解构赋值

`数组的解构赋值`

```javascript
let ary=[12,13,14]
//let a=ary[0],b=ary[1],c=ary[2];  //把每一项赋值给a,b,c
let [a,b,c]=ary; //让等号左边和右边出现相同的数据结构，左边可以创建一些变量快速获取到右侧对应位置的值。
let [a]=ary // a=12
let [,,c]=ary //c=14
let [a,,c]=ary //a=12,c=14
let [a, ...b]=ary; //a=12  b=[13,14] "..."在此处称之为剩余运算符：除了前面的项，都放在一个数组中

//a和b交换位置
let a=12,b=13;
[a,b]=[b,a];

```

`对象的解构赋值`

```javascript
let obj ={name:hlx,age:25,sex:0};
let{name,age}=obj;//name=hlx,age=25   =>对象的解构赋值默认情况下要求：左侧变量名和对象中的属性名一致才可以
let {sex}=obj;//sex=0 =>左侧会自己在对象中去找

let {age:age1}=obj//=>25  给解构的属性名取别名作为我们使用的变量

```

“...”在ES6的语法中，三个点有三种含义

​	1.剩余运算符

​	2.拓展运算符

​	3.展开运算符

```javascript
//编写一个方法实现任意数字求平均值（去除数字中的最大最小值，然后算剩下数的平均数，保留小数点后两位）
let fn=function(){
    //=>把类数组转换为数组ary（把类数组克隆一份一模一样的，最后存储到数组中）=>数组的slice可以实现的克隆的
	let ary=[].slice.call(arguments,0);
    /*在ES6中
    	let ary=[...arguments];//把类数组转换为数组
    */
    //排序去除最大和最小
    ary.sort(function(a,b){
        return a-b;
    }).pop();
    ary.shift();
    return(eval(ary.join('+'))/ary.length).toFixed(2);
}
/*Array.prototype.myslice=function(){
  	//=>把操作的数组克隆一份 this:ary
    var newary=[];
    for(let i;i<this.length;i++){
    	newary.push(this[i]);	        
    }
    return newary;
};*/
var max=fn(10,11,32,45,6,78,67,98,34,56);
console.log(max);

```

##### 箭头函数 

```javascript
let fn=function(x,y){
  	  
};
//下面这种和上面是一样的效果
let fn=(x,y)=>{
    
};
fn(20,30)
---------------------------------------
let fn=x=>{
    //如果只有一个形参，我们可以省略小括号
}
fn(10)
---------------------------------------
let fn=function(x,y){
    return(x+y);
};
let fn=(x=0,y=0)=>x+y; //如果函数体中只有一句操作，并且是return的，我们可以省略大括号（可以给形参设置默认值）
---------------------------------------
let fn=x=>y=>x+y;
//这两个是一个函数
let fn=function(x){
    return function(y){
        return (x+y);
    }
}

```

1.箭头函数当中没有arguments（可以使用剩余运算符代替"..."）。

2.箭头函数中没有自己的执行主体（this），他的this都是继承上下文中的**this**

##### 获取数据和实现数据绑定

 真实项目中，页面的大部分数据都不是写死的，而是动态绑定的

A：从服务器端获取到数据（基于Ajax/Json等技术，通过服务器端提供的

数据API接口地址，把数据请求回来）

B：把获取的数据进行解析

c：把数据绑定在HTML页面中（数据绑定）：ES6中的模板字符串

*从服务器端获取的数据格式一般都是JSON格式的*

window.json

1.parse：把json格式的字符串转换为对象（json.parse()）

2.stringify：把对象转换为JSON格式的字符串(json.stringify())

 let obj={"name":"xxx"};   //json格式的对象

 let str='{"name":"xxx"}'; //json格式的字符串

**数据绑定**：依托获取的数据，把页面中需要展示的数据和结构都搞出来，

然后把创建好的数据和结构放到页面的指定容器中

1.字符串拼接

​	传统字符串拼接

​	ES6模板字符串拼接

​	模板引擎：原理也是字符串拼接

2.动态创建dom

​	creatElement

​	appendChild   

 弊端：操作起来太麻烦，而且性能消耗较大（DOM回流）

**ES6模板字符串**

let str=``(tab上面的键)



**DOM的映射机制**

页面中的HTML元素，和JS中通过相关方法获取到的元素集合或者元素对象存在映射关系（一个修改另外一个也会修改）

xxx.style.color='red'：把xxx元素对象对应堆内存中的style属性下的color属性值修改为‘red’（本质操作的是js的堆内存）；但是由于DOM的映射关系，页面中的标签和xxx元素对象是绑定在一起的，我们修改元素对象空间的值，页面中的元素会按照最新的值进行渲染；

在元素绑定之前，我们获取容器中元素，得到一个空的元素集合，元素数据绑定后，我们不需要重新获取，DOM的映射机制会帮我们把新增加的元素映射到之前获取的空集合中让其变为有元素的集合（querySelectorAll获取的集合是静态集合（staticNodeList），不存在上述所谓的映射机制，所以基于这种办法，数据绑定完成后需要重新获取一次才可以）



appendChild在追加元素对象的时候，如果这个元素之前容器中已经存在，此时不是克隆一份新的再追加到末尾，而是把原有的元素移动到末尾位置

### LESS

它是css的预编译语言，和他类似的还有sass/stylus...

css是标记语言，不是编程语言；而less就是让css具备面向对象编程的思想；但是浏览器不能直接识别和渲染less代码，需要我们把less代码预先编译为正常的css后，在交给浏览器渲染解析；

**less的编译**

- 在开发环境下编译（产品还正在开发）

	> 导入less.js就可以了

	```javascript
	<link rel="stylesheet/less" href="../index.less">
	<script src="./less-2.5.3.min.js"></script>
	
	
	```

- 在生产环境下编译（产品开发完了，部署到服务器上）

	> 项目上线，不能把less部署，这样用户每一次打开页面都需要重新的编译，非常耗性能，，我们部署到服务器上的是编译后的css

-------------------------------

定时器：设定一个定时器，并且设定了等到的时间，当到达指定的事件，浏览器会把对应的方法执行

[常用定时器]

​	setTimeout([function],[interval]) 	//只执行一次

​	setInterval([function],[interval])	//轮循定时器，每间隔一段时间都会把方法执行

​		[function]：到达时间后执行的方法（设置定时器的时候方法没有执行，到达指定时间浏览器帮我们执行）

​		[interval]：时间因子，需要等待的时间

定时器需要手动删除，clearTimeout/clearInterval：这两个方法中的任意一个，都可以清除用任何方法创建的定时器

1.设置定时器会有一个返回值，这个只是一个数字，属于定时器的编号，代表当前是第几个定时器，这个编号会累加

2.clearTimeout([序号])/clearInterval([序号])

**JS中的同步编程和异步编程**

- 浏览器是多线程的，JS是单线程的（浏览器只分配一个线程来执行JS）
- 进程大线程小：一个进程中包含多个线程，例如在浏览器中打开一个HTML页面就占用了一个进程，加载页面的时候，浏览器分配了一个线程去计算DOM树，分配其它的线程去加载对应的资源文件。。再分配一个线程去自上而下执行JS

​	同步编程：任务是按照顺序依次处理，当前这件事没有彻底做完，下一件事是执行不了的

​	异步编程：当前这件事没有彻底做完，需要等待一段时间才能继续处理，此时我们不等，继续执行下面的任务，当后面的任务完成后，再去吧没有彻底完成的事情完成。

​	**[JS中的异步编程]**：【sync=>micro=>macro】

​		**【宏任务 ：macro task】**

​				**1.所有的事件绑定都是异步编程。** xxx.onclick=function(){}

​				**2.所有定时器都是异步编程。**	setTimeout(function(){},1000)

​				**3.AJAX中一般都使用异步编程处理**

​				**4.回调函数也算是异步编程**

​				**5.Node中fs可以进行异步的I/O操作**

​		**【微任务 ：micro task】**

​				**6.process.nextTick**	

​				**7.Promise(async/await)**	=>Promise不是完全的同步，当在Excutor中执行resolve或者reject方法的时候，此时是异步操作，会先执行then/catch等，当主栈完成后，才会去调用resolve/reject把存放的方法执行

```javascript
console.log(1);
new Promise((resolve,reject)=>{
    //new promise 的时候回立即把Excutor函数（也就是传递的回调函数）执行，所以Promise本身可以理解为是同步的
    console.log(2);
    setTimeout(()=>{
        resolve();//promise内部机制：执行resolve会把之前基于then存放的方法执行
    },10);
}).then(()=>{	//执行完成Excutor,紧挨着执行then，执行then方法，会把传递的回调函数放到指定的容器中，等待触发执行（Promise内部的机制）
    console.log(3);
});
console.log(4);
```

Async/await

```javascript
function AA(){
    console.log(1);
    return new Promise((resolve,reject)=>{
        setTimeout(()=>{
            resolve();
        },10)
    });
}
async function fn(){
    console.log(2);
    let res=await AA();
    /*
     *先把AA执行，返回一个Promise实例，它会暂时跳出当前执行的函数（FN），也就是await后
     *面的代码先不执行放到等待区域中，主栈暂时空闲，当主栈中的其它任务完成主栈空闲，并且		 *AA中的Promise也已经计算完成最后的结果，在把之前放到等待区的内容，重新拿回主栈中执		*行
    */
    console.log(3);
}
fn();
console.log(4);
//=>2 1 4 3 =>await并不是同步
```

所有的JS中的异步编程仅仅是根据某些机制来管控任务的执行顺序，不存在同时执行两个任务这一说法。

**综合测试**

```javascript
async function async1(){
    console.log('async1 start');
    await async2();
    console.log('async1 end');
}
async function async2(){
    console.log('async2');
}
console.log('script start');
setTimeout(function(){
    console.log('setTimeout');
},0);
async1();
new Promise(function(resolve){
    console.log('promise1');
    resolve();
}).then(function(){
    console.log('promise2');
});
console.log('script end');
/*script start
async1 start
async2
promise1
script end
async1 end
promise2
setTimeout*/
```



-----------------------------

### 事件

1.什么是事件？

​	一个事情或者一个行为，对于页面元素来说，它的很多事件都是天生附带的，只要我们去操作这个元素，就会触发这些行为

“事件就是天生自带的行为，我们操作元素，就会触发相关的实践行为”

2.事件绑定：给天生自带的行为绑定方法，当事件触发，会把对应的方法执行（eg：oBox.onclick=function(){}）

3.元素天生自带的事件

[鼠标事件]

​	click：点击（pc端是点击，移动端是单击[移动端使用会有300ms 的延迟]）

​	dblclick：双击

​	mouseover：鼠标经过

​	mouseout：鼠标移出

​	mouseenter：鼠标进入

​	mouseleave：鼠标离开

​	mousemove：鼠标移动

​	mousedown：鼠标按下（鼠标左右键都触发，按下即触发）

​	mouseup：鼠标抬起（会先触发down和up才触发click）	

​	mousewheel：鼠标滚轮滚动

**mouseenter和mouseover的区别？**

1.over属于滑过（覆盖）事件，从父元素进入到子元素，属于离开了父元素，会触发父元素的out，触发了元素的over

​	enter属于进入，从父元素进入子元素，并不打算离开父元素，不会触发父元素的leave，触发子元素的enter

2.enter和leave阻止了事件的冒泡传播，而over和out还存在冒泡传播的

所以对于父元素的嵌套子元素这种情况，使用over会发生很多不愿意操作的事情，此时我们使用enter会更加简单，操作方便，所以真实项目中enter的使用会比over多

[键盘事件]

​	keydown，keyup，keypress

[表单元素常用事件]

​	focus：获取焦点

​	blur：失去焦点

​	change：内容改变

[其他常用事件]

​	load：加载完成

​	unlod,beforeunload,

​	scroll：滚动条滚动事件

​	resize：大小改变事件 window.onresize=function(){}当浏览器窗口大小发生改变

[移动端手指事件]

​	touch:

​		touchstart:手指按下

​		touchmove：手指移动

​		touchend：手指离开

​		touchcancel：因为意外情况导致手指操作取消

​	gesture：

​		gesturestart：手指按下

​		gesturechange：手指改变

​		gestureend：手指离开

[H5中的AUDIO/VIDEO音频事件]

​	canplay：可以播放（播放过程中可能出现由于资源没有加载完成，导致的卡顿）

​	canplaythrough：资源加载完成，可以正常无障碍播放



#### 事件绑定

[DOM0级事件绑定]

​	[element].onXXX=function(){}

[DOM2级事件绑定]

​	[element].addEventListener(‘XXX’,function(){},false);

​	[element].attachEvent('XXX',function(){}); [IE6~8]

目的：给当前元素的某个事件绑定方法（不管是基于DOM0还是DOM2），都是为了触发元素的相关行为的时候，能做点事情（也就是把绑定的方法执行）：“不仅把方法执行了，而且浏览器还给方法传递了一个实参信息值==>这个值就是事件对象”

```javascript
box.onclick=function(ev){
    //定义一个形参接收方法执行的时候，浏览器传递的信息值(事件对象：mouseevent鼠标事件对象，KeyboardEvent键盘事件对象，Event普通事件对象)
    //事件对象中记录了很多属性名和属性值，这些信息中包含了当前操作的基础信息，例如：鼠标点击位置的X/Y轴坐标，鼠标点击的是谁（事件源）等信息
    /*[mouseEvent]
     * ev.target:事件源（操作的是哪一个元素）
     * ev.clientX/ev.clientY:当前鼠标触发点距离当前窗口左上角的X/Y轴坐标
     * ev.pageX/ev.pageY:当前鼠标触发点距离BODY（第一屏幕）左上角的X/Y轴坐标
     * ev.preventDefault():阻止默认行为
     * ev.stopPropagation():阻止事件的冒泡传播
     * ev.type:当前事件类型
     *[KeyboardEvent]
     * ev.code:当前按键‘keyE’
     * ev.key:当前按键‘e’
     * ev.which/ev.keyCode:当前按键的键盘码
     * let code=ev.which||ev.keyCode；
     *=>常用的键盘码
     * 左-上-右-下：37-38-39-40
     * Backspace：8
     * Enter:13
     * space:32
     * Delete:46
     * Shift；16
     * Alt:18
     * Ctrl:17
     * ESC:27
     * F1~F12:112~123
     * 数字键：48~57
     * 小写字母：65~90
    */
}
```

**事件的默认行为**：事件本身就是天生就有的，某些时间触发，即使你没有绑定方法，也会存在一些效果，这些默认效果就是“事件的默认行为”

​	A标签的点击操作就存在默认行为

​		1.页面跳转

​		2.锚点定位（HASH定位（哈希定位））（基于HASH值我们还可以实现SPA单页面应用）

​	INPUT标签也有默认行为

​		1.输入内容可以呈现到文本框中

​		2.输入内容的时候会把之前输入的一些信息呈现出来（并不是所有情况下都有）

​	SUBMIT按钮也有默认行为

**阻止默认行为**：

​	1.阻止a标签的默认行为：很多时候我们使用a标签并不需要其跳转，仅仅是一个按钮，点击实现功能，也不想锚点定位

​	在结构中阻止：

```javascript
<a href="javascript:;">hlx </a>
```

​	在JS中可以阻止：给其cllick事件绑定方法，当我们点击A标签的时候，先触发click事件，其次才会执行自己的默认行为

**事件的传播机制**

​	冒泡传播：出发当前元素的某一个事件（点击事件）行为，不仅当前元素事件行为触发，而且其祖先元素的相关事件行为也会依次被处罚，这种机制就是“事件的冒泡传播机制”(按照HTML的结构而传播，和页面中的位置无关)

​	1.捕获阶段

​		当你点击的时候，首先会从最外层开始向内查找（找到操作的事件源），查找的目的是，构建出冒泡传播阶段需要传播的路线（查找就是按照HTML层级结构找的）

​	2.目标阶段

​		把事件源的相关操作行为触发（如果绑定了方法，则把方法执行）

​	3.冒泡传播

​		把当前事件源的祖先元素，按照捕获阶段规划的路线，自内而外，把当前事件源的祖先元素的相关事件行为触发（如果某一个祖先元素事件行为绑定了方法，则执行方法，没绑定方法，则行为触发了，什么都不做，继续向上传播即可）

xxx.onxxx=function(){} DOM0事件绑定，给元素的事件行为绑定方法，这些方法都是在当前元素事件行为的冒泡阶段（或者目标阶段）执行的

xxx.addEventListener('xxx',function(){},false) 第三个参数false也是控制绑定的方法在事件传播的冒泡阶段（或者目标阶段）执行；只有第三个参数为true才代表让当前方法在事件传播的捕获阶段触发执行（这种捕获阶段执行没啥实际意义，项目中不用）

#### 事件委托（事件代理）

利用事件的冒泡传播机制，如果一个容器的后代元素中，很多元素的点击行为（其它事件行为也是）都要做一些处理，此时不需要再向以前一样一个个获取一个个绑定了，我们只需要给容器的click绑定方法即可，这样不管点击的是哪一个后代元素，都会根据冒泡传播的传递机制，把容器的click行为触发，把对应的方法执行，根据事件源，我们都可以知道点击的是谁，从而做不同的事情即可。

--------------------------------------

### 响应式布局

 **一、viewport视口**

​		在pc端，我们开发的html页面运行在浏览器中，浏览器有多宽（一般浏览器代表设备的宽度）html就有多宽，也就是在浏览器宽度的视口中渲染和呈现我们的页面

​		移动端和PC端区别：不管移动端设备（代指打开的浏览器）的宽度是多少，HTML页面宽度是980（或者1024）=>导致的问题：如果在设备窗口想要把整个页面呈现出来（小窗口中完全展示大页面），我们只能把大页面进行缩放，HTML页面缩放了，那么页面中所有内容都缩放了

​	【解决方案】

​		只要让H5页面的宽度和手机设备的宽度保持一致即可，就不会出现手机渲染页面的时候把页面缩放的事情了

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
这个meta标签就是在设置VP（视口）的规则
	<!-- width=device-width 让HTML的宽度等于设备的宽度
	initial-scale：1.0  初始缩放比例是1:1（也就是既不放大也不缩小）
	user-scalable=no 禁止用户手动缩放
	maximum-scale=1.0 设置最大缩放比例为1:1
	minimum-scale=1.0 设置最小缩放比例为1:1（计步放大也不缩小=>部分安卓手机中设置user-scalable是不起作用的，需要这两个一起使用）
	....
	-->
```

    layout viewport:布局（页面）视口（和开发css等相关）

​	visual viewport：手机视口

​	ideal viewport：理想视口

​	真实的移动端项目开发中，一般是不会出现横向滚动条的，想让他不出现横向滚动条就要保证内容的宽度不超过HTML的页面宽度

​	移动端开发手机设备宽度不一定->HTML页面的宽度也不一定->所以内容的宽度一般也是不固定的（也就是所谓的百分比宽度）

​		移动端开发：外层盒子的宽度一般都是百分比设定的，很少有固定值的（里面具体的小元素可以固定）

**二、平时处理的移动端项目**

​	`1.PC端和移动端共用一套项目的（结构相对简单的：一般都是展示类的企业站）`

​		【设计师一般只给一套设计稿】

​		A：先做PC端（设计给的设计稿一般都是给PC端的）

​			一般宽度都是自适应的（具体情况有所不同）

​		B：切换到手机端，使用@media（媒体查询）把不同设备上不合适的样式进行修改

​			我们可以吧@media理解为JS中的条件判断：在不同条件中使用不同的css样式进行渲染

​			@media[媒体设备]

​					all->所有设备

​					screen->所有屏幕设备

​					print->所有打印机设备

​					....

​			@media[媒体设备] and [媒体条件] and [媒体条件] .....

​	`2.PC端和移动端是分开的两套不同的项目`

​		【设计师一般会给两套设计稿（PC+移动）】

​		=>PC端单独做（做的时候不需要考虑移动端响应式）

​			固定布局

​		=>移动端单独做（只需要考虑移动端响应式适配即可）

​			响应式布局

​				A.依然可以基于@media来处理（麻烦一些）

​				B.固定布局（viewport=>width=320px）：按照设计稿把320尺寸的写好即可（所有的尺寸都可以固定，而且都是设计稿的一半【因为设计稿都是大一倍的】），在其它设备上，让320的页面居中展示即可

​				C.scale等比缩放布局（严格按照设计稿的尺寸来写样式【没有啥自适应宽度，都是固定值】，在其它设备上，首先获取设备的宽度，让其除以设计稿的宽度，然后让原始写好的页面按照这个比例整体缩小即可）transform-origin：left top =>控制最终缩放的时候：不是从中心点缩放，而是从左上角  、、=>会导致一些问题列入字体模糊...

​				D.REM等比缩放：参考scale，只是使用rem单位来实现等比缩放（严格按照设计稿的尺寸编写【但是一般宽度让他自适应】，其余的值可以写成固定值->在编写css样式的时候，我们把所有的px单位都换算成REM单位->当加载页面的时候，根据当前设备的尺寸除以设计稿，根据比例动态调整REM和PX的换算比例）

​	**REM**是相对单位，相对于根元素（HTML标签）的字体大小设定的单位

​				E:CSS3中提供了flex-box伸缩盒子模型，基于这个属性，可以让某些效果处理起来更加的方便

-----------------------



### 一、HTML5（H5）

**1.新增加(修改/删除)的语义化标签**
  header
  footer
  main 主体
  section 区域
  article 文章区域
  aside 与内容无关的部分（例如：广告）
  nav
  figure 配图区域
  figcaption 配图说明

  mark 标记
  time 时间标记
  progress 进度条
  ...

**2.关于表单元素的新改革**
 [传统表单元素]
    input:text/password/radio/checkbox/file/hidden/button/submit/reset...
    select
    textarea 文本域
    button
    form
    label
    ...

 [新增一些表单元素或者是表单类型]
    input:search/email/tel/number/range/color/date/time/url...

**3.音视频标签**
  audio

​	 关于AUDIO的一些常用属性

​     [属性]

​     duration:播放的总时间(S)

​     currentTime:当前已经播放的时间(S)

​     ended:是否已经播放完成

​     paused:当前是否为暂停状态

​    volume:控制音量 (0~1)

 

​     [方法]

​     pause() 暂停

​     play() 播放

 

​     [事件]

​     canplay：可以正常播放（但是播放过程中可能出现卡顿）

   canplaythrough：资源加载完毕，可以顺畅的播放了

​     ended：播放完成

​     loadedmetadata：资源的基础信息已经加载完成

​     loadeddata：整个资源都加载完成

​     pause:触发了暂停

​     play:触发了播放

​     playing:正在播放中

  video
  =>让我们告别了FLASH时代

**4.canvas图形绘制**

**5.提供了一些新的API**
  本地存储：localStorage/sessionStorge
  获取地理位置： navigator.geolocation.getCurrentPosition 调取手机内部的GPS定位系统获取当前手机所在地的经纬度以及精准度等
  ...
  还提供了一些API，让我们可以通过浏览器调取手机内部的软件或者硬件（但是性能都不咋高，而且兼容性不是特别好）

6.websocket：socket.io 客户端和服务器端新的传输方式（即时通讯IM系统基本上很多是基于它完成的）

...



### 二、CSS3

  学习一些样式属性和选择器就差不多了

  [选择器]
    #ID
    .CLASS
    TAG
    *
    SELECTOR1,SELECTOR1... 群组选择器

```
A .B{} 后代
A.B{} 既具备A也具备.B的（同级二次筛选）
A>B{} 子代
A+B{} 下一个弟弟
A~B{} 兄弟

A[NAME=''] 属性选择器 NAME!='' / NAME^='' / NAME$='' / NAME*='' ...

A:HOVER
A:ACTIVE
A:VISTED
A:AFTER
A:BEFORE

A:NTH-CHILD
A:NTH-LAST-CHILD
A:NTH-OF-TYPE
A:NTH-LAST-OF-TYPE
A:NOT
A:FIRST-CHILD
A:LAST-CHILD

...
```

  [样式属性]
    1.基本常用的
      border-radius
      box-shadow
      text-shadow

```
2.背景的
  background -color / -image / -position / -repeat / -attachment / ...

  background-size：
       100px 100px  宽高具体值
       100% 100%  宽高百分比（相对于所在容器）
       cover  以合适的比例把图片进行缩放(不会变形)，用来覆盖整个容器
       contain 背景图覆盖整个容器（但是会出现，如果一边碰到容器的边缘，则停止覆盖，导致部分区域是没有背景图的）
       ...

  background-clip: 背景图片裁切
      border-box
      padding-box
      content-box

  background-origin：设置背景图的起始点
      border-box
      padding-box
      content-box

  ...

  filter

3.CSS3动画和变形(2D/3D)

  //=>变形不是动画
  transform:
     translate(X|Y|Z)  位移
     scale 缩放
     rotate 旋转
     skew 倾斜
     matrix 矩阵(按照自己设定的矩阵公式实现变形)
  transform-style:preserve-3d 实现3D变形
  transform-origin：变形的起点

  //=>过渡动画
  transition:
     transition-property:all/width... 哪些属性样式发生改变执行过渡动画效果，默认ALL，所有样式属性改变都会执行这个过渡效果
     transition-duration:过渡动画的时间，我们一把都用秒，例如：.5s
     transition-timing-function:动画运动的方式 linear(默认) ease ease-in ease-out ease-in-out cubic-bezier(执行自己设定的贝塞尔曲线)
     transition-delay:设置延迟的时间,默认是0s不延迟,立即执行动画
     ...

  //=>帧动画
  animation：
     animation-name 运动轨迹的名称
     animation-duration 运动的时长
     animation-timing-function 运动的方式(默认ease)
     animation-delay 延迟时间
     animation-iteration-count 运动次数(默认1  infinite无限次运动)
     animation-fill-mode 运动完成后的状态（帧动画完成后，元素会默认回到运动的起始位置，如果想让其停留在最后一帧的位置，设置这个属性值为forwards；backwards是当前帧动画如果有延迟时间，在延迟等待时间内，元素处于帧动画的第一帧位置；both是让帧动画同时具备forwards和backwards）
     ...

  //=>设置帧动画的运动轨迹
  @keyframes [运动轨迹名称] {
    from{
       //开始的样式
    }
    to{
       //结束的样式
    }
  }

  @keyframes [运动轨迹名称] {
     0%{
        //开始的样式
     }
     50%{}
     100%{
        //结束的样式
     }
  }

4.CSS3中的新盒子模型
  box-sizing: border-box / padding-box / content-box（默认值） 改变的就是我们在CSS中设置的WIDTH/HEIGHT到底代表啥  border-box让其代表整个盒子的宽高，当我们去修改PADDING或者BORDER，盒子大小不变，只会让内容缩放

  columns：多列布局

  flex：弹性盒子模型

5.一些其它的CSS3属性
  perspective:视距 实现3D动画必用的属性
  @media:媒体查询 实现响应式布局的一种方案
  @font-face:导入字体图标
  ...
```

### 三、响应式布局开发

   响应式布局：在不同尺寸的设备上都能良好的展示，这就是响应式布局设计（Responsive Layout）

   公司中的产品形态：
     1.PC端(全屏页面需要宽度自适应，但是一般都是固定宽度的)
     2.PC+移动端用同一套项目（简单的页面，例如：产品介绍，公司展示类的官网等）
     3.移动端（移动端设备尺寸差异较大，需要做响应式布局开发）
       嵌入到APP中的H5
       微信中分享出来的H5
       微信公号
       小程序
       靠浏览器访问的H5
       ...
     4.RN(React Native) / ionic / cordova ... JS开发APP的框架，使用JS代码开发APP，最后框架会把代码转换为 安卓和IOS 需要的代码

   如何实现响应式布局开发?
     最常用的方案：REM等比缩放响应式布局

```
 做移动端H5开发，首先加META标签
    <!--meta:vp [Tab]-->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    REM和PX一样都是样式单位，PX是固定单位，REM是相对单位（相对于当前页面根元素HTML的字体设定的单位）

    我们开始给HTML的字体大小设置为100PX(1REM=100PX)，接下来我们写样式的时候，把所有的尺寸都用REM设定（测量出来的PX值/100就是应该设置的REM的值）,如果HTML的FONT-SIZE不变，用REM和PX一样，但是如果字体大小改变，也就是改变了REM和PX之间的换换算比例，那么之前所有用REM做单位的样式都会自动按照最新的比例进行缩放（实现了改动HTML的FONT-SIZE，整个页面中的元素都跟着缩放了，牵一发而动全身）

    真实项目中，设计师给给我们一套设计稿（常用的尺寸：640*1136  750*1334 640*960 ...），拿到设计稿后，我们严格按照设计稿中的尺寸去编写样式
       HTML{
          FONT-SIZE:100PX;
       }
       接下来写样式，把测量出来的PX都除以100变为REM，所有的单位基于REM来搞
       =>假设设计稿是750,也就相当于750的设备下,1REM=100PX

    我们页面运行在320的设备上，我们需要修改HTML的字体大小，以此实现页面跟着整体缩放：320/750*100 =>当前设备上HTML的字体大小
```



### 四、微信二次开发（小程序） =>Hybrid混合APP开发

​	Hybrid混合APP开发

1.前端做的都是H5页面  WebApp
  ->运行在浏览器中
  ->移动端不仅可以运行在浏览器中，还可以运行在 APP 中（例如：微信、自己公司的APP中）

  [优点]
    及时更新（不需要用户选择，我们只需要把服务器上的源文件更新，用户访问的永远是最新的）
    跨平台

  [弊端]
    不是直接运行在操作系统中的吗，是运行在浏览器或者APP中的，所以不能直接的操作手机上的软硬件（运作模式：H5通知浏览器或者APP我们想做什么 -> 浏览器调取手机的软硬件 ->浏览器把信息返回给H5）
    性能没有APP好
    ...

2.APP不是H5，它是原生的应用 NativeApp
  ->IOS: object-c / swift  (需要C的功底)
  ->安卓：java-native   (需要JAVA功底)

 [优点]
   用户把安装包下载到手机上进行安装，后期程序是直接运行在手机操作系统中的
     A:性能高
     B:可以调取手机内置的软件或者硬件（例如：调取摄像头、重力感应器、通讯录等）[前提用户需要同意才可以]

 [弊端]
   不能跨平台，一款产品需要两个团队开发两套不同的安装包
     A:成本大
     B:版本不统一
   不能及时更新
   苹果商店上传一款APP需要7天审核周期

3.Hybrid混合开发模式
  把传统IOS和安卓开发与H5开发结合在一起来做（微信公众号开发：把我们做的H5运行在微信APP中）

4.ReactNative ionic 微信小程序 ...



### 五、移动端事件

### 六、移动端常用的插件、类库、框架等

-------------------------------

### JS中this汇总

**JS中的this汇总**

this：当前方法执行的主体，（谁执行的这个方法，那么this就是谁，所以this和当前方法在哪创建或者在哪执行都没有必然的关系）

​	1.给元素的某个事件绑定方法，方法中的this都是当前操作的元素本身

```javascript
document.body.onclick=function(){
    //this:body
}
```

​	2.函数执行，看函数前面是否有点，有的话，点前面是谁this就是谁，没有点，this就是window（在JS的严格模式下，没有点就是undefined）

```javascript
let fn=function(){
    console.log(this.name);
};
let obj={
    name:'haha',
    fn:fn
}
fn();	//this:window
obj.fn();	//this:obj
```

​	3.构造函数执行，方法中的this一般都是当前类的实例

```javascript
let fn=function(){
    this.x=100;//this:fn
};
let f=new fn;
```

​	4.箭头函数中没有自己的this，则this是上下文中的this

```javascript
let obj={
    fn:function(){
        //this:obj
        setTimeout(()=>{
            //this:obj
        },1000);
    }
};
obj.fn();
```

​	5.在小括号表达式中，会影响this的指向

```javascript
let obj={
    fn:function(){
        console.log(this);
    }
};
obj.fn(); //this :obj
(12,obj.fn)();	//this :window
```

​	6.使用call、apply、bind可以改变this的指向

```javascript
fn.call(obj);//this:obj
fn.call(12);//this:12
fn.call();	//this:window  在非严格模式下call、apply、bind第一个参数不写或者写null和undefined，this都是window，在严格模式下写谁就是谁，不写是undefined
```



-----------------------

### JS盒子模型属性

​	=>在JS中通过相关的属性可以获取（设置）元素的样式信息，这些属性就是盒子模型属性（基本上都是有关于样式的）

​	**client**（top/left/height/width）

​		1.clientWidth & clientHeight：获取当前可视区域的宽高（内容的宽高+左右/上下padding），和内容有溢出无关和是否设置了overflow：hidden也无关，就是我们设定的内容的宽高+padding。（如果没有设置高度，则会以内容的高度+padding为准）

​		获取当前页面的可视区域宽度和高度:

```javascript
document.documentElement.clientWidth||document.body.clientWidth   document.documentElement.clientHeight||document.body.clientHeight
```

​		2.clientTop & cliientLeft ：获取（上/左）边框的宽度

```javascript
xxx.clientTop
xxx.cliientLeft
```

​	**offset**（top/left/height/width/parent）

​		1.在client的基础上加上border（和内容是否溢出也没有关系）

```javascript
xxx.offsetWidth
xxx.offsetHeight
```

​		2.offsetLeft & offsetTop:获取当前盒子距离其父级参照物的偏移量（左偏移/上偏移）

```javascript
xxx.offsetLeft
xxx.offsetTop
```

​		3.offsetParent：获取当前盒子的父级参照物

```javascript
xxx.offsetParent
```

​			参照物：同一平面中，元素的父级参照物和他的结构没有必然的关系，默认他们的参照物都是body（当前平面最外层的盒子） BODY的父级参照物是null

​			参照物可以改变：构建出不同的平面即可（使用zindex，但是这个属性只对定位有作用），所以改变元素的定位（position：relative/absolute/fixed）可以改变其父级参照物

**scroll**  (top/left/heigt/width)

​		1.scrollWidth & scrollHeight ：真实内容的宽高（不一定是自己设定的值，因为可能存在内容溢出，溢出的内容也要算上）+左/上padding（没有内容溢出和client一样）在不同的浏览器中，或者是否设置了overflow：hidden都会对最后的结果产生影响，所以这个值仅作参考。

​		2.scrollTop/scrollLeft：滚动条卷去的宽度或者高度

​			最小卷去值：0

​			最大卷去值：document.docunmentElement.scrollTop-document.documentElement.clientHeight

```javascript
document.docunmentElement.scrollTop
```





------

**通过JS盒模型属性获取值的特点**

1.获取的都是数字不带单位

2.获取的都是整数，不会出现小数（一般都是四舍五入，尤其是获取的偏移量）

3.获取的结果都是复合样式值（好几个元素的样式组合在一起的值），如果只想获取单一样式值（例如：只想获取padding，我们的盒子模型属性就操作不了了（这不嫩能说没有用，真实项目中，有的时候我们就需要获取组合的值来完成一些操作）

**获取元素具体的某个样式**

1.[元素].style.xxx 操作获取

​	只能获取所有写在元素行内上的样式（不写在行内上，不管你有没有写都获取不到，真实项目中我们很少会把样式写在行内上）

=>outer.style.width =>''(width是写在样式表中的)

2.获取当前元素所有经过浏览器计算的样式

​	经过计算的样式：只要当前元素可以在页面中呈现（或者浏览器渲染他了），那么他的样式都是被计算过的。不管当前样式写在哪，不管你是否写了（浏览器会给元素设置一些默认样式）

// 标准浏览器（IE9+）

​	window.getComputedStyle([元素],[伪类，一般都写null]),获取到当前元素所有被浏览器计算过的样式（对象）

```javascript
window.getComputedStyle(outer,null).width
```

//IE6-8

​	[元素].currentStyle 获取经过计算的样式

封装一个方法快速获取当前css某一个样式的属性值

```javascript
let getCss =function(curEle,attr){
    let val=null;
    if(typeof window.getComputedStyle ==='undefined'){
        return;
    }
    let val=window.getComputedStyle(curEle,null)[attr];
    let reg=/^-?\d+(\.\d+)?(px|rem|em|pt)?$/i
    reg.test(val)?val=parseFloat(val):null;
    return val
};
onsole.log(getCss(outer,'border'));
```

设置当前元素的某一个具体样式的属性值

```javascript
let setCss=function(curEle,attr,value){
     /*
     * 细节处理
     *   1.如果需要考虑IE6~8兼容，透明度这个样式在低版本浏览器中不是使用opacity，而是filter（我们两套都要设置）
     *   2.如果传递进来的VALUE值没有带单位,我们根据情况设置PX单位
     *     ->某些样式属性才会加单位：WIDTH/HEIGHT/PADDING(LEFT...)/MARGIN(LEFT...)/FONT-SIZE/TOP/LEFT/BOTTOM/RIGHT...
     *     ->用户自己传递的VALUE值中是没有单位的
     */
    if(attr=='opacity'){
        curEle.style.opacity=value;
        curEle.style.filter='alpha(opacity=${value *100})';
        return;
    }
    if(!isNaN(value)){
        //=>IS-NaN检测的结果是FALSE：说明VALUE是纯数字没单位
        let reg = /^(width|height|fontSize|((margin|padding)?(top|left|right|bottom)?))$/i;
        reg.test(attr) ? value += 'px' : null;
    }
    curEle['style'][attr] = value;
}

```

批量设置样式的属性值

```javascript
let setGroupCss=function(curEle,option={}){
    //=>遍历传递的OPTIONS,有多少键值对,就循环多少次,每一次都调取SET-CSS方法逐一设置即可
    for (let attr in options) {
        if (!options.hasOwnProperty(attr)) break;
        //=>options:传递进来的需要修改的样式对象(集合)
        //=>attr:每一次遍历到的集合中的某一项(要操作的样式属性名)
        //=>options[attr]:传递的要操作的样式属性值
        setCss(curEle, attr, options[attr]);
    }
}
setGroupCss(outer,{
    width:600px;
})

```

*FOR-IN循环只遍历当前对象可枚举（可遍历）的属性*

​	1.对象的私有属性(自己写的)是可枚举的

​    2.浏览器内置的属性一般都是不可枚举的

​    3.自己在类的原型上设置的属性也是可枚举的,FOR-IN循环的时候也会被遍历出来（一般情况下我们是不想遍历到原型上的公有属性的）





### 实例：跑马灯

js

```javascript
/* js中的定时器
setInterval(()=>{},1000); */
let wrapper = document.querySelector('ul');
/*为了实现无缝，将元素克隆一份放到末尾 */
/* let wrapperList=wrapper.querySelectorAll('li');
let frg=document.createDocumentFragment();  //创建一个文档碎片，防止文档回流
[].forEach.call(wrapperList,(item)=>{  //遍历每一项，并且将其克隆并添加到创建的文档碎片中
    frg.appendChild(item.cloneNode(true));
});
wrapper.appendChild(frg);
frg=null; */

wrapper.innerHTML += wrapper.innerHTML; //简单的实现克隆，因为wrapper.innerHTML存储的就是那几个标签

utils.css(wrapper, 'width', utils.css(wrapper, 'width') * 2);//修改wrapper的宽度

setInterval(() => {
    //获取当前wrapper的left值,减去步长，赋值给元素即可
    let curl = utils.css(wrapper, 'left');
    curl += -1;
    utils.css(wrapper, {
        left: curl
    });
    //实现无缝：当我们UL距离marqueeBox的左偏移已经是整个wrapper的一半宽度，此时让wrapper立马移动到left=0的时候
    if(Math.abs(wrapper.offsetLeft)>=utils.css(wrapper,'width')/2){
        utils.css(wrapper,'left',0);
    }
}, 14);

```

html

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="../../reset.min.css">
    <title>跑马灯</title>
    <!-- <style>
        marquee{
            display: block;
            margin: 20px auto;
            height: 30px;
            width: 600px;
            line-height: 30px;
            background-color: lightblue;
        }
    </style> -->
    <style>
        .marqueeBox{
            position: relative;
            margin: 30px auto;
            height: 100px;
            width: 500px;
            border: 1px solid green;
            overflow: hidden;
        }
        .wrapper{
            position: absolute;
            top: 0;
            left: 0;
            width: 900px;
            height: 100px;
        }
        .wrapper li{
            float: left;
            width: 100px;
            height: 100px;
            line-height: 100px;
            text-align: center;
            font-size: 20px;
        }
        .wrapper li:nth-child(3n+3){
            background-color: aqua;
        }
        .wrapper li:nth-child(3n+2){
            background-color:lightblue;
        }
        .wrapper li:nth-child(3n+1){
            background-color: lightgreen;
        }
    </style>
</head>

<body>
    <!-- 很早以前使用marquee实现跑马灯，无法实现无缝连接，开始显示内容的时候有空白，性能消耗大 -->
    <!-- <marquee behavior="" direction="">大苏打交换机法国海军撒谎附件是快递发货集合发动机哈卡大家分厘卡大家粉红色的金卡八年发表电视阿布发货VS的环境发v不合适v的给VS大部分健康不健康的吧</marquee> -->
    <div class="marqueeBox">
        <ul class="wrapper">
            <li>1</li>
            <li>2</li>
            <li>3</li>
            <li>4</li>
            <li>5</li>
            <li>6</li>
            <li>7</li>
            <li>8</li>
            <li>9</li>
        </ul>
    </div>
    <script src="../../utils.js"></script>
    <script src="../js/跑马灯.js"></script>
</body>

</html>

```









