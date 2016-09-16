# Agenda
* What is ReactJS ?
    * What is problem he solve ?
    * How it builds components ?
* Simple Component
    * React.createElement
    * JSX
* Reusable Components
    * Stateless Functions
    * React.createClass
    * Mixins 
    * React.Component / No Mixins / No Autobinding
    * Prop Validation
* Lifecycle
    * getInitialState
    * getDefaultProps
    * propTypes
    * mixins
    * statics 
    * displayName
    
    * componentWillMount
    * componentDidMount
    * componentWillReceiveProps 
    * shouldComponentUpdate
    * componentWillUpdate
    * componentDidUpdate
    * componentWillUnmount

## What is ReactJS ?

* React is a JavaScript library for creating user interfaces by Facebook and Instagram.
* Many people choose to think of React as the V in MVC.

### What is problem he solve ?
* Building large applications which automatically manage all UI updates  when your data changes over time.
* When the data changes, React conceptually hits the "refresh" button, and knows to only update the changed parts.

### How it builds components ?
* React encapsulated components make code reuse, testing, and separation of concerns easy.

### Example 1 
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Example 1</title>
    
    <script src="https://unpkg.com/react@15.3.1/dist/react.js"></script>
    <script src="https://unpkg.com/react-dom@15.3.1/dist/react-dom.js"></script>
    <script src="https://unpkg.com/babel-core@5.8.38/browser.min.js"></script>
    
  </head>
  <body>
    <div id="example"></div>
    <script type="text/babel">
    
      ReactDOM.render(
        <h1>Hello, world!</h1>,
        document.getElementById('example')
      );
      
    </script>
  </body>
</html>
```

## React.createElement
```
const ComponentA = React.createClass({
    displayName: "A",

    render: function render() {
        return React.createElement(
                "div",
                { className: "someClassName" },
                "Element Content ",
                this.props.name
        );
    }
});

ReactDOM.render(
    React.createElement(ComponentA, { name: "John" }),
    document.getElementById('example')
);
```

## React.DOM
```
const ComponentA = React.createClass({
    displayName: "A",

    render: function render() {
        return React.DOM.div(
                null,
                "Element Content ",
                this.props.name
        );
    }
});

ReactDOM.render(
    React.createElement(ComponentA, { name: "John" }),
    document.getElementById('example')
);
```

## JSX

an XML-like syntax called JSX. 

```
var ComponentA = React.createClass({
  render: function() {
    return (<div>Element Content {this.props.name}</div>);
  }
});

ReactDOM.render(
    React.createElement(ComponentA, { name: "John" }),
    document.getElementById('example')
);
```

## Stateless Functions

You may also define your React classes as a plain JavaScript function. For example using the stateless function syntax:

```
function HelloMessage(props) {
  return <div>Hello {props.name}</div>;
}

HelloMessage.propTypes = {
  name: React.PropTypes.string
}

HelloMessage.defaultProps = {
  name: 'John Doe'
}

ReactDOM.render(<HelloMessage name="Mădălina"/>, mountNode);
```

## Mixins

Components are the best way to reuse code in React, but sometimes very different components may share some common functionality. 

```
const LifeCycleMixin2 = {
    componentWillMount() {
        log('LifeCycleMixin2 componentWillMount');
    }
};

const LifeCycleMixin = {
  componentWillMount() {
      log('LifeCycleMixin componentWillMount');
  }
};

const WeatherApp = React.createClass({
    mixins: [LifeCycleMixin, LifeCycleMixin2],
    componentWillMount:  function() {
      log('WeatherAppView componentWillMount');
    },

    render: function () {
        return (<WeatherAppView />)
    }
});

export default WeatherApp;
```

## React.Component

You may also define your React classes as a plain JavaScript class. For example using ES6 class syntax:

```
class HelloMessage extends React.Component {
  render() {
    return <div>Hello {this.props.name}</div>;
  }
}

ReactDOM.render(<HelloMessage name="Sebastian" />, mountNode);
```

## No Autobinding

they don't automatically bind this to the instance

```
// You can use bind() to preserve `this`
<div onClick={this.tick.bind(this)}>

// Or you can use arrow functions
<div onClick={() => this.tick()}>
```