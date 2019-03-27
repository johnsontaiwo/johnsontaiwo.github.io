---
layout: post
title:      "How to use setState() method in     React."
date:       2019-03-27 01:37:04 +0000
permalink:  how_to_use_setstate_method_in_react
---


React Components can receive or pass data either as props or state. The main difference between the two is their immutability. While state’s data can be changed by their components, props’s data cannot be changed by child components, according to React documentations.

Also, props are passed down from a parent component to a child component while state is owned by the component in which it’s declared.
In this short article, I’ll concentrate on Component’s state and how to update it properly, using the **setState()** method provided by React.

Take for example the code below: 
```
class Comment extends Component {

 state = {
 likes: 0
 }

render() {
 return(
 <div>
 Likes: {this.state.likes}
 </div>
 )
 }
}
export default Comment

```

In the above code, we have a class Comment component with a state object, initialized with likes, whose value is set to zero. We can access the current state’s value directly in the **render()** method like as shown above, to give us the value of the state, which is zero (0).

Supposing we want to increase the number of the likes in our comment component, then we’ll need to update the state to accomplish this task.
One way to do this will be to write a code like this: 
```
handleLikesChange() {
 this.state.likes = this.state.likes + 1
}

```

According to React documentations the code above will not work because, the component will not re-render. instead React provides us with a **setState()** method to update a component’s state.

However, the **setSate()** method is Asynchronous and must be used properly. In our commentcomponent, to increase the likes with setState(), the following code may fail to work:

```
addLike = () => {
this.setState({
likes: this.state.likes + 1}
)}

```
Because the value of our next state depends on the value of our previous state, it’s better to use the second form of **setState()** that accepts a function as its argument. That function will receive the previous state as its first argument:
```
addLike = () => {
this.setState(prevState => {
return {
likes: prevState.likes + 1}}
)}

```

The only reason for this is to ensure reliability in performance. Like I mentioned above, **setSate()** is asynchronous which will re-render the component and get called after the addLike function is executed. It’s a request but not a command.
See the complete code below.

```
class Comment extends Component {

 state = {
 likes: 0
 }
addLike = () => {
this.setState(prevState => {
return {
likes: prevState.likes + 1}}
)}

render() {
 return(
 <div>
 <button onClick={ this.addLike }>Like</button>
 </div>
 )
 }
}
export default Comment

```
