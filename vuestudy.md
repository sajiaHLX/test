### 创建Vue实例传入的OPTIONS

options中可以包含很多的选项：https://cn.vuejs.org/v2/api/

目前掌握的：

- **el：**
	- 类型：String|HTMLElement
	- 作用：决定之后Vue实例会管理哪一个DOM
- **data：**
	- 类型：object|Function(组件当中data必须是一个函数)
	- 作用：Vue实例对应的数据对象
- **methods：**
	- 类型：{[key：string]：Function}
	- 作用：定义属于Vue的一些方法，可以在其他地方调用，也可以在指令中使用

### 插值的操作

- **mustache语法（双大括号）**

	- mustache语法中，不仅可以直接写变量，还可以写简单的表达式

	- ```html
		<div id="app">{{message}}
		    <h2>{{first+second}}</h2>
		    <h2>{{first+' '+second}}</h2>
		    <h2>{{first}} {{second}}</h2>
		    <h2>{{content*2}}</h2>
		</div>
		  <script src="js/vue.js"></script>
		  <script>
		    const app = new Vue({
		      el: '#app',
		      data: {
		        message:'i love code',
		        first:'firstname',
		        second:'lastname',
		        content:100
		      }
		    })
		  </script>
		```

- **v-once**

	- 该指令后面不需要更任何表达式（比如之前的v-for后面是有表达式的）

	- 该指令标识元素和组件只渲染一次，不会随着数据的改变而改变

	- ```html
		<h2 v-once >{{message}}</h2>
		```

- **v-html**

	- 该指令后面往往会跟上一个string类型，会将string的HTML解析出来并且进行渲染

	- ```html
		<h2 v-html="link"></h2>
		....
		link:'<a href="http://www.baidu.com">百度一下</a>'
		....
		```

- **v-text**

	- 用于将数据显示在界面中，通常接收一个string类型

	- ```html
		<h2 v-text="message"></h2>
		```

- **v-pre**

	- 用于跳过这个元素和它的子元素的编译过程，用于显示原本的mustache的语法

	- ```html
		<h2 v-pre>{{message}}</h2>
		```

- **v-cloak**

	- 在vue解析之前，div中有一个v-cloak属性，此时在样式中有display：none，所以不显示

	- 在vue解析之后，div中没有v-cloak属性

	- ```ht
		<style>
		    [v-cloak]{
		      display: none;
		    }
		</style>
		<div id="app">
		    <h2>{{message}}</h2>
		    <h2 v-cloak>{{message}}</h2>
		</div>
		```

