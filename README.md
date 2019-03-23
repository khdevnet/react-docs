# React Docs
### Four ways to Create React Components
##### ES5 create class
* Autobinding of functions (this.handleChange)
* PropTypes declared
* Default props declared
* Set initial state in method getInitialState

```javascript
var InputControlES5 = React.createClass({
  propTypes: {
    initialValue: React.PropTypes.string
  },
  defaultProps: {
    initialValue: ''
  },
  // Set up initial state
  getInitialState: function() {
    return {
      text: this.props.initialValue || 'placeholder'
    };
  },
  handleChange: function(event) {
    this.setState({
      text: event.target.value
    });
  },
  render: function() {
    return (
      <div>
        Type something:
        <input onChange={this.handleChange}
               value={this.state.text} />
      </div>
    );
  }
});
```
##### ES6 class
* No autobind (this.handleChange.bind(this))
* PropTypes declared separately
* Default props declared separately
* Set initial state in constructor

```javascript
class InputControlES6 extends React.Component {
  constructor(props) {
    super(props);

    // Set up initial state
    this.state = {
      text: props.initialValue || 'placeholder'
    };

    // Functions must be bound manually with ES6 classes
    this.handleChange = this.handleChange.bind(this);
  }
  
  handleChange(event) {
    this.setState({
      text: event.target.value
    });
  }
  
  render() {
    return (
      <div>
        Type something:
        <input onChange={this.handleChange}
               value={this.state.text} />
      </div>
    );
  }
}
InputControlES6.propTypes = {
  initialValue: React.PropTypes.string
};
InputControlES6.defaultProps = {
  initialValue: ''
};
```
##### ES5 stateless function
```javascript
var HelloWorld = function(props) {
  return <h1>Hello World</h1>;
};
```
##### ES6 stateless function
* No class needed
* Avoid `this` keyword
* Keep component pure
* High signal-to-noise ratio (less code need to write)
* Enhanced code completion/intellisense
* Easy to test
* Performance

```javascript
const HelloWorld = props => {
  const sayHi = event => {
    console.log(`Hi ${props.name}`);
  };

  return (
    <div>
      <a href="#" onClick={sayHi}>
        Say hi
      </a>
    </div>
  );
};

HelloWorld.propTypes = {
  name: React.PropTypes.string
};
HelloWorld.defaultProps = {
  name: ""
};

```
* Many more
