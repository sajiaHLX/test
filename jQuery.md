	1.类库：JQ/ZEPTO...提供一些真实项目中常用的方法，任何项目都可以把类库导入进来，调取里面的方法实现自己需要的业务逻辑

​	2.插件：具有一定的业务功能，列如，我们可以封装轮播图插件，选项卡插件，模态框插件等（插件规定了当前这个功能的样式结构，把实现功能的js进行封装，以后想实现这个功能直接导入插件即可）swiper/iscroll/jquery-dialog/jquery-drag/jquery-datepicker/ECharts

​	3.UI组件：把结构，css，js全部都封装好了，我们想要实现功能直接导入就好了（偶尔需要修改）bootstrap......

​	3.框架：具备了一定的编程思想，要求我们按照框架的思想开发，一般框架中提供了常用的类库方法，提供了强大的插件功能，有的也提供了强大的UI组件...React/Vue/Angular/Backbone/Sea.js/Require.js ...

### jQuery

基于原生JS封装的一个类库，提供了很多方法，而且这些方法是兼容所有浏览器的。

jQuery是一个类（也是一个普通对象）：函数的两种角色，JQ是一个类库提供了很多方法，其中这些方法有两部分

​		1.放到JQ原型上的（jQuery.fn/jQuery.prototype）,这里面的方法是供JQuery实例调取使用的。

​		2.把JQ当做一个普通对象，在对象上设置一些私有的属性和方法，这类方法以后用的时候直接jQuery.xxx()执行即可

JQ选择器：基于各种选择器创建的一个实例（JQ对象）

​	1.selector选择器的类型（一般都是字符串，但是支持函数或者元素对象）

​		jQuery选择器的selector可以是字符串，字符串的格式有两种

​			=> 选择器

​			=> HTML字符串拼接的结构：把拼接好的HTML字符串转换为JQ对象，然后可以基于appendto等方法追加到页面中

​	2.context基于选择器获取元素时候指定的上下文（默认document）

JQ对象：一个类数组结构（JQ实例），这个类数组集合中包含了获取的元素

EACH：JQ中的EACH方法是用来进行遍历的（类似于数组中的foreach）

​	[可遍历的内容]

​		1.数组

​		2.对象	

​		3.类数组（JQ对象）

​	[三种EACH]

​		1.给jQuery设置的私有属性	$.each()

```javascript
$.each([12,23,45],(index,item)=>{
    //参数的顺序和内置的FOREACH相反
    console.log(index,item);
});

$.each({name :'hlx' ,age :12,sex:'man'},(key,value)=>{
    //原理就是for in循环
    console.log(key,value);
});
```

​		2.给实例设置的公有属性	$([selector]).each()

```javascript
$('.tabBox li').each(function(index,item){
	//非箭头函数：this===item，当前遍历的这一项（原生的JS对象）0
    //=>$(this)把当前这一项转换为JQ对象
    $(this).click(function(){
       	//给每一个遍历的LI都绑定一个点击事件
       	//this:当前点击的LI（原生的JS对象）
        $(this).css({
            color:'red';
        });
    });
});
```

​		3.内置的EACH

```javascript
$('.tabBox li').click(function(){
    //=>获取的JQ集合中有三个，我们此处相当于给三个LI都绑定了点击事件（JQ在调取click的时候，会默认把三个集合EACH遍历，把每一项都给click了）
    $(this).css({
        color:'red'
    });
});

$('.tabBox li').css({
    color:'green'
});
```











