**浏览器中报icon的错（就是没有找到网站的小图标），在head中加入如下语句即可：**

- <link rel="shortcut icon" href="#" />

**跨域问题在服务器的app.js文件中加上**

```javascript
var allowCrossDomain = function(req, res, next) {
  res.header('Access-Control-Allow-Origin', '*');//允许跨域的地址，此处*代表都可以
  res.header('Access-Control-Allow-Methods', 'GET,PUT,POST,DELETE');
  res.header('Access-Control-Allow-Headers', 'Content-Type');
  res.header('Access-Control-Allow-Credentials','true');
  next();
};
app.use(allowCrossDomain);
```

<!--more-->

**哪些元素不支持伪元素：**

- text ，submit ，button ， textarea ， select ， img ， iframe

**vuecli3设置代理**

- 在vue.config.js中添加

- ```javascript
	devServer: {
	    proxy: {
	      '/api': {
	        target: 'http://localhost:3000',
	        changeOrigin: true,
	        ws: true,
	        pathRewrite: {
	          '^/api': ''
	        }
	      }
	    }
	  }
	```