### 一、节流
限制频繁操作的执行频率
```js
function throttle(fn, delay) {
  var timer = null;
  return function () {
    if(timer) {
      return;
    }
    timer = setTimeout(() => {
      fn.apply(this, arguments);
      timer = null;
    }, delay)
  }
}
```
### 二、防抖
解决由于频繁操作而频繁发送请求的问题，当操作结束后一定时间再发送请求
```js
function debounce(fn, delay) {
  var timer = null;
  return function () {
    if(timer) {
      clearTimeout(timer);
    }
    timer = setTimeout(() => {
      fn.apply(this, arguments);
      timer = null;
    }, delay)
  }
}
```