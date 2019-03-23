# React Docs
### Four ways to Create REact Components
* ES5 create class
```javascript
var HelloWorld = React.createClass({
  render: function() {
    return <h1> Hello World </h1>;
  }
});
```
* ES6 class
```javascript
class HelloWorld extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return <h1>Hello World</h1>;
  }
}

```
* ES5 stateless function
* ES6 stateless function
* Many more
