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





--------------------------

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











