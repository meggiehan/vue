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
//必须使用export default导出一个对象，然后，这个对象内部，必须有一个data函数，函数内部，必须返回一个对象
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

## 路由的概念
1. 什么是路由：不同的URL地址，可以链接到不同的页面，这就是路由；
2. 什么是路由规则：就是url地址栏中，不同的hash就是不同的路由规则；
  + 首页：/home
  + 新闻咨询：/news/newslist
  + 新闻详细：/news/newsinfo/13
3. 路由规则的表现形式：
  + 单层路由规则：/home
  + 嵌套路由规则：/photo/photolist
  + 带参数的路由规则：/photo/photoinfo/:id


## vue-router的使用
1. 运行`cnpm i vue-router --save`安装vue-router2.0的版本
2. 导入vue模块和vue-router模块
```
import Vue from 'vue'
import VueRouter from 'vue-router'
```
3. 注册vue-router到vue中`Vue.use(VueRouter)`
4. 创建路由规则：
```
var router = new VueRouter({
    routes: [ // 所有的路由规则，都存在于这个数组下面
        { name: 'login', path: '/login', component: LoginCom }, // 登录页面的路由规则
        { name: 'register', path: '/register', component: RegisterCom } // 注册页面的路由规则
    ]
});
```
5. 使用路由规则
```
// 5. 创建Vue实例，在实例中，使用路由规则
new Vue({
    el:'#app', // 指定挂载到的元素
    router:router, // 在vue实例中，使用了路由规则
    render: c=>c(App)
});
```
6. 在页面中使用`<router-link to="/login">登录</router-link>`创建路由链接
7. 在页面中使用`<router-view></router-view>`显示路由中，`component`所对应的页面




## vue中的过滤器和计算属性
1. filters对象：过滤器
 + 定义过滤器：
 ```
 filters:{ // 定义当前组件中自己的过滤器
        strToUpperCase(input){ // 过滤器是一个方法
            return input.toUpperCase();
        },
        // 假如用户输入的名称，长度超过了N位，则截取前N个字符，之后的所有字符，用...来表示
        sliceName(name, length){ // 使用多个过滤器来处理我们“即将”渲染到页面上的数据，可以给过滤器传参，从第二个参数开始，就是我们调用过滤器时候，传递的参数列表
            return name.slice(0, length) + '...';
        }
    }
 ```
 + 使用过滤器：
 ```
 <div>{{name | strToUpperCase | sliceName(5)}}</div>
 ```


2. computed对象：计算属性
 + 计算属性的好处：让我们在使用某些属性的时候，不必需要手动拼接了
 + 注意：计算属性在定义的时候，是一个方法；但是，在使用的时候，不能当作方法来调用，只能像属性一样直接使用；因此，不能给它传参
 + 计算属性 和 过滤器 的区别：过滤器可以传参，但是计算属性不能传参
 + 计算属性的特点：会跟着Data中属性的变化，而重新计算值

## vue-resource的配置
1. 使用vue-resource来实现vue的数据请求；
2. 用的最多的数据请求方式：get \ post \ jsonp
3. vue-resource的配置方式：
 + 运行`cnpm i vue-resource --save-dev`，把vue-resource安装为我们的运行依赖；
 + 导入vue-resource模块：`var VueResource = require('vue-resource');`
 + 注册vue-resource到Vue之中：`Vue.use(VueResource);`
 + 修改请求的方式：`Vue.http.options.emulateJSON = true;`

## vue-resource的使用
1. 当Vue实例调用`created`生命周期函数的时候,表示我们的组件已经在内存中初始化完毕，同时，组件中的数据 和 事件 都已经初始化完毕了！
2. 当组件渲染到页面上之后，会调用`Mounted`生命周期函数；当我们需要操作界面上的一些元素的时候，需要在Mounted事件中进行；
3. 代码示例：
```
getData(){ // 定义一个get请求，获取服务器数据
        // this.$http.get('http://127.0.0.1:8899/api/getnewslist').then(成功的回调函数，失败的回调函数);
        this.$http.get('http://127.0.0.1:8899/api/getnewslist').then(data=>{
            console.log(data.body);
        });
    },
    postData(){ // 定义一个Post请求，获取服务器数据
        this.$http.post('http://127.0.0.1:8899/api/post',{name:'zs'}).then(data=>{
            console.log(data.body);
        });
    },
    jsonpData(){// 定义一个jsonp请求，获取服务器数据
        this.$http.jsonp('http://127.0.0.1:8899/api/jsonp').then(data=>{
            console.log(data.body);
        });
    }
```

## 箭头函数（lambda）的补充【音译：拉姆达表达式】
1. ()=>{} 这是箭头函数最标准的书写格式，前面的()表示形参列表， 后面的{}表示函数体 lambda 拉姆哒表达式
2. data =>{console.log(data.body);} 如果箭头函数前面的形参列表，只有一个形参，那么可以省略小括号
3. data => console.log(data.body) 如果我们的函数体，只包含一行代码，那么，表示函数体的{}也可以被省略
4. (data, index) =>{} 如果有多个形参，那么，前面的小括号不可以省略，多个形参之间使用逗号`,`分割


## vue.js中使用Mint-UI
1. 运行`cnpm i mint-ui --save`将Mint-UI安装到运行依赖
2. 导入Mint-UI模块:`import MintUI from 'mint-ui'`
3. 导入Mint-UI的样式文件:`import 'mint-ui/lib/style.css'`
4. 注册MintUI到Vue中:`Vue.use(MintUI)`


## vue.js中使用MUI
1. 导入MUI的JS文件`import MUI from '../libs/mui-master/dist/js/mui.min.js'`
2. 导入MUI的CSS样式文件`import '../libs/mui-master/dist/css/mui.min.css'`
3. 导入MUI的图标样式文件`import '../libs/mui-master/examples/hello-mui/css/icons-extra.css'`
4. **【注意：】**由于MUI的JS中，使用了**callee，caller,arguments**，导致严格模式下，webpack编译不通过，因此，我们需要借助于babel-plugin-transform-remove-strict-mode来帮我们移除严格模式！
```
transform-remove-strict-mode的使用步骤：
1.运行 npm install babel-plugin-transform-remove-strict-mode --save-dev 把其安装到开发依赖；
2.在.babelrc配置文件中，添加plugins节点，并配置如下：
{
  "plugins": ["transform-remove-strict-mode"]
}
```