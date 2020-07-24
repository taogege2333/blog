### 一、函数中this指向问题
1. 函数中的this指向在函数调用时确定
```js
function a() {
  return this;
}
var b = {name: 'b', a: a};
var c = {name: 'c', a: a};
console.log(b.a().name); // b
console.log(c.a().name); // c
```
2. 修改函数this指向的方法：call, apply, bind
```js
var a = {
  name: 'a',
  fn: function () {
    console.log(this.name);
  }
}
var b = {name: 'b'};
a.fn(); // a
a.fn.call(b); // b
a.fn.apply(b); // b
a.fn.bind(b)(); // b
``` 
区别：它们的第一个参数都是修改后this指向的对象
- call：从第二个参数开始，向函数传参，参数必须一个一个传，之后立即执行
- apply：第二个参数为函数的arguments，之后立即执行
- bind：从第二个参数开始，向函数传参，参数必须一个一个传，不会立即执行，而是返回一个指定this指向的新函数
### 二、函数中变量使用问题
函数中的变量是在声名时确定的
```js
var a = 100;
function b() {
  var a = 200;
  return function () {
    console.log(a);
  }
}
var fn = b();
fn(); // 200
```
