### 创建Vue实例传入的OPTIONS

#### 注意事项

- vue中存在一个内部复用的问题，比如下面的input标签，如果用户在input中输入了值，再去点切换，那么input中用户的输入不会被去掉。如果不想要这个内部复用，则需要给两个input加上不同的key属性。

	```html
	<span v-if="isUser">
	    <label for="username">账号登录：</label>
	    <input type="text" placeholder="用户账号登录" id="username">
	</span>
	<span v-else>
	    <label for="email">邮箱登录：</label>
	    <input type="text" placeholder="用户邮箱登录" id="email">
	</span>
	<button @click="user()">账号/邮箱登录</button>
	```

	

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
	
- **v-show**

	- 和v-if类似都是判断是否显示信息
	- 与v-if的不同处：
		- v-if：当条件为false时，包含v-if指令的元素，根本就不会存在dom中，当条件为true时，会重新创建一个元素
		- v-show：当条件为false时，v-show只是给元素添加了一个行内样式：display：none
	- 如何选择v-if和v-show：
		- 如果需要在显示和不显示之间切换频率很高使用v-show，否则使用v-if

- **v-for**

	- 不需要索引值

		```html
		<li v-for="item in names">{{item}}</li>
		```

	- 需要索引值

		```html
		<li v-for="(item,index) in names">{{index+item}}</li>
		```

	- 获取对象的value

		```html
		<li v-for="value in hlx">{{value}}</li>
		```

	- 获取对象的value和key

		```html
		<li v-for="(value,key) in hlx">{{key}}:{{value}}</li>
		```

	- 获取对象的value和key和索引值

		```html
		<li v-for="(value,key,index) in hlx">{{key}}:{{value}}:{{index}}</li>
		```

		**响应式的数组方法**

		```javascript
		1.push：向数组末尾添加元素
			this.names.push('aaa','bbb');
		2.pop：删除数组末尾的元素
			this.names.pop()
		3.shift：删除数组的第一个元素
			this.names.shift();
		4.unshift：向数组的开始添加元素
			this.names.unshift('aaa','bbb');
		5.splice：删除元素、插入元素、替换元素
			this.names.splice(1,1);
		    this.names.splice(1,0,'aaa','bbb')
		    this.names.splice(1,1,'aaa')
		6.sort：为数组排序
			this.names.sort()
		7.reverse：为数组倒序
			this.names.reverse();
		```

		**不是响应式的**

		```javascript
		通过索引修改数组中的元素
			this.names[1]='abccc';
		```

- **v-model表单绑定**

	- 表单控件在实际开发中非常常见，特别是对于用户信息的提交，需要大量的表单，Vue中使用v-model指令来实现表单元素和数据的双向绑定

		```html
		<input type="text" v-model="message">
		```

	- **修饰符**

		- lazy修饰符

			- 默认情况下，v-model默认是在input事件中同步输入框数据的，也就是说，一旦有数据发生改变对应的data中的数据就会改变

			- lazy修饰符可以让数据在失去焦点或者回车时才更新

				```html
				<input type="text" v-model.lazy="message">
				```

				

		- number修饰符

			- 默认情况下，在输入框中无论我们输入的是数字还是字母，都会被当做字符串来处理
			- number修饰符可以让在输入框中输入的内容自动转换成数字类型

		- trim修饰符

			- 如果输入的内容收尾有很多空格，通常我们希望将它去除
			- trim可以过滤内容给左右两边的空格

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

### 组件化开发

- 组件不可以访问Vue实例数据，组件是一个单独的模块的封装，这个组件有属于自己的HTML模板，也有自己的数据data

- 第一步创建组件构造器

	```html
	const componentName = Vue.extend({
		template:``
	})
	```

- 第二步注册组件

	- 全局组件（可以在多个Vue实例中使用）

		```html
		Vue.component('mycpn(调用时的组件名)',componentName)
		```

	- 局部组件

		```html
		const app = new Vue({
			el: '#app',
			data: {
				message:'i love code'
			},
			components: {
				mycpn:cpn
			},
		})
		```

- 第三步使用组件

	```html
	<mycpn></mycpn>
	```

- 父子组件

	```html
	const cpn1（子组件，只能在cpn2中使用）=Vue.extend({
		template:`
	        <div>
	            <h2>我是测试1</h2>
	            <p>我是小测试1</p>
	            <p>我是小测试1</p>
	        </div>`
	})
	const cpn2(父组件)=Vue.extend({
		template:`
			<div>
	    		<h2>我是测试2</h2>
	   	 		<p>我是小测试2</p>
	    		<p>我是小测试2</p>
	    		<cpn1></cpn1>
			</div>
		`,
		components:{
			cpn1:cpn1
		}
	})
	```

- 语法糖

	- 全局组件

	```html
	Vue.component('cpn3',{
	    template:`
	        <div>
	            <h2>我是测试3</h2>
	            <p>我是小测试3</p>
	            <p>我是小测试3</p>
	        </div>`
	})
	```

	- 局部组件

	```html
	const app = new Vue({
	    el: '#app',
	    data: {
	    	message:'i love code'
	    },
	    components:{
	        cpn1:{
	            template:`
	            <div>
	                <h2>我是测试1</h2>
	                <p>我是小测试1</p>
	                <p>我是小测试1</p>
	            </div>`
	        }
	    } 
	})
	```

	```html
	可以将template中的内容放在一个template标签中，然后在注册组件时通过id调用
	<template id="cpn" name="component-name">
	    <div>
	      <h2>{{cmovies}}</h2>
	      <ul>
	        <li v-for="item in cmovies" >{{item}}</li>
	      </ul>
	      <p>{{cmessage}}</p>
	    </div>
	</template>
	const app = new Vue({
	    el: '#app',
	    data: {
	        message:'i love code',
	    },
	    components: {
	        cpn:{
	          template:'#cpn',
	        }
		}
	}
	
	```
	
	

#### 父子组件的通信

- 子组件中无法引用父组件或者vue实例的数据的，但是在开发中有一些数据需要从上层传递到下层，比如我么请求了很多数据，其中一部分大组件使用，有些则需要子组件进行展示，所以就需要父组件把这些数据传递给小组件

- **通过props向子组件传递数据**

	- ```javascript
		props: {
		    // 方法1.限制数据的属性
		    cmovies:Array,
		
		    //方法2.限制数据的属性（type）和默认值（default），以及是否必须（required）
		    cmessage: {
		        type: String,
		        default: 'aaa',
		        required:true
		    },
		    cmovies:{
		        type:Array,
		        default:[]
		    }
		}
		```

- **通过事件向父组件发送消息**

	- ```html
		在子组件中，通过$emit()来触发事件，
		    //发出事件
		    this.$emit('itemclick',item)
		在父组件中，通过v-on来监听子组件事件。
		<cpn @itemclick="cpnclick"></cpn>
		```

### 父子组件的访问方式：

- 有时候我们需要直接访问而不是通过传数据

	- 父组件访问子组件：使用$children或者$refs

	- ```javascript
		//$children获取的是一个数组，它包含了所有的子组件
		this.$children[0].showmessage();
		console.log(this.$children[0].name);   
		//$refs=>是对象类型，默认是一个空对象,需要在自定义的标签上添加ref="aaa"
		<cpn ref="aaa"></cpn>
		、、、、、
		this.$refs.aaa
		```

	- 子组件访问父组件：是用$parent

	- ```javascript
		//访问父组件
		this.$parent
		//访问根组件
		this.$root
		```

### slot插槽

- 组件的插槽让我们封装的组件更具有扩展性，让使用者决定组件内部的一些内容到底展示什么，如果在自定义标签中有多个值，那么插槽会全部接受，一起作为替换元素

	- ```html
		<cpn><button>按钮</button></cpn>
		<template id="cpn" name="component-name">
		    <div>
		      <h2>我是组件</h2>
		      <p>我是p标签</p>
		      <slot></slot>
		    </div>
		</template>
		```

- 插槽中也可以有一个默认值

	- ```html
		<slot><button>按钮</button></slot>
		```

- 具名插槽

	- ```html
		<div id="app">
		    <cpn><button slot="left">将左边替换为按钮</button></cpn>
		</div>
		<template id="cpn" name="component-name">
		    <div>
		      <slot name="left"><span>左边</span></slot>
		      <slot name="center"><span>中间</span></slot>
		      <slot name="right"><span>右边</span></slot>
		      <slot>hahahh </slot>
		    </div>
		</template>
		```

### 编译作用域

- 父组件模板的所有东西都会在父级作用域内编译，子组件模板的所有东西都会在子级作用域内编译

- ```html
	<div id="app">
	    <cpn v-show="isshow"></cpn>
	  </div>
	  <template id="cpn" name="component-name">
	    <div>
	      <h2>我是谁</h2>
	    </div>
	  </template>
	  <script src="js/vue.js"></script>
	  <script>
	    const app = new Vue({
	      el: '#app',
	      data: {
	        message:'i love code'
	      },
	      data:{
	        isshow:true
	      },
	      components: {
	        cpn:{
	          template:'#cpn',
	          data() {
	            return {
	              isshow: false
	            }
	          },
	        }
	      },
	    })
	</script>
	```

### 作用域插槽

- 由子组件提供内容，让父组件选择标签来展示

	- ```html
		子组件中slot的属性  :dataname(随意取名)="(要传给父组件的数据)"
		<template id="cpn" name="component-name">
		    <div>
		      <slot :dataname="pLanguages">
		          <ul>
		              <li v-for="item in pLanguages">{{item}}</li>
		          </ul>
		      </slot>
		    </div>
		</template>
		在父组件中通过 slot-scope="(在父组件中使用的变量名)"获取到子组件传递的数据
		<div slot-scope="slotname">
			<span v-for="item in slotname.dataname" >{{item}}-</span>
		</div>
		```

### vue-cli2

- 安装`npm install -g @vue/cli`，拉取旧版本`npm install -g @vue/cli-init`

- 创建一个项目

	- `vue init webpack hello-world`

	- 接下来就是输入

	- ```
	项目名称
		project name
		项目简介
		project description
		作者
		author
		选择vue的模式
		vue build
		安装vue路由
		install vue-router
		使用esLint规范代码
		use eslint to lint your code
		选择使用的代码规范
		pick an eslint preset
		是否使用单元测试
		set up unit tests
		安装nightwatch使用端到端测试
		setup e2e tests with nightwatch     
		使用npm或者yarn管理
		should we run 'npm install' for you after the project has been created?flat
		```

### vue-cli3

- 创建一个项目

	- `vue create hello-world`

	- ```
		#选择一个设置（默认还是手动）
		please pick a preset: 1.default 2.manually select features
		#选择一些你需要的项目（按空格选择或取消）
		#check the features needed for your project:
		babel
		typescript
		progressive web-app support  （先进的webapp）
		pouter
		vuex
		css pre-processors （css预处理器）
		linter / formatter
		unit testing
		e2e testing
		#where do you prefer placing config for babel,postcss,eslint,etc?(你打算把这些东西放在哪里？)
		in dedicated config files （在一个单独的config文件中）
		in package.json		(放在package.json中)
		#save this as a preset for future projects?（将刚才的选择保存，下次创建就不需要再选了）
		```



