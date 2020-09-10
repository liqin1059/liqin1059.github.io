---
layout: post
title: webpack提取页面公共资源
date: 2020-08-25 12:31:30
categories: webpack
tags:
- webpack
- SplitChunksPlugin
- 打包
- treeShaking
---

项目下面有很多页面，使用的基础库是一样的，同样的模块公共的部分重复打包浪费，如何基础包分离，页面之间公共包、公共模块的分离
<!-- more -->

# 基础库分离

## 将react、react-dom基础包通过cdn 引入，不打入bundle中

用html-webpack-externals-plugin

```javascript
const HtmlwebpackExternalsPlugin = require( 'html-webpack-externals-plugin');
plugins: [
  new HtmlwebpackExternalsPlugin({
    externals: [
      {
        module: 'react',
        entry: '//11.url.cn/now/lib/15.1.0/react-with-addons.min.js?_bid=3123'，
        global: 'React'
      },{
        module: 'react-dom',
        entry: '1/11.url.cn/now/lib/15.1.0/react-dom.min.js?_bid=3123',
        global: 'ReactDOM'
      }
    ]
  });
};
```

# 利用 SplitChunksPlugin进行公共脚本分离

Webpack4内置的，替代CommonsChunkPlugin插件

```javascript
module.exports = {
  optimization: {
    splitChunks: {
      chunks: 'async',
      minSize: 30000, // 抽离的包最小的大小
      maxSize: 0,
      minChunks: 1, // 设置最小引用次数
      maxAsyncRequests: 5,
      maxlnitialRequests: 3,
      automaticNameDelimiter: '~', // 浏览器请求异步资源的次数
      name: true,
      cacheGroups: {f
      vendors: {
      test:/[lW]node_modules[\V]/,
      priority: -10
    }
  }
};

```

## chunks参数说明

- asy异步引入的库进行分离(默认)
- initial同步引入的库进行分离
- all所有引入的库进行分离(推荐)

eg:分离react react dom

```javascript
module.exports = {
optimization: {
  splitChunks: {
    cacheGroups: {
      commons: {
        test: /(react|react-dom)/, // 匹配出需要分离的包
        name: 'vendors',
        chunks: 'all'
      }
    }
  }
};

```

# tree shaking(摇树优化)

## 概念

1个模块可能有多个方法，只要其中的某个方法使用到了，则整个文件都会被打至
bundle里面去，tree shaking 就是只把用到的方法打入bundle ，没用到的方法会在

## 使用

- webpack默认支持,在.babelrc里设置modules: false即可
- production mode的情况下默认开启

## 要求

必须是ES6的语法，CJS的方式不支持

## DCE(Elimination)

- 代码不会被执行，不可到达
- 代码执行的结果不会被用到
- 代码只会影响死变量(只写不读)

## Tree-shaking原理

利用ES6模块的特点:

- 只能作为模块顶层的语句出现
- import的模块名只能是字符串常量
- import binding是immutable的

代码擦除:uglify阶段删除无用代码

mode设置为none不开启，设置为production的时候默认开启

```javascript
module.exports = {
  entry: entry,
  mode: 'production'
}
```

# Scope Hoisting

现象:构建后的代码存在大量闭包代码

```javascript
ll a.js
export default 'xXXx';
ll b.js
import index from './a';
console.log(index);
```

## 问题

大量函数闭包包裹代码，导致体积增大（模块越多越明显)
运行代码时创建的函数作用域变多，内存开销变大

## 模块转换分析

### 模块

```javascript
import { helloworld } from './helloworld';
import '../../common';
document.write( helloworld());
```

### 模块初始化函数

```javascript
/* */
/***/(function(module，_webpack_exports_,_webpack_require_) {
"use strict";
_webpack_require_.r(_webpack_exports_);
harmony import */ var _common_WEBPACK_IMPORTED_MODULE_0_ =_webpack_require_(1);
/*harmony import*/ var _helloworld_WEBPACK_IMPORTED_MODULE_1_=_webpack_require_(2);
document.write(object(_helloworld_WEBPACK_IMPORTED_MODULE_1_["helloworld"])());
/***/})
```

### 结论

- 被webpack转换后的模块会带上一层包裹
- import会被转换成_webpack_require

## 分析webpack的模块机制

```javascript
(function( modules) {
  var installedModules = {};
function _webpack_require_(moduleId) {
  if (installedModules[moduleId])
    return installedModules[moduleId].exports;
    var module = installedModules[moduleId]= {
      i: moduleId,
      l: false,
      exports: {}
};
modules[moduleId].call(module.exports，module,module.exports, _webpack_require_);
module.l = true;
return module.exports;
}
_webpack_require__(e);
}([
*0 module * /
(function (module，_webpack_exports__,_webpack_require__) i
})，
* 1 module */
(function (module，_webpack_exports__，_webpack_require_) {
}),
* n module * /
(function (module，_webpack_exports__._webpack_require_) {
})
]);
```

### 分析

- m打包出来的是一个IIFE（匿名闭包)
- modules是一个数组，每一项是一个模块初始化函数
- m_webpack_require用来加载模块，返回module.exports
- m通过WEBPACK_REQUIRE_METHOD(O)启动程序

## scope hoisting原理

原理:将所有模块的代码按照引用顺序放在一个函数作用域里，然后适当的重命名一些变量以防止变量名冲突
对比:通过scope hoisting 可以减少函数声明代码和内存开销

- webpack mode为production默认开启
- 必须是ES6语法，CJS不支持

```javascript
module.exports = {
entry: {
  app: './src/app.js',
  search: './src/search.js'
),
output: {
  filename:'[name][chunkhash:8].js',
  path:_dirname +'/dist'
},
plugins: [
  new webpack.optimize.ModuleConcatenationPlugin() // webpack3
};
```


