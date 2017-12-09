# React-native 学习笔记之五 网络请求

React Native提供了和web标准一致的[Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)，用于满足开发者访问网络的需求。如果你之前使用过`XMLHttpRequest`(即俗称的ajax)或是其他的网络API，那么Fetch用起来将会相当容易上手，你可以使用你喜欢的搜索引擎去搜索`fetch api`关键字以了解更多信息。以下以豆瓣api为例子:

* 发起网络请求

  ```javascript
  fetch('https://api.douban.com/v2/movie/in_theaters')
  	.then((res) => res.json())
  	.then((res) => console.log(res))
  	.catch((err) => console.error(err))
  ```

  1. fetch是基于ES6Promise的标准进行二次封装的网络请求方法，即在语法层面上使异步的网络请求看起来像同步执行一样，方便开发人员阅读与维护

  2. 第一步中，fetch可传入两个参数，第一个是请求的url地址，第二个是请求的参数配置，如下:

     | 参数名     | 类型            | 默认值  | 例子                                       |
     | ------- | ------------- | ---- | ---------------------------------------- |
     | method  | string        | get  | method: 'post'                           |
     | headers | object        | {}   | headers: { 'Content-type': 'application/json'} |
     | body    | string/object | ''   | body: {JSON.stringify({name: 'lilei'})}  |

     * method声明该请求的类型，有: GET,POST,PUT,DELETE,OPTIONS,PATCH(对应restful api的设计规范)
     * headers声明该次请求的请求头信息，可以设置请求体的内容类型如application/json或者加入cooking信息(react-native中没有，推荐使用token)等
     * body用于设置该次请求的参数根据请求头的content-type不同，设置的格式也不同

  3. 当请求发起后，成功的话，fetch将会把请求回来的结果通过promise传到下个then函数里，此时的请求结果如下:

     ![请求豆瓣api第一层结果](http://otbs2h7e2.bkt.clouddn.com/react-native-fetch.png)

     response只返回该次请求的状态的描述对象，并没有看到返回的结果。所以我们想要取的结果还需要调用该对象上的json方法，将返回结果转回json对象给我们处理。

  4. 同样，调用json方法后会返回一个Promise对象，我们需要在下一个then中才进行我们需要的处理。

     ![请求豆瓣api最终结果](http://otbs2h7e2.bkt.clouddn.com/react-native-fetch-result.png)

     最后我们才得到了整个豆瓣api返回的电影列表数据

  5. 当然，在网络不好或服务器无法正常响应的情况下，请求失败时，fetch会抛出一个错误，我们需要通过catch捕获这个错误并处理它。

* 处理请求的数据

  上面我们初步认识了如何使用fetch进行网络请求，接下来我们结合react-native来展示一个电影列表。

  1. 首先，我们先创建一个列表框架

  ```jsx
  import React from 'react'
  import {
    View,
    Text,
    FlatList,
    Alter,
    StyleSheet
  } from 'react-native'

  export default class App extends React.Component {
    constructor() {
      super()
      this.state = {
        movies: []
      }
    }

    render() {
      if (this.state.movies.length <= 0) {
        return (
          <View style={styles.container}>
            <Text>正在请求豆瓣API中，请稍后...</Text>
          </View>
        )
      }

      return (
        <View style={styles.container}>
          <FlatList
            data={this.state.movies}
            renderItem={({ item }) => <Text>{item.title}</Text>}
          />
        </View>
      )
    }
  }

  const styles = StyleSheet.create({
    container: {
      flex: 1,
      flexDirection: 'column',
      justifyContent: 'center',
      alignItems: 'center',
    }
  })
  ```

  ​	在没有请求回来数据之前，页面只显示正在请求中，现在我们来补充网络请求的代码

  2. 这里需要利用到生命周期函数，在组件初次渲染完成之后，我们再调用fetch进行网络请求

  ```jsx
  componentDidMount() {
      fetch('https://api.douban.com/v2/movie/in_theaters')
        .then((response) => response.json())
        .then((res) =>
          this.setState({
            movies: res.subjects
          })
        )
        .catch((err) => Alert(err))
    }
  ```

  ​	componentDidMount函数在组件初次渲染之后调用，此时请求豆瓣api，将api返回的结果通过setState函数设置到state里并再次触发组件渲染。这里，我们只需要结果中的subjects结果集。

  3. 当state里的movies长度大于0时，组件就会执行下方返回的结果，渲染出一个电影列表，当然这里我们只显示出电影的标题，其他年份海报还没显示，有兴趣的可以调style样式进行布局。

     ```jsx
     import React from 'react'
     import {
       View,
       Text,
       FlatList,
       Alter,
       StyleSheet
     } from 'react-native'

     export default class App extends React.Component {
       constructor() {
         super()
         this.state = {
           movies: []
         }
       }
       
       componentDidMount() {
         fetch('https://api.douban.com/v2/movie/in_theaters')
           .then((response) => response.json())
           .then((res) =>
             this.setState({
               movies: res.subjects
             })
           )
           .catch((err) => Alert(err))
       }

       render() {
         if (this.state.movies.length <= 0) {
           return (
             <View style={styles.container}>
               <Text>正在请求豆瓣API中，请稍后...</Text>
             </View>
           )
         }

         return (
           <View style={styles.container}>
             <FlatList
               data={this.state.movies}
               renderItem={({ item }) => <Text>{item.title}</Text>}
             />
           </View>
         )
       }
     }

     const styles = StyleSheet.create({
       container: {
         flex: 1,
         flexDirection: 'column',
         justifyContent: 'center',
         alignItems: 'center',
       }
     })
     ```

* 使用其他网络请求库

  除了react-native自带的fetch网络请求库，我们还可以通过包管理工具，下载一些我们觉得好用的网络请求库，如axios等等

  *注意不要引入jquery，因为jquery除了ajax请求还引入了一些只有web才有的如window对象。
