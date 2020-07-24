![react生命周期](https://upload-images.jianshu.io/upload_images/19863207-59a5bad5020cf32a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* `componentWillMount` 组件将要挂载到页面之前
* `render` 数据发生变化，重新渲染页面
* `componentDidMount` 组件挂载结束时
* props发生改变时独有的生命周期函数：
  `componentReceiveProps` 子组件接收到父组件的props，并且父组件执行render后执行
* props或state发生改变时，执行的生命周期函数如下：
  1. `shouldComponentUpdate` return true || false    数据更新之前询问是否要更新，如果为false则不执行更新生命周期
  2. if (true) {
     `componentWillUpdate` 更新之前
     `render` 重新渲染页面
     `conponentDidUpdate` 更新结束
  }
* `componentWillUnmount` 组件被从页面删除之前执行
