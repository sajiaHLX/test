### webpack

- **认识webpack**
	- 从本质上来说，webpack是一个现代JavaScript应用的静态模块打包工具
	- 和grunt/gulp的对比
		- grunt和gulp的核心是task
		- 我们可以配置一系列的task，并且定义task要处理的事务（例如es、6ts转化、图片压缩、scss转成css）
		- 之后让grunt/gulp来依次执行这些task，而且让整个流程自动化
		- 所以grunt/gulp也被称为前端自动化任务管理工具
		- 只需要进行简单的合并，压缩，就使用grunt/gulp即可
	- webpack更加强调模块化开发管理，而文件压缩合并，预处理等功能，是他附带的功能
	
- **webpack的安装**

	- npm install webpack

- **webpack的起步**

	- webpack ./src/index.js ./dist/bundle.js

- **webpack的配置**

	- 新建webpack.config.js文件

	- ```javascript
		const path=require('path')
		
		module.exports={
		  entry:'./src/index.js',
		  output:{
		    path:path.resolve(__dirname,'dist'),
		    filename:'bundle.js'
		  },
		}
		```

- **loader的使用**

  - 不同类型的文件需要加载不同的loader，

  - 需要在webpack.config.js文件中配置

  - ```javascript
  	const path=require('path')
  	
  	module.exports={
  	  entry:'./src/index.js',
  	  output:{
  	    path:path.resolve(__dirname,'dist'),
  	    filename:'bundle.js',
  	    publicPath:'dist/'
  	  },
  	  module:{
  	    rules:[
  	        //css打包需要的
  	      {
  	        test:/\.css$/,
  	        use:['style-loader','css-loader']
  	      },
  	        //less打包需要的
  	      {
  	        test:/\.less$/,
  	        use:[
  	          {loader:"style-loader"},
  	          {loader:"css-loader"},
  	          {loader:"less-loader"}
  	        ]
  	      },
  	        //图片打包需要的loadernpm 
  	      {
  	        test: /\.(png|jpg|gif|jpeg)$/,
  	        use: [
  	          {
  	            loader: 'url-loader',
  	            options: {
  	              limit: 8192
  	            }
  	          }
  	        ]
  	      }
  	    ]
  	  }
  	}
  	```

- **webpack中配置Vue**

	- ```javascript
		npm install vue --save
		npm install --save-dev vue-loader vue-template-comiler
		```

	- 同时webpack.config.js中也需要配置

	- ```javascript
		module:{
			rules:[
		    	{
		        	test:/\.vue$/,
		        	use:{
		        	  loader : 'vue-loader'
		        	}
		      	}
		    ]
		},
		resolve:{
		    //alias别名
		    alias:{
		      'vue$':'vue/dist/vue.esm.js'
		    }
		}
		```

	- App.vue文件中

	- ```vue
		<template>
		  <div id="app">
		    <h2 class="class">{{message}}</h2>
		      {{message}}
		      <Cpn></Cpn>
		      <button @click="btnclick">按钮</button>
		  </div>
		</template>
		
		<script>
		export default {
		  name:'App'
		  data () {
		    return {
		      message: 'hello webpack'
		    }
		  },
		  methods: {
		    btnclick() {
		      console.log("i am hlx");
		    },
		  }
		}
		
		</script>
		<style scoped>
		  .class{
		    color: antiquewhite
		  }
		</style>
		```

	- 在index.js文件中

	- ```javascript
		import Vue from 'vue'
		import App from './vue/App.vue'
		new Vue({
		  el:'#app',
		  template:`<App></App>`,
		  components:{
		    App
		  }
		})
		```

- **plugin的使用**

  - plugin是插件的意思，通常是用于对某个现有的架构进行扩展

  - ```javascript
  	const path=require('path')
  	//添加注释需要用的
  	const webpack=require('webpack')
  	//打包HTML需要用的
  	const HtmlWebpackPlugin=require('html-webpack-plugin')
  	//压缩js代码需要的
  	const UglifyjsWebpackPlugin=require('uglifyjs-webpack-plugin')
  	
  	module.exports={
  		entry:'./src/index.js',
  	    output:{
  	        path:path.resolve(__dirname,'dist'),
  	        filename:'bundle.js',
  	    },
  	    module:{
  	        rules:[
  	        	{
  	                test:/\.css$/,
  	                use:['style-loader','css-loader']
  	            },
  	        ]
  	    },
  	    plugins:[
  	        //添加注释
  	        new webpack.BannerPlugin({
  	            banner:'made by XXX'
  	        }),
  	        //打包html文件
  	        new HtmlWebpackPlugin(),
  	        new UglifyjsWebpackPlugin()
  	    ]
  	}
  	```

- **搭建本地服务器**

	- 方便测试，实现实时刷新页面

	- `npm install --save-dev webpack-dev-server`

	- devserver也是作为webpack中的一个选项，选项本身有如下属性：

		- contentBase：为哪一个文件夹提供本地服务，默认是根文件夹
		- port：端口号
		- inline：页面 实时刷新
		- historyApiFallback：在spa页面中，依赖HTML5的history模式

	- 如果没有全局安装还需要配置package.json中的script脚本，添加执行的命令

		- ```javascript
			"scripts": {
			    "dev": "webpack-dev-server --open --config ./build/dev.config.js(该地址为需要执行的文件的地址)"
			},
			```

