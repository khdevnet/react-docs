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
* Keep component pure, best for presentation component
* Use them whenever is possible 
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
##### Other ways
* Object.create
* Mixins
* Parasitic Components
* StampIt

#### When should I use  Class vs Stateless Components
| Class | Stateless  |        
| ------------- |:-------------:| 
| State      | Everywhere else | 
| Refs      |       |  
| Lifecycle methods |      | 
| Child functions (for performance) |       | 


#### Difference Container vs Presentation Components
| Container | Presentation  |        
| ------------- |:-------------:| 
| Little to no markup      | Nearly all markup | 
| Pass data and actions down | Receive data and actions via props  |  
| Knows about Redux | Doesn't know about Redux  | 
| Often stateful |  Typically functional components (stateless)   | 

####  When Do I Need Redux?
* Complex data flows
* Inter-component communication
* Non-heirarchical data
* Many actions
* Same data used in multiple places

#### Redux Core principles
* Single source of truth - The state of your whole application is stored in an object tree within a **single store**.
* State is read-only - The only way to change the state is to emit an **action**, an object describing what happened.
* Changes are made with pure functions - To specify how the state tree is transformed by actions, you write pure **reducers**.
![](https://github.com/khdevnet/react-docs/blob/master/docs/redux-data-flow.png)

#### Flux Core principles
* Single source of truth - The state of your whole application is stored in an multiple object tree within a **multiple stores**.
* State is mutable - The  way to change the state is to emit an **action** or change it directly, an object describing what happened.
* The **dispatcher** receives actions and dispatches them to stores that have registered with the dispatcher. Every store will receive every action. There should be only one singleton dispatcher in each application..
![](https://github.com/khdevnet/react-docs/blob/master/docs/flux-data-flow.png)

### Flux Vs Redux
* Flux is a pattern and Redux is a library.

* Flux is a fancy name for the observer pattern modified a little bit to fit React, but Facebook released a few tools to aid in implementing the Flux pattern, so the following is the difference between using these tools (which is commonly referred to as using Flux) and using Redux.

* Both Flux and Redux have actions. Actions can be compared to events (or what trigger events). In Flux, an action is a simple JavaScript object, and that’s the default case in Redux too, but when using Redux middleware, actions can also be functions and promises.

* With Flux it is a convention to have multiple stores per application; each store is a singleton object. In Redux, the convention is to have a single store per application, usually separated into data domains internally (you can create more than one Redux store if needed for more complex scenarios).

* Flux has a single dispatcher and all actions have to pass through that dispatcher. It’s a singleton object. A Flux application cannot have multiple dispatchers. This is needed because a Flux application can have multiple stores and the dependencies between those stores need a single manager, which is the dispatcher.

* Redux has no dispatcher entity. Instead, the store has the dispatching process baked in. A Redux store exposes a few simple API functions, one of them is to dispatch actions.

* In Flux, the logic of what to do on the data based on the received action is written in the store itself. The store also has the flexibility of what parts of the data to expose publicly. The smartest player in a Flux app is the store.

* In Redux, the logic of what to do on the data based on the received actions is in the reducer function that gets called for every action that gets dispatched (through the store API). A store can’t be defined without a reducer function. A Redux reducer is a simple function that receives the previous state and one action, and it returns the new state based on that action. In a Redux app, you can split your reducer into simpler functions as you would do with any other function. The smartest player in Redux is the reducer.

* In Redux, also, there isn’t a lot of flexibility about what to expose as the store’s state. Redux will just expose whatever returned from the store’s reducer. This is one constraint.

* The other bigger constraint is that the store’s state cannot be mutable (or really, shouldn’t be). There is no such constraint in Flux, you can mutate the state as you wish. The state’s immutability, in Redux, is achieved easily by making the reducers pure functions (with no side effects). Redux reducers always copy the state they receive and returns a modified version of the state’s copy, not the original object itself. While this is a big constraint, it makes life much easier long term.
