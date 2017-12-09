# React-native学习笔记之六 使用react-navigation组件搭建app导航栏（一）

* 安装：

  在项目根目录运行命令行，使用`yarn add react-navigation`安装依赖包（如项目正在运行，请先停止）

* 快速创建：

  1. 打开App.js文件

  ```jsx
  import {
    StackNavigator
  } from 'react-navigation'
  import MainScreen from './js/MainScreen'
  import ProfileScreen from './js/ProfileScreen'

  const App = StackNavigator({
    Main: { screen: MainScreen },
    Profile: { screen: ProfileScreen },
  })

  export default App
  ```

  2. 根目录创建js目录，并新建MainScreen和ProfileScreen两个文件

  ```jsx
  import { Button } from 'react-native'
  import React from 'react'

  export default class MainScreen extends React.Component {
    static navigationOptions = {
      title: 'My initial Scene',
    };
    render() {
      const { navigate } = this.props.navigation;
      return (
        <Button
          title="Tap me to load the next scene"
          onPress={() =>
            navigate('Profile');
          }
        />
      );
    }
  }
  ```

  ```jsx
  import { Button } from 'react-native'
  import React from 'react'

  export default class ProfileScreen extends React.Component {
    static navigationOptions = {
      title: 'Welcome',
    };
    render() {
      const { goback } = this.props.navigation;
      return (
        <Button
          title="Tap me to load the next scene"
          onPress={() =>
            goback();
          }
        />
      );
    }
  }
  ```

* 效果如下：

  ![导航效果](http://reactnative.cn/static/docs/0.50/img/NavigationStack-NavigatorIOS.gif)

* 更多使用方法请参考[react-navigation官方文档](https://reactnavigation.org/docs/intro/)