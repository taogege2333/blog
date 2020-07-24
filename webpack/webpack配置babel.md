1. 执行`npm i -D babel-loader @babel/core`安装babel-loader和@babel/core，然后在webpack.config.js中配置loader，将webpack与babel连接起来。
```
module: {
  rules: {
    {
      test: /\.js$/,
      exclude: "node_modules", //不包括node_modules文件
      loader: "babel-loader",
    }
  }
}
```
2. 以上只是配置了babel，但并未做任何事情，执行`npm i -D @babel/preset-env`安装@babel/preset-env，进行转换，配置方式如下：
- 在根目录创建.babelrc文件，在文件中添加内容
```
{
  "presets": ["@babel/preset-env"]
}
```
3. 以上配置仅仅转换了es2015+的语法，并没有定义新增的api，需要执行`npm i -s @babel/polyfill`安装@babel/polyfill，然后在需要转换的文件中添加`import "@babel/polyfill";`来引入新增的api。

4. 以上配置会将所有的新增特性api全部添加，会使打包后的文件变得很大，多出很多我们不需要的东西。在.babelrc文件中添加配置
```
{
  "presets": [
    ["@babel/preset-env", {useBuiltIns: "usage"}]
  ]
}
```
然后babel只会添加我们使用到的特性。