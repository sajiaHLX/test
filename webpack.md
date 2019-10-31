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
		    filename:'bundle.js'
		  },
		  module:{
		    rules:[{
		      test:/\.css$/,
		        //从右向左读取loader
		      use:['style-loader','css-loader']
		    }]
		  }
		}
		```

- **webpack中配置Vue**

- **plugin的使用**

- **搭建本地服务器**

	