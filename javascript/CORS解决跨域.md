[跨域资源共享 CORS 详解](http://www.ruanyifeng.com/blog/2016/04/cors.html)
1. nodejs配置响应头
```js
res.setHeader('Access-Control-Allow-Origin', req.headers.orgin);
```
2. CORS请求默认不发送cookie，要想发送cookie需要配置如下：
- node配置Access-Control-Allow-Credentials
 ```js
res.setHeader('Access-Control-Allow-Credentials', true);
```
- 原生ajax或axios配置，允许客户端（浏览器）发送cookie
```javascript
// 原生ajax
var xml = new XMLHttpRequest();
xml.withCredentials = true;
// axios
axios.defaults.withCredentials = true;
```
3. axios的post请求默认发送数据类型是`application/json`，会触发CORS的复杂请求，该请求会在发送post请求之前先发送一次options请求。
- 解决方案：将复杂请求转换为简单请求
```js
axios.defaults.headers['Content-Type'] = 'application/x-www-form-urlencoded';
```
>满足以下条件，即为简单请求
>1. 请求方法是以下三种方法之一：
>- HEAD
>- GET
>- POST
>2. HTTP的头信息不超出以下几种字段：
>- Accept
>- Accept-Language
>- Content-Language
>- Last-Event-ID
>- Content-Type：只限于三个值application/x-www-form-urlencoded、multipart/form-data、text/plain 