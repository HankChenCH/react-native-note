# React-native 学习笔记之二 开发前须知

* 目录结构，如下图：

  ![目录结构](http://otbs2h7e2.bkt.clouddn.com/react-native-catalog.png)

  1. tests目录用于存放测试文件
  2. android目录是安卓app编译目录
  3. ios目录是苹果app编译目录
  4. node_modules目录是程序依赖包目录
  5. .babelrc是ES6转义ES5的babel工具的配置文件
  6. App.js是项目根模块组件，用于导出整个项目app模块
  7. index.js是项目入口文件，引入App.js的模块，打包成两个平台的app文件
  8. package.json是项目的描述文件，包含项目名称，描述，项目依赖包的情况等详细条目
  9. yarn.lock是yarn包管理工具的生成文件，用于记录那些依赖包已经被下载安装，下次安装时无需重新下载

* 依赖包安装，以及模块导出和引入

  1. 和平常js文件引入不同，react-native的项目依赖包安装全部通过包管理工具（npm、yarn）进行安装和管理

  2. npm在安装node的时候已经自动一起安装，但是react-native官方推荐使用yarn包管理工具，所以这里我们需要另外安装一下yarn。打开cmd，输入`npm install -g yarn`，等待命令运行完毕，yarn包管理工具已经安装上。

  3. 安装依赖包：例--安装react-navigation

     打开cmd，进入项目目录，运行`yarn add react-navigation`， 包管理工具自动下载安装工具包和其依赖的其他包。安装完成后package.json文件会写入依赖文件名称，方便项目共享或重新安装。

     *`npm install react-navigation --save`具有同样安装效果，但建议还是使用yarn工具管理，使用两种包管理工具，可能导致项目文件被锁，操作项目启动失败

  4. 依赖包安装之后，在项目文件里只需要按照ES6模块引入规范，即可完成工具包引入:

     ```javascript
     import React from 'react'
     import { StackNavigator } from 'react-navigation'
     import * as Layout from './src/components'
     ```

     上述是ES6引入模块的三种方式:

     * 第一种是这个模块导出了一个模块对象，所以可以直接引入
     * 第二种是只引入这个模块对象里的其中的一些方法，使用了ES6的析构语法糖
     * 第三种是这个模块导出了几个模块对象，引入的时候将他们全部合并到一个对象里进行引入（这里演示的是引入自己写的模块，所以路径跟上面两种有所不同，依赖包引入不需要填写完整路径只需要填写包的名称）

  5. 自身编写完一些函数之后，可以通过export方法导出这个模块，供其他页面使用:

     ```javascript
     export default function foo(){}
     export function bar(){}
     export {
       test() {},
       woo() {}
     }
     module.exports={
       a:1,
       b:2
     }
     ```

     * 第一种是将这个方法导出成这个模块的默认方法，一般用于组件的导出
     * 第二种、第三种是将改方法普通导出，与其他方法组成整个模块，与第四种类似
     * 第四种将该文件以对象的形式，挂载在module对象里进行导出

  6. 以上关于ES6模块的介绍只是个人的理解，可能有误差，详尽的介绍请到[ES6入门教程查找](http://es6.ruanyifeng.com/#docs/module)

     ​

     ​