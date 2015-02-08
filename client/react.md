# React
React is a Javascript framework, but not an MVC one like Angular. React is just the view.

React is all about modular, composable components. A component bundles together the HTML and the JS of a particular UI element. Components may store internal state, but at the end they just generate HTML.

You absolutely cannot build a fully functional dynamic application with React alone.

<br />

##### Component examples
Components must implement a `render` function which should return the HTML representation of that component at any given time. The `render` function is called when the component is instantiated and automatically every time the state of the component is updated.

The render function has access to the state of the component `this.state` and to the properties of the component `this.props` which have been passed by its parent.

```js
var HelloMessage = React.createClass({
  render: function() {
    return <div>Hello {this.props.name}</div>;
  }
});

React.render(<HelloMessage name="John" />, mountNode);
```

```js
var Timer = React.createClass({
  getInitialState: function() {
    return {secondsElapsed: 0};
  },
  tick: function() {
    this.setState({secondsElapsed: this.state.secondsElapsed + 1});
  },
  componentDidMount: function() {
    this.interval = setInterval(this.tick, 1000);
  },
  componentWillUnmount: function() {
    clearInterval(this.interval);
  },
  render: function() {
    return (
      <div>Seconds Elapsed: {this.state.secondsElapsed}</div>
    );
  }
});

React.render(<Timer />, mountNode);
```

<br />
##### Render
When `render()` has returned, React will only update the real DOM if your rendered output has changed. Your render function is actually generating a "virtual DOM", which React compares to the previous output of `render()`. If the two virtual DOMs are different, React will update the real DOM with only the difference.

<br />
##### Props
You can pass properties to a component like this:
```js
render: function() {
    return (
      <div className="commentList">
        <Comment author="Pete Hunt" />Some text</Comment>
      </div>
    );
  }
```
From the Comment component, you can access the author via `this.props.author`. You can access the inner nested elements (in this case 'Some text') via `this.props.children`.

Props are immutable.

<br />
##### State
The state of a component is kept in `this.state`. The state is private to the component and can be changed by calling this.setState(). When the state is updated, the component re-renders itself.

A component may provide an implementation of `getInitialState()`, which is executed only once, at the beginning of the lifecycle of the component, and sets up the initial state of the component.

<br />
##### Form events
Components can contain forms. You can define a callback to be invoked when the user submits the form:
```js
var CommentForm = React.createClass({
  handleSubmit: function(e) {
    e.preventDefault();
    var author = this.refs.author.getDOMNode().value.trim();
    // TODO: send request to the server
    this.refs.author.getDOMNode().value = '';
  },
  render: function() {
    return (
      <form className="commentForm" onSubmit={this.handleSubmit}>
        <input type="text" ref="author" />
        <input type="submit" value="Post" />
      </form>
    );
  }
});
```

<br />
##### Refs
We use the ref attribute to assign a name to a child component and `this.refs` to reference the component. We can call getDOMNode() on a component to get the native browser DOM element.

<br />
##### Callbacks as props
A component parent passes props to its children. A prop can be a callback function in the parent component, so that when a particular event happens in the child, the child can invoke that callback within the parent.

<br />
##### Other component functions and objects
* `object getInitialState()`: Invoked once before the component is mounted. The return value will be used as the initial value of this.state.
* `object getDefaultProps()`: Invoked once and cached when the class is created. Values in the mapping will be set on `this.props` if that prop is not specified by the parent component.
* `object propTypes`: Allows you to validate props being passed to your components.
* `componentWillMount()`: Invoked once immediately before the initial rendering occurs.
* `componentDidMount()`: Invoked once immediately after the initial rendering occurs.
* `componentWillUpdate(object nextProps, object nextState)`: Invoked immediately before rendering when new props or state are being received. This method is not called for the initial render.
* `componentDidUpdate(object prevProps, object prevState)`: Invoked immediately after the component's updates are flushed to the DOM. This method is not called for the initial render.
* `componentWillUnmount()`: Invoked immediately before a component is unmounted from the DOM. Perform any necessary cleanup in this method.
* `boolean shouldComponentUpdate(object nextProps, object nextState)`: Invoked before rendering when new props or state are being received. This method is not called for the initial render or when forceUpdate is used.

<br />
##### Mixins
Components are the best way to reuse code in React, but sometimes very different components may share some common functionality. React provides mixins to solve this problem. A mixin allows you to implement a common set of component lifecycle methods that can be re-used across multiple components.
```js
var SetIntervalMixin = {
  componentWillMount: function() {
    this.intervals = [];
  },
  setInterval: function() {
    this.intervals.push(setInterval.apply(null, arguments));
  },
  componentWillUnmount: function() {
    this.intervals.map(clearInterval);
  }
};

var TickTock = React.createClass({
  mixins: [SetIntervalMixin],
  ...
```

<br />
