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

原型链：它是一种基于\_\_proto\_\_向上查找的机制，当我们操作实例的某个属性和方法的时候，首先找自己空间中私有的属性或者方法1.找到了则结束查找。2.没找到，则基于\_\_proto\_\_找到所属类的prototype，如果找到则使用共有的，如果没找到，则基于原型上的\_\_proto\_\_继续向上查找，一直找到Object.prototype的原型为止，如果还没有，则操作的属性或者方法不存在



![prototype1（1）](D:\BaiduNetdiskDownload\2018年第二期源码、笔记\2018年第二期源码、笔记\WEEK1\0415DAY5\prototype1（1）.png)

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

![Array的两种角色](D:\BaiduNetdiskDownload\2018年第二期源码、笔记\2018年第二期源码、笔记\WEEK2\0418DAY2\Array的两种角色.png)

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



#### LESS

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












