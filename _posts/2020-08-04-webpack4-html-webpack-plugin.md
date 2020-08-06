---
layout: post
title: webpack4 之html-webpack-plugin
date: 2020-08-04 12:31:30
categories: webpack4
tags:
---
# webpack4 之html-webpack-plugin
- 为html文件中引入的外部资源如script、link动态添加每次compile后的hash，防止引用缓存的外部文件问题
- 可以生成创建html入口文件，比如单页面可以生成一个html文件入口，配置N个html-webpack-plugin可以生成N个页面入口

## title
生成html文件的标题

## filename
输出的html的文件名称

## template
html模板所在的文件路径
根据自己的指定的模板文件来生成特定的 html 文件。这里的模板类型可以是任意你喜欢的模板，可以是 html, jade, ejs, hbs, 等等，但是要注意的是，使用自定义的模板文件时，需要提前安装对应的 loader， 否则webpack不能正确解析。
如果你设置的 title 和 filename于模板中发生了冲突，那么以你的title 和 filename 的配置值为准。

## inject
注入选项。有四个选项值 true, body, head, false.
- true：默认值，script标签位于html文件的 body 底部
- body：script标签位于html文件的 body 底部（同 true）
- head：script 标签位于 head 标签内
- false：不插入生成的 js 文件，只是单纯的生成一个 html 文件

## favicon
给生成的 html 文件生成一个 favicon。属性值为 favicon 文件所在的路径名

## minify
minify 的作用是对 html 文件进行压缩，minify 的属性值是一个压缩选项或者 false 。默认值为false, 不对生成的 html 文件进行压缩。
```
plugins:[
        new HtmlWebpackPlugin({
//部分省略，具体看minify的配置
minify: {
     //是否对大小写敏感，默认false
    caseSensitive: true,
    
    //是否简写boolean格式的属性如：disabled="disabled" 简写为disabled  默认false
    collapseBooleanAttributes: true,
    
    //是否去除空格，默认false
    collapseWhitespace: true,
    
    //是否压缩html里的css（使用clean-css进行的压缩） 默认值false；
    minifyCSS: true,
    
    //是否压缩html里的js（使用uglify-js进行的压缩）
    minifyJS: true,
    
    //Prevents the escaping of the values of attributes
    preventAttributesEscaping: true,
    
    //是否移除属性的引号 默认false
    removeAttributeQuotes: true,
    
    //是否移除注释 默认false
    removeComments: true,
    
    //从脚本和样式删除的注释 默认false
    removeCommentsFromCDATA: true,
    
    //是否删除空属性，默认false
    removeEmptyAttributes: true,
    
    //  若开启此项，生成的html中没有 body 和 head，html也未闭合
    removeOptionalTags: false, 
    
    //删除多余的属性
    removeRedundantAttributes: true, 
    
    //删除script的类型属性，在h5下面script的type默认值：text/javascript 默认值false
    removeScriptTypeAttributes: true,
    
    //删除style的类型属性， type="text/css" 同上
    removeStyleLinkTypeAttributes: true,
    
    //使用短的文档类型，默认false
    useShortDoctype: true,
    }
    }),
]
```

## hash
hash选项的作用是 给生成的 js 文件一个独特的 hash 值，该 hash 值是该次 webpack 编译的 hash 值。默认值为 false
```
plugins: [
    new HtmlWebpackPlugin({
        hash: true
    })
]
```
## cache
默认是true的，表示内容变化的时候生成一个新的文件。

## showErrors
这个我们自运行项目的时候经常会用到，showErrors 的作用是，如果 webpack 编译出现错误，webpack会将错误信息包裹在一个 pre 标签内，属性的默认值为 true ，也就是显示错误信息。
开启这个，方便定位错误

## chunks
chunks主要用于多入口文件，当你有多个入口文件，那就回编译后生成多个打包后的文件，那么chunks 就能选择你要使用那些js文件

## excludeChunks
排除掉一些js
