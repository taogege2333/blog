```javascript
// a.js
export const name = 'xiaoming'
export function log(value) { console.log(value) }
export default 'A'

// b.js
export const name = 'xiaoming'
export function log(value) { console.log(value) }
export default 'A'

// c.js
// 将a、b两个模块在c模块中导出，不包含default，导出的a、b模块中重名的变量或方法将会被省略
export * from 'a.js'
export * from 'a.js'
// 导出a、b模块的default
export { default as a } from 'a.js'
export { default as b } from 'a.js'
// 将重名的变量或方法重命名，才会被导出
export * from 'a.js'
export { name as name2, log as log2 } from 'b.js'
// 若重名，但是在c中明确过，则会导出确认过的
// 以下将会导出b模块的name，而a模块的name将会省略
export * from 'a.js'
export { name } from 'b.js'
```

