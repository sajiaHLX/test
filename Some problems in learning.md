浏览器中报icon的错，在head中加入如下语句即可：

<link rel="shortcut icon" href="#" />

跨域问题在服务器的app.js文件中加上

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

