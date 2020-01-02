### Node

- 什么是node？
	- 基于V8引擎（谷歌浏览器的引擎）渲染JS的工具或者环境
		- 安装node
		- 把JS代码放到node环境中执行
	
- node安装完成后
	
	<!--more-->
	
	- 当前电脑上自动安装了npm（node Package Manager）：一个JS模块（所有封装好的可以供其他人调取使用的都可以称之为模块或者包）管理的工具，基于npm可以安装下载JS模块
	- 他会生成一个node执行的命令（可以在dos窗口或者终端命令中执行）node xxx.js
	
- 如何在node中渲染和解析JS
	- REPL模式（read-Evaluate-Print-Loop，输入-求值-输出-循环）
	- 直接基于node来执行JS文件
	
- 之所以把node作为后台编程语言，是因为：
	- 我们可以把node安装在服务器上
	- 我们可以把编写的JS的代码放到服务器上，通过node来执行它（我们可以使用JS来操作服务器，换句话说，使用js来实现服务器端的一些功能操作）
	
- node做后台的优势和特点
	- 传统后台语言：JAVA/Python/PHP/C#......
	- 单线程的
	- 基于V8引擎渲染：快
	- 异步无阻塞的I/O操作：I/O对文件的读写
	- event-driven事件驱动：类似于发布定于或者回调函数



Node给JS提供了很多的内置属性和方法，例如：http、fs、url、path、等对象中都提供了很多API供JS操作。

前端（浏览器运行JS）是限制I/O操作的	

​		Input type=‘file’ 这种算是 I/O 操作，但是需要用户手动选择（而且还仅仅是一个读取不是写入）

node中运行JS是不需要限制 I/O 操作的

-----------

**npm的应用**

​	目前“工程化/自动化”开发（）不一定写后台，都是基于node环境，基于npm管理模块，基于webpack实现模块之间的依赖打包，部署上线等

```
npm install xxx 把模块安装到当前目录
npm install xxx -g 把模块安装在全局目录下
npm uninstall xxx / npm uninstall xxx -g 卸载模块
npm install xxx@xxx  限制安装版本
npm view xxx> xxx.version.txt 查看模块的历史版本
```

- 切换安装源

	- 淘宝镜像

		- 安装cnpm

		- ```
			npm install cnpm -g
			cnpm install zepto
			```

		- 安装nrm切源工具，基于nrm把源切换到淘宝源上

		- ```
			npm install nrm -g
			nrm ls 查看当前可以使用的源
			nrm use xxx 使用某个源
			这样处理完成后，后期模块的管理依然是基于npm即可
			```

	- 基于yarn安装，他也是模块管理工具，类似于npm，但是安装管理的速度比npm快很多

		- ```
			npm install yarn -g
			yarn add xxx
			yarn remove xxx
			使用yarn只能把模块安装到当前目录下，不能安装到全局环境下
			```
	
	- bower也是类似的npm的包管理器，只不过他是从github上下载安装
	
		- ```
			npm install bower -g
			bower install xxx
			```



- 在本地项目中基于npm/yarn安装第三方模块
	- 第一步：在本地项目中创建一个“package.json”的文件，用于把当前项目所有依赖的第三方模块信息（包含：模块名称以及版本号等信息）都记录下来，可以在这里配置一些可执行的命令脚本等。
	- 第二步：安装
	- 第三步：部署的时候“跑环境”
		- 不需要自己一个一个的安装，只需要执行npm install或者yarn install即可，npm会自己先检测目录中是否有package.json文件，如果有的话，会按照文件的配置清单依次安装
- 安装在本地和全局的区别
	- [安装在全局的特点]  
		- 所有项目都可以使用这个模块
			- 容易导致版本冲突
			- 安装在全局的模块，不能基于commonJS模范规范调取使用
			- 可以使用命令操作 
	- [安装在本地的特点]
		- 只能当前项目使用这个模块
			- 不能直接使用命令操作

**为什么在全局下可以使用命令？**

​		npm root  / -g  查看本地项目或者全局环境下，npm的安装目录

​		安装在全局目录下的模块，但部分都会生成一个xxx.cmd的文件，只要有这个文件，那么xxx就是一个可执行的命令（例如：yarn.cmd=>yarn就是一个可执行命令）

**能否既安装在本地也可以命令操作？**

​		可以但是需要配置package.json中的script

​				1.把模块安装在本地，如果支持命令操作的（会在node_modules的bin中生成xx.cmd的命令文件，只不过这个文件无法在全局下执行=>不能直接使用命令）

​				2.在package.json的script中配置需要执行的命令脚本

```
"scripts":{
	"hlx":"lessc -v"//属性名自己设置，属性值是需要执行的命令脚本，根据自己的需要编写
}
```

​				3.npm run hlx / yarn hlx 这样的操作就是把配置的脚本执行

​					->首先到配置清单的scripts中查找

​					->找到把后面对应的属性值（执行脚本）执行

​					->执行脚本的时候，会到本地node_modules中的bin文件夹下查找，如果没有的话，再向npm根目录下查找

**node入门**

- node本身是基于CommonJs模块规范设计的。
	- 内置模块：Node天生提供给JS使用的
	- 第三方模块：别人写好的，我们可以基于NPM安装使用
	- 自定义模块：自己创建的一些模块

- CommonJS模块设计的思想（AMD/CMD/ES6 module都是模块设计思想）

	- CommonJS规定，每一个JS都是一个单独的模块（模块是私有的：里面涉及的值和变量以及函数都是私有的，和其他JS文件中的内容是不冲突的）

	- CommonJS中允许模块中的方法互相调用（B模块中想要调取A模块中的方法，A导出，B导入）

		- 导出：CommonJS给每一个模块（每个JS）中都设置了内置的变量、属性、方法
			- module：代表当前这个模块对象[object]
			- module.exports:模块的这个"属性"是用来导出属性方法的[object]
			- exports：是内置的一个“变量”，也是用来导出当前模块属性方法，虽然和module.exports不是一个东西，但是对应的值是同一个（module.exports=exports值都是对象）

		- 导入：
			- require：CommonJS提供的内置变量，用来导入模块的（其实导入的就是module.exports暴露出来的东西）：导入的值也是[object]

	temp1.js

	```javascript
	let a=12,
	    fn=b=>{
	        return a*b;
	    };
	exports.fn=fn;//把当前模块私有的函数放到exports导出对象中（赋值给它的某一个属性），这样在其他模块中，可以基于require导入进来使用 module.exports.fn=fn;
	//exports={}; 重新定向到自己的堆内存，用来实现导出，是无法导出内容的：默认exports和module.exports是同一个堆内存，但是这种操作让exports指向一个新的堆内存，而module.exports不受影响（require导入的是module.exports对应的堆内存，而不是exports的）
	```

	temp2.js

	```javascript
	let a=13,
	    fn=b=>{
	        return a/b;
	    };
	let temp1 =require('./temp1');//（.js可以忽略）require导入时：首先把temp1模块中的JS代码自上而下执行，把exports对应的堆内存导入进来，所以接收到的结果是一个对象（require是一个同步操作：只有把导入的模块代码执行完成，才可以获取值，然后继续执行本模块下面的代码）
	```

**CommonJS模块的特点**

- 所有代码都运行在模块作用域下，不会污染全局作用域
- 模块可以多次加载，但是只会在第一次加载时运行一次，然后运行结果就被缓存了，以后再加载，就直接读取缓存中的结果，要想让模块再次运行，必须清除缓存
- 模块加载的顺序按照其在代码中出现的顺序
- CommonJS规范加载模块是同步的，也就是说，只有加载完成，才能执行后面的操作

**node中的内置模块**

- **fs的内置模块：实现I/O操作**

	- let fs=require('fs');

		- 1.fs.mkdir / fs.mkdirSync：创建文件夹，有Sync是同步创建，没有是异步，想要实现无阻塞操作，一般都使用异步操作完成要处理的事

			```javascript
			//let result =fs.mkdirSync('./less');  //同步
			let fs=require('fs');
			fs.mkdir('./less',err=>{				//异步
			    if(err){
			        console.log(err);
			        return;
			    }
			});
			console.log(1);
			```

			

		- 2.fs.readdir / fs.readdirSync ：读取文件操作

			```javascript
			//let result =fs.readdirSync('./');  //同步
			let fs=require('fs');
			fs.readdir('./',(err,result)=>{		//异步
			    if(err){
			        console.log(err);
			        return;
			    }
			    console.log(result);//返回的结果是一个数组
			});
			```

		- 3.fs.rmdir / fs.rmdirSync：删除文件夹（文件夹必须为空）

			```javascript
			let fs=require('fs');
			fs.rmdir('./less',err=>{
			    if(err){
			        console.log(err);
			        return;
			    }
			});
			```

		- 4.fs.readFile：读取文件中的内容

			```javascript
			let fs=require('fs');
			fs.readFile('./less/1.less','utf-8',(err,result)=>{
			    //不设置UTF-8编码模式，读取出来的是buffer格式的数据，设置后读取到的是字符串格式的数据
			    if(err){
			        console.log(err);
			        return;
			    }
			    console.log(result);
			});
			```

		- 5.fs.writeFile：向文件中写入内容（覆盖写入：写入的新内容会替换原有的内容）

			```javascript
			let fs=require('fs');
			fs.writeFile('./less/1.less','hahahha','utf-8',(err)=>{
			    if(err){
			        console.log(err);
			        return;
			    }
			    console.log('ok');
			});
			```

		- 6.fs.appendFile：追加写入新的内容，原有的内容还在

			```javascript
			let fs=require('fs');
			fs.appendFile('./less/1.less','hahahha','utf-8',(err)=>{
			    if(err){
			        console.log(err);
			        return;
			    }
			    console.log('ok');
			});
			```

		- 7.fs.copyFile：拷贝文件到新的位置

			```javascript
			let fs=require('fs');
			fs.copyFile('./1.js'(目标文件),'./less/11.js'（目的地以及文件名）,(err)=>{
			    if(err){
			        console.log(err);
			        return;
			    }
			    console.log('ok');
			});
			```

		- 8.fs.unlink：删除文件

			```javascript
			let fs=require('fs');
			fs.unlink('./less/1.less',(err)=>{
			    if(err){
			        console.log(err);
			        return;
			    }
			    console.log('ok');
			});
			```


**URL内置模块**

- url.parse(url,[flag])：把一个url地址进行解析，把地址中的每一部分按照对象键值对的方式存储起来。第二个参数是false，设置为true可以把问号传参的部分也解析成为对象键值对的方式

- ```javascript
	let url = require('url');
	//不加true
	var no1 = url.parse('http://www.baidu.com/main/guide/index.html?from=qq&lx=stu#video');
	console.log(no1);
	/* Url {
	  protocol: 'http:', 				=>协议
	  slashes: true,					=>是否有双斜线
	  auth: null,						=>作者
	  host: 'www.baidu.com',			=>域名+端口
	  port: null,						=>端口
	  hostname: 'www.baidu.com',		=>域名
	  hash: '#video',					=>哈希值
	  search: '?from=qq&lx=stu',		=>问号传参
	  query: 'from=qq&lx=stu',			=>问号传递的参数，不包含问号
	  pathname: '/main/guide/index.html',=>请求资源的路径名称
	  path: '/main/guide/index.html?from=qq&lx=stu',
	  href: 'http://www.baidu.com/main/guide/index.html?from=qq&lx=stu#video'
	} */
	//加true
	var no1 = url.parse('http://www.baidu.com/main/guide/index.html?from=qq&lx=stu#video',true);
	/*
	query: [Object: null prototype] { from: 'qq', lx: 'stu' },加和不加的区别就在于query中
	*/
	```

**HTTP内置模块**

```javascript
let server = http.createServer();	//创建服务
server.listen();					//监听窗口
```

注意：基于node创建后台程序，我们一般都会创建一个server模块，在模块中实现创建web服务，和对于请求的处理（并且我们一般都会把server模块放到当前项目的根目录下）

简单的监听应用

```javascript
let http =require('http'),
    url = require('url'),
    path=require('path'),
    fs=require('fs');
let port=8686; 		//监听8686端口
let handle=function handle(req,res){
    //req：request请求对象，包含了客户端请求的信息
    //req.url存储的是
    //req.method 客户端请求的方式
    //res:reponse 响应对象，包含了一些属性和方法，可以让服务器端返回内容
   	//res.write 基于这个方法，服务器端可以向客户端返回内容
    //res.end 结束响应
    //res.writeHead 重写响应头信息
    let {url,method}=req;
    console.log(url,method);
    res.writeHead(200,{'content-type':'text/plain;charset=utf-8;'});
    res.end(JSON.stringify({name:'哈哈哈'}));//服务器端返回给客户端的内容一般是string或者buffer格式的数据
};
http.createServer(handle).listen(port,()=>{
    console.log(`server is success，listen on ${port}!`);
});
```

服务器上有一堆代码，这堆项目代码中既可能有服务器端的程序代码，也可能有客户端的程序代码 ，而客户端程序代码我们一般都放到static这个文件夹中。

```javascript
static
	都是服务器端需要返还给客户端，由客户端浏览器渲染和解析的（前端项目：包括页面，CSS，JS，图片等）
server.js
	都是需要在服务器端基于node执行的（后端项目：一般只有JS）
```

我们创建的WEB服务需要处理两类请求：

- 静态资源文件的请求处理：想要文件

- API接口的请求处理：想要数据

	区别：第一类请求的地址中有后缀名，第二类没有后缀   



**NODE中独有的异步操作API**

- sestImmediate它也是定时器，但是它不设置时间，但是它也是异步编程（宏任务)

	```javascript
	setImmediate(()=>{	
	
	},10);
	```

- process.nextTick：把当前任务放到主栈的最后执行（当主栈执行完，先执行nextTick，再到等待队列中）

	```javascript
	process.nextTick(()=>{
	});
	```

- process.env.NODE_ENV ：全局环境变量

	- 用途：真实项目中，我们项目基于webpack打包配置的时候，往往需要区分不同环境下的不同操作，例如有 开发环境，测试环境，生产环境....而我们一般都是基于环境变量来区分打包配置的！

### Express：node.js web应用框架

```javascript
let express=require('express'),
    app=express(),
    port=8686;

//创建服务和监听端口两件事都处理了,并且有请求过来执行的是app这个方法
app.listen(port,()=>{
    console.log(`sever is success,listen on ${port}!`);
});

//静态资源文件处理
app.use(express.static('./static'));

//API处理
app.get('/getUser',(req,res)=>{
    res.send({
        /*
         *当客户端向服务器发送请求,如果请求方式是GET，请求路径是'/getUser',就会把回调函数触发执行，里面有三个参数req/res/next
         *REQ:request（他不是我们之前原生node中的req，他是espress框架封装处理的，但是也是存储了很多客户端传递信息的对象）
         *	req.params 存储的是路径参数信息
         * 	req.path 请求路劲的名称
         *  req.query 请求的问号参数的信息（get请求都是这样传递信息的）（对象）
         *	req.body 请求的方式是post，我们基于body-parser中间件处理后，会把客户端请求主体中传递的内容存放到body属性上
         * 	req.session 当我们基于express-session中间件处理后，会把session操作放到这个属性上，基于这个属性可以操作session信息
         * 	req.cookies 当我们基于cookie-parser中间件处理后，会把客户端传递的cookie信息存放到这个属性上
         *	req.get() 获取指定请求头的信息
         *	req.param() 基于这个方法可以把url-encoded格式字符串（或者路径参数）中的某一个属性名对应的信息获取到
         *  req.response 也不是原生中的res，也是经过express封装处理的，目的是为了提供一些属性和方法，可以供服务器端向客户端返回内容
         *	res.cookie() 通过此方法可以设置一些cookie信息，通过响应头set-cookie返回给客户端，客户端把返回的cookie信息种到本地
         *	res.type() 设置响应内容的MIME类型
         *	res.status() 设置响应状态码
         *	res.send-status() 设置返回的状态码
         * 	res.json() 向客户端返回json格式的字符串，允许我们传递json对象，方法会帮我们转换为字符串然后返回（执行此方法后会自动结束响应，也就是自动执行res.end）
         *	res.send-file（[path]） 首先把path指定的文件夹中内容得到，然后把内容返回给客户端浏览器（完成了文件的读取和响应两步操作），也会自动结束响应
         * 	res.send（） 自己设置返回的东西，也会自动结束响应
         *	res.redirect（）响应是冲定向的（状态码302）
         *	res.render() 服务器渲染的时候才会使用
        */
        message:'ok'
    });
});

app.post('/register',(req,res) =>{
    //get请求，接收问号传参的信息，可以使用：req.query/req.param()
    //post请求，接收请求主体传递的信息，此时我们需要使用一个中间件（body-parser）
})

```

