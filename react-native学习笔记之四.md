# React-native 学习笔记之四 Props(属性)与State(状态)

* 在React native中，所有的组件的参数均以props传递。如Image组件里

```jsx
class App extends React.Component
{
  render() {
    return (
    	<Image 
        	source={{ uri: 'https://upload.wikimedia.org/wikipedia/commons/d/de/Bananavarieties.jpg' }}
         	style={{ width: 100 }}
         />
    )
  }
}
```

​	这里的source和style就是组件需要的属性。在自定义组件中，props一般为改组件的配置属性。

```jsx
class MyComponent extends React.Component
{
  constructor(props) {
    super(props)//这里是ES6绑定传入参数到this对象的方法
  }
  
  render() {
    return(
    	<View style={this.props.style}>
      		<Text style={this.props.fontStyle}>{this.props.title}</Text>
      	</View>
    )
  }
}
```

​	这里的自定义组件MyComponent中，通过传入不同的style属性控制自定义组件的样式行为，使其可以灵活使用在不同的场景之下。如传入一些警示用语到title，控制其为灰色，该组件就能作为警示语组件使用。

* 关于组件的状态，在React和React-native中，每个组件都是一个状态机。组件在不同的生命周期有不同的状态，这需要开发者自身去处理。如下:

```jsx
class MyCount extends React.Component
{
  constructor(props) {
    super(props)
    this.state = {
      count: 0
    }
  }
  
  handlePress = () => {
    this.setState({
      count: ++this.state.count 
    })
  }
  
  render() {
    return (
    	<View>
        	<Text>{this.state.count}</Text>
      		<Button onPress={this.handlePress} title="点击加一" />
      	</View>
    )
  }
}
```

​	这里我们实现了一个简单的计数器，当我们点击按钮的时候，触发handlePress函数，该函数让state里的count状态自增1，通过学习笔记三我们知道setState之后，组件会重新渲染视图更改发生变动的节点元素，从而实现更新组件的功能。

​	这里我们只是改变文本内容，假如组件中有类似高度，宽度等状态存于state里，那么发生改变的就是组件的宽高甚至其他样式。所以state不仅仅是数据的管理器，更是整个组件的数据/状态管理中心。