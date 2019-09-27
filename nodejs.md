### Node

- 什么是node？
	- 基于V8引擎（谷歌浏览器的引擎）渲染JS的工具或者环境
		- 安装node
		- 把JS代码放到node环境中执行
- node安装完成后
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

