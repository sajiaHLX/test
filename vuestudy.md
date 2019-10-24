### 创建Vue实例传入的OPTIONS

options中可以包含很多的选项：https://cn.vuejs.org/v2/api/

目前掌握的：

- **el：**
	- 类型：String|HTMLElement
	
	- 作用：决定之后Vue实例会管理哪一个DOM
	
	- ```html
		el:'#app',
		```
	
- **data：**
	- 类型：object|Function(组件当中data必须是一个函数)
	
	- 作用：Vue实例对应的数据对象
	
	- ```html
		data:{
		        movies:['海贼王','进击的巨人','火影忍者'],
		        message:'hello world',
		        isactive:true,
		        first:'h',
		        last:'l',
		    },
		```
	
- **methods：**
	- 类型：{[key：string]：Function}
	
	- 作用：定义属于Vue的一些方法，可以在其他地方调用，也可以在指令中使用
	
	- ```html
		methods: {
		        active:function(index){
		          console.log(index);
		          this.isactive=!this.isactive;
		        }
		      }
		```
	
- **computed：**

	- 类型：{[key：string]：Function}

	- 作用：计算属性，一般没有set方法，只有get方法（只读属性）

	- ```html
		computed: {
		        fullName:function(){
		          return this.first+' '+this.last;
		        }
		      },
		<!--计算属性的本质
		computed: {
			fullName:{
		        get:function(){
		          return this.first+' '+this.last;
		        }
		      }
			},
		-->
		```

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

- **v-bind(绑定属性)**

  - 缩写：**：**

  - 有些内容和属性需要动态绑定，比如a的href属性，img的src属性

  - ```html
    <img v-bind:src="imgUrl" alt="">
    <img :src="imgUrl" alt=""> <!--简写(语法糖)-->
    ```

  - 绑定class有两种方式：

    - 对象语法

    	- ```html
    		用法一：直接通过{}绑定一个类
    		<h2 :class="{'active':isactive}"></h2>
    		用法二：通过判断传入多个值
    		<h2 :class="{'active':isactive,'line':isLine}"></h2>
    		用法三：和普通的类同时存在
    		<h2 class="title" :class="{'active':isactive}"></h2>
    		用法四：如果类过于复杂，可以放在一个methods或者computed中
    		注：classes是一个计算属性
    		<h2 class="title" :class="classes"></h2>
    		```

    - 数组语法

- **v-bind(绑定style)**

	- ```html
		50px必须加上单引号，否则会当做变量解析然后报错。
		<h2 :style="{fontSize:'50px'}"></h2>
		finalSize当做一个变量使用
		<h2 :style="{fontSize: finalSize + 'px'}"></h2>
		```
	
- **v-if**

	- ```html
		<h2 v-if="isShow">{{message}}</h2>通过控制isShow来判断是否显示message
		```

- **v-if和v-else**

	- ```html
		<h2 v-if="isShow">{{message}}</h2>
		<h2 v-else>{{message1}}</h2>
		```

- **v-if和v-else-if和v-else**

	- ```html
		<h2 v-if="score>=90">优秀</h2>
		<h2 v-else-if="score>=80">良好</h2>
		<h2 v-else>舒服</h2>
		```

### 事件监听

- **v-on**

	- 缩写：@

	- ```html
		<button @click="">+</button>
		```

	- 参数：如果该方法不需要额外的参数，那么方法后的()不用添加（但是方法本身需要一个参数，但是将括号省略了，那么会默认将原生事件event参数传递进去），如果需要也可以使用$event传递原生事件。

- 修饰符

	- .stop：调用event.stopPropagation()

		```html
		<button @click.stop='btn1click'>按钮1</button>
		```

	- .prevent：调用event.preventDefault()，阻止事件的默认行为

		```html
		<a href="http://www.baidu.com" @click.prevent>aaa</a>
		```

	- .{keyCode|keyAlias}：只当事件是从特定键触发时才触发回调

		```html
		<input type="text" @keyup='keyup'>监听键帽
		<input type="text" @keyup.enter='keyup'>监听回车键（键别名）
		<input type="text" @keyup.13='keyup'>监听键代码
		```

	- .native：监听组件根元素的原生事件

	- .once：只触发一次回调

		```html
		<button @click.once="onceClick">an</button>
		```

		

		