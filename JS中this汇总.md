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













