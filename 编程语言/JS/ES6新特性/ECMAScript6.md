## ECMAScript6
### 参考链接 廖雪峰老师写的 [《ECMAScript6入门》](https://es6.ruanyifeng.com/#docs/intro)
### 历史：这里就不过多赘述，可以了解的是ECMAScript 和 JavaScript 的关系是，前者后者的规格，后者是前者的一种实现（另外的 ECMAScript 方言还有 JScript ActionScript）。日常场合，这两个词是可以互换的。

---

### Babel 转码器
Babel 是一个广泛使用的 ES6 转码器，可以将 ES6 代码转为 ES5 代码，从而在现有环境执行。这意味着，你可以用 ES6 的方式编写程序，又不用担心现有环境是否支持。下面是一个例子。
```
// 转码前
input.map(item => item + 1);

// 转码后
input.map(function (item) {
  return item + 1;
});
```
#### 配置文件.babelrc
Babel 的配置文件是.babelrc，存放在项目的根目录下。使用 Babel 的第一步，就是配置这个文件。
```
 {
    "presets": [
      "@babel/env",
      "@babel/preset-react"
    ],
    "plugins": []
  }
```  

### @babel/polyfill
Babel 默认只转换新的 JavaScript 句法（syntax），而不转换新的 API，比如`Iterator`、`Generator`、`Set`、`Map`、`Proxy`、`Reflect`、`Symbol`、`Promise`等全局对象，以及一些定义在全局对象上的方法（比如Object.assign）都不会转码。

举例来说，ES6 在Array对象上新增了Array.from方法。Babel 就不会转码这个方法。如果想让这个方法运行，必须使用babel-polyfill，为当前环境提供一个垫片。

安装命令如下。
```
$ npm install --save-dev @babel/polyfill
```
然后，在脚本头部，加入如下一行代码。
```
import '@babel/polyfill';
// 或者
require('@babel/polyfill');
```