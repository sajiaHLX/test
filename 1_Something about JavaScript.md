## JS中一些关于字符串的知识
>在JS中所有由单引号或者双引号包起来的都是字符串，每个字符串都是由零或多个字符组成
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
字符串是基本的数据类型，字符串的每一次操作都是值直接进行操作，不像数组一样是基于空间地址来操作的，所以不存在原有字符串是否改变这一说，肯定都是不变的
**`charAt/charCodeAt`**
作用：charAt根据索引获取指定位置的字符，charCodeAt不仅仅获取字，它获取的是字符对应的Unicode编码值（ASCII码值）
参数：索引
返回：字符或者对应编码
![9d2d0197280d6bf87eaf66f17730539f.png](en-resource://database/498:1)
![20cd0baccaea0b8cc348bcf30cc69c28.png](en-resource://database/500:1)
****indexOf/lastindexOf****
基于这两个方法，可以获取字符在字符串中第一次或者最后一次出现位置的索引，不包含这个字符返回-1，所以可以基于这两个方法，验证当前字符串中是否包含某个字符
```
var str='hlxshibaba';
if(str.indexOf('@')>-1){
    //=>如果条件成立说明包含@符号
}
```
**`slice`**
作用：str.slice(n,m)从索引n开始找到索引为m处（不包含m），把找到的字符当作新字符串返回
![e532e5e54287963e889fda2d366d245f.png](en-resource://database/502:1)
**`substring`**
和slice语法一样，唯一区别在于slice支持负数索引，而substring不支持
**`substr`**
也是字符串的截取方法
语法：str.substr(n,m)，从索引n开始截取m个字符
![27f06bdf099b85cc65269f0041951f15.png](en-resource://database/504:1)
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
>![5926e296251dff907195965f29d5cdf9.png](en-resource://database/506:1)
### URL地址问号传参解析
>有一个URL地址“http://www.hlxshibaba.com/stu/?lx=1&name=AA&sex=man”地址问号后面的类容是我们需要解析出来的参数信息
>{
>lx:1，
>name:'AA',
>sex:'man'
>}
>![a67cd4958b2ca8355e765f93a67add70.png](en-resource://database/512:1)


### JS中的数学函数Math
Math称为数学函数，但他属于对象类型
```javascript
typeof Math =>"object"
```
之所以叫做数学函数，是因为Math这个对象中提供了很多数字的方法
#### Math中提供的常用方法
**`取绝对值`**：取绝对值
![fc5e77ca42e1021091186303b02579b9.png](en-resource://database/508:1)
**`ceil/floor`**：向上（变大）或者向下（变小）取整
![e5307c551774b7236d41ca774ad35014.png](en-resource://database/510:1)
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
>1.获取的元素集合是一个类数组，不能直接使用数组的方法
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
>![6dc585f91834456be1311f3b819abc28.png](en-resource://database/514:1)

需求二：获取当前元素的上一个哥哥元素节点
>previousSibling:上一个哥哥节点
>previousElementSibling：上一个哥哥元素节点（但是不兼容）
>![2adb9fee4a9bdded5aa70c1500e7636a.png](en-resource://database/516:1)


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
>![84fd6bf9ec40ae47fd90bdca4407b2da.png](en-resource://database/518:1)


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

