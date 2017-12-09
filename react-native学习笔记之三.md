# React-native学习笔记之三 从编写一个Hello world中理解RN开发的思路

* 打开App.js文件，编写如下代码:

  ```jsx
  import React from 'react'
  import { View, Text, StyleSheet } from 'react-native'

  export default class App extends React.Component
  {
    render() {
      return (
      	<View style={styles.container}>
        		<Text style={styles.hello}>Hello world</Text>
          </View>
      )
    }
  }

  const styles = StyleSheet.create({
    container: {
      flex: 1,
      justifyContent: 'center',
      alignItems: 'center'
    },
    hello: {
      color: '#3f3f3f',
      fontSize: 20
    }
  })
  ```

  1. 引入基础模块React、视图组件View、文本组件Text和样式表组件StyleSheet；

  2. 创建一个名为App的组件，继承React的基础组件。通过这种方式创建的组件具有react组件的生命周期特性，如下图示例，对应执行不同的生命周期函数:

     ![react生命周期图](http://upload-images.jianshu.io/upload_images/1814354-4bf62e54553a32b7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

     *也可以直接创建一个纯函数代替继承方法创建的组件如:

     ```jsx
     const App = ({ ...props }) => {
       return (
       	<View>
         	<Text>Hello world</Text>
         </View>
       )
     }
     ```

     通过这种方法创建的组件没有生命周期函数，也没有this对象指向自身的属性，父组件传入的属性都会变成该函数的参数对象依次传入。这种组件称为无状态组件

  3. 如组件有父组件传入的参数，需要在组件类调用如下方法，使参数绑定至this里

     ```jsx
     class App extends React.Component
     {
       constructor(props) {
         super(props)
       }
     }
     ```

  4. render方法里返回需要渲染的组件结构和样式，如同写Html标签一样，只需要按照react-native官方的组件要求使用即可

     *这里有一点与Html不一样，文本只能在Text组件里写入，其他组件入内含文本，项目编译时会报错

  5. 组件内的样式通过StyleSheet组件生成一个对象，视图组件只需要调用其中的对象名称即可，如需要调用多个style，可以按如下方法调用:

     ```jsx
     render() {
       <View style={[styles.style1, styles.style2]}></View>
     }
     ```

     *style对象仅在当前文件的模块生效，即使是同名style也在其他模块无效

  6. 最后通过export导出组件