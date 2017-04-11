# Vue.js第一天

## vue课程介绍及项目演示
 - 课程目标：
  + 掌握Webpack的基本配置和使用，能够使用webpack提高开发效率；
  + 掌握vue的相关知识，能够在公司中运用vue快速进行产品开发；
  + React，RN；NG; vue

## 公司中项目的开发流程
 - 需求调研：开发价值、市场需求、产品定位、受众群体；【产出物：需求文档】
 - 产品设计：功能模块、流程逻辑；【产出物：设计文档，设计稿】，确定项目的基本功能；
 - 项目开发：项目架构、美工、前端、后台、测试【产品的把控】 500W 70%
 - 运营维护：上线试运行、调Bug、微调功能模块、产品迭代
 - 维护周期3年

> 根据需求做设计、根据设计搞开发
> 前端的主要工作职责：桥梁、所见即所得

## 技术选型
基于Webpack和vue.js，开发一套SPA应用；
+ 用到的vue技术
 - vue-resource -> 实现在Vue中获取后台数据
 - vue-router -> 基于vue-router实现页面之间的跳转
 - vue组件 -> VUE的基本用法
+ 用到的UI组件
 - Mint-UI 饿了么团队开源的vue组件
 - MUI 实实在在的HTML+CSS+JS实现的一套前端UI

## 基于webpack搭建项目结构
1. 搭建项目目录结构
2. 运行`npm init`初始化NPM包管理配置文件
3. 运行` cnpm i webpack --save-dev`安装webpack到项目开发依赖
4. 运行`cnpm i webpack-dev-server html-webpack-plugin --save-dev`
5. 在`package.json`中，新增script节点：`webpack-dev-server --hot --open --port 3002`，参数项可以挪到webpack的配置文件中，新增`devServer`节点
6. 运行`cnpm i style-loader css-loader sass-loader node-sass --save-dev`安装处理CSS相关的loader
7. 运行`cnpm i url-loader file-loader --save-dev`安装处理URL路径的相关loader
8. 运行`cnpm i babel-core babel-loader babel-preset-es2015 babel-preset-stage-0 babel-plugin-transform-runtime --save-dev`安装babel相关的loader，同时添加`.babelrc`文件，内容如下：
```
{
    "presets":["es2015", "stage-0"],
    "plugins":["transform-runtime"]
}
```
9. 运行`cnpm i vue --save`安装vue到项目依赖
10. 运行`cnpm i vue-loader vue-template-compiler --save-dev`，安装vue相关loader和编译工具到开发依赖项
11. 在loader配置项中，`exclude`表示，排除哪些文件；一般都排除`node_modules`文件夹

## vue.js中组件的基本结构
1. `<template></template>`注意事项：只能有一个根元素包裹，否则会报错
2. `<script></script>`注意事项
```
//必须使用export default导出一个一个对象，然后，这个对象内部，必须有一个data函数，函数内部，必须返回一个对象
export default{
    data(){
        return {}
    }
}
```

3. `<style></style>`注意事项：
```
scoped属性，表示当前vue组件的样式，只会应用到当前的组件结构中，并不会作用到其它组件上；假如没有这个scoped属性，那么，可能会造成一些样式冲突！
推荐大家都使用scoped属性，来划分样式表的作用域！！！
```
4. 普通HTML页面有哪些内容组成呢？HTML+CSS＋JS；与之对应的，我们的vue组件也有这些内容，只是书写的格式稍微有些变化；


## vue.js中基本的指令
1. 插值语法`{{}}`和插值语法中的表达式
2. 纯文本`v-text`
3. 纯HTML`v-html`
4. 绑定表单控件`v-model`，可以实现双向数据绑定
5. 绑定属性`v-bind:`，缩写为`:`
6. 绑定事件`v-on:`，缩写为`@`
7. 条件渲染`v-if`和`v-show`
v-if：直接把元素从页面上删除；
v-show:不删除元素，只是修改了元素的display属性

8. 列表渲染`v-for`


## Vue对象中的相关参数
1. data方法
2. methods对象
3. props数组
4. components对象

## vue.js中父组件给子组件传递数据
+ 注册子组件：
 - `import SonCom from './SonCom.vue' // 1. 【引入子组件】`
 - ```
components:{ // 2. 【注册组件】当前组件中，引用的子组件，都在这个components对象中进行定义
            Myson:SonCom // 在注册的时候，可以给组件设置别名
        }
```
+ 给子组件传递数据：
 - 父组件通过属性绑定的形式，将数据向下传递给子组件：`<Myson :fatherName="pName" :sonName="sName"></Myson>`
 - 子组件使用props属性，来接受父组件传递过来的值：`props:['fatherName', 'sonName'] // 父组件传递给子组件的属性，是一个数组形式的`

## vue-router的使用

## vue中的过滤器和计算属性
1. filters对象
2. computed对象

## vue-resource的使用

## vue.js中使用Mint-UI和MUI