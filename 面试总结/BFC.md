1. BFC基本概念

- 块级格式化上下文

2. BFC的原理（即渲染规则）

- 同一BFC垂直方向上的边距会发生重叠

- BFC的区域不会与浮动元素box重叠
- BFC是一个独立的容器，外面的元素不会影响它里面的元素，里面的元素也不会影响外面的元素
- 计算BFC高度的时候浮动元素也会参与计算

3. 如何创建BFC

- float值不为none(默认)，只要当前元素浮动，那么就创建了一个BFC
- position值不为static(默认)和relative，那么就创建了一个BFC
- display设置为与table相关的值(即table、table-cell、table-row...)，那么就创建了一个BFC
- overflow值不为visible，即值为auto、hidden，那么就创建了一个BFC

4. 使用场景

- 解决子元素浮动，父元素高度塌陷问题
- 解决标准流盒子与浮动盒子的重叠问题
- 解决兄弟盒子垂直方向上外边距的重叠问题
