# Data scientist Interview Questions & Answers

---

### Table of Contents

| No. | Questions                                                                                                                                                                                                                        |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|     | **Core React**                                                                                                                                                                                                                   |
| 1   | [What is React?](#what-is-react)                                                                                                                                                                                                 |
| 2   | [What are the major features of React?](#what-are-the-major-features-of-react)                                                                                                                                                   |
| 3   | [What is JSX?](#what-is-jsx)                                                                                                                                                                                                     |
| 4   | [What is the difference between Element and Component?](#what-is-the-difference-between-element-and-component)                                                                                                                   |
| 5   | [How to create components in React?](#how-to-create-components-in-react)                                                                                                                                                         |
| 6   | [When to use a Class Component over a Function Component?](#when-to-use-a-class-component-over-a-function-component)                                                                                                             |
| 7   | [What are Pure Components?](#what-are-pure-components)                                                                                                                                                                           |
| 8   | [What is state in React?](#what-is-state-in-react)                                                                                                                                                                               |
| 9   | [What are props in React?](#what-are-props-in-react)                                                                                                                                                                             |
| 10  | [What is the difference between state and props?](#what-is-the-difference-between-state-and-props)      


## Core React

1.  ### What is React?

    React is an **open-source front-end JavaScript library** that is used for building user interfaces, especially for single-page applications. It is used for handling view layer for web and mobile apps. React was created by [Jordan Walke](https://github.com/jordwalke), a software engineer working for Facebook. React was first deployed on Facebook's News Feed in 2011 and on Instagram in 2012.

    **[⬆ Back to Top](#table-of-contents)**

2.  ### What are the major features of React?

    The major features of React are:

    - Uses **JSX** syntax, a syntax extension of JS that allows developers to write HTML in their JS code.
    - It uses **VirtualDOM** instead of RealDOM considering that RealDOM manipulations are expensive.
    - Supports **server-side rendering**.
    - Follows **Unidirectional** data flow or data binding.
    - Uses **reusable/composable** UI components to develop the view.

    **[⬆ Back to Top](#table-of-contents)**

3.  ### What is JSX?

    _JSX_ is a XML-like syntax extension to ECMAScript (the acronym stands for _JavaScript XML_). Basically it just provides syntactic sugar for the `React.createElement()` function, giving us expressiveness of JavaScript along with HTML like template syntax.

    In the example below text inside `<h1>` tag is returned as JavaScript function to the render function.

    ```jsx harmony
    export default function App() {
      return (
        <div>
          <h1>{"Welcome to React world!"}</h1>
        </div>
      );
    }
    ```

     <details><summary><b>See Class</b></summary>
     <p>

    ```jsx harmony
    class App extends React.Component {
      render() {
        return (
          <div>
            <h1>{"Welcome to React world!"}</h1>
          </div>
        );
      }
    }
    ```

     </p>
     </details>

    **Note:** JSX is stricter than HTML

    **[⬆ Back to Top](#table-of-contents)**

4.  ### What is the difference between Element and Component?

    An _Element_ is a plain object describing what you want to appear on the screen in terms of the DOM nodes or other components. _Elements_ can contain other _Elements_ in their props. Creating a React element is cheap. Once an element is created, it is never mutated.

    The object representation of React Element would be as follows:

    ```javascript
    const element = React.createElement("div", { id: "login-btn" }, "Login");
    ```

    The above `React.createElement()` function returns an object:

    ```
    {
      type: 'div',
      props: {
        children: 'Login',
        id: 'login-btn'
      }
    }
    ```

    And finally it renders to the DOM using `ReactDOM.render()`:

    ```html
    <div id="login-btn">Login</div>
    ```

    Whereas a **component** can be declared in several different ways. It can be a class with a `render()` method or it can be defined as a function. In either case, it takes props as an input, and returns a JSX tree as the output:

    ```javascript
    const Button = ({ onLogin }) => (
      <div id={"login-btn"} onClick={onLogin}>
        Login
      </div>
    );
    ```

    Then JSX gets transpiled to a `React.createElement()` function tree:

    ```javascript
    const Button = ({ onLogin }) =>
      React.createElement(
        "div",
        { id: "login-btn", onClick: onLogin },
        "Login"
      );
    ```

    **[⬆ Back to Top](#table-of-contents)**

5.  ### How to create components in React?

    There are two possible ways to create a component.

    1. **Function Components:** This is the simplest way to create a component. Those are pure JavaScript functions that accept props object as the first parameter and return React elements:

       ```jsx harmony
       function Greeting({ message }) {
         return <h1>{`Hello, ${message}`}</h1>;
       }
       ```

    2. **Class Components:** You can also use ES6 class to define a component. The above function component can be written as:

       ```jsx harmony
       class Greeting extends React.Component {
         render() {
           return <h1>{`Hello, ${this.props.message}`}</h1>;
         }
       }
       ```

    **[⬆ Back to Top](#table-of-contents)**

6.  ### When to use a Class Component over a Function Component?

    If the component needs _state or lifecycle methods_ then use class component otherwise use function component.

    _However, from React 16.8 with the addition of Hooks, you could use state , lifecycle methods and other features that were only available in class component right in your function component._
    _So, it is always recommended to use Function components, unless you need a React functionality whose Function component equivalent is not present yet, like Error Boundaries._

    **[⬆ Back to Top](#table-of-contents)**

7.  ### What are Pure Components?

    _`React.PureComponent`_ is exactly the same as _`React.Component`_ except that it handles the `shouldComponentUpdate()` method for you. When props or state changes, _PureComponent_ will do a shallow comparison on both props and state. _Component_ on the other hand won't compare current props and state to next out of the box. Thus, the component will re-render by default whenever `shouldComponentUpdate` is called. In functional components we use `React.memo()` API. `React.memo()` is a higher-order component. It takes a React component as its first argument and returns a special type of React component that allows the renderer to render the component while memoizing the output. Therefore, if the component’s props are shallowly equal, the `React.memo()` component will bail out the updates.

    **[⬆ Back to Top](#table-of-contents)**

8.  ### What is state in React?

    _State_ of a component is an object that holds some information that may change over the lifetime of the component. We should always try to make our state as simple as possible and minimize the number of stateful components.

    Let's create a user component with message state,

    ```jsx harmony
    import React, { useState } from "react";

    function User() {
      const [message, setMessage] = useState("Welcome to React world");

      return (
        <div>
          <h1>{message}</h1>
        </div>
      );
    }
    ```

    <details><summary><b>See Class</b></summary>
    <p>

    ```jsx harmony
    class User extends React.Component {
      constructor(props) {
        super(props);

        this.state = {
          message: "Welcome to React world",
        };
      }

      render() {
        return (
          <div>
            <h1>{this.state.message}</h1>
          </div>
        );
      }
    }
    ```

    </p>
    </details>

    ![state](images/state.jpg)

    State is similar to props, but it is private and fully controlled by the component ,i.e., it is not accessible to any other component till the owner component decides to pass it.

    **[⬆ Back to Top](#table-of-contents)**

9.  ### What are props in React?

    _Props_ are inputs to components. They are single values or objects containing a set of values that are passed to components on creation using a naming convention similar to HTML-tag attributes. They are data passed down from a parent component to a child component.

    The primary purpose of props in React is to provide following component functionality:

    1. Pass custom data to your component.
    2. Trigger state changes.
    3. Use via `this.props.reactProp` inside component's `render()` method.

    For example, let us create an element with `reactProp` property:

    ```jsx harmony
    <Element reactProp={"1"} />
    ```

    This `reactProp` (or whatever you came up with) name then becomes a property attached to React's native props object which originally already exists on all components created using React library.

    ```
    props.reactProp
    ```

    **Example: Props in Class Based Component**

    ```jsx
    import React from "react";
    import ReactDOM from "react-dom";

    class ChildComponent extends React.Component {
      render() {
        return (
          <div>
            <p>{this.props.name}</p>
            <p>{this.props.age}</p>
          </div>
        );
      }
    }

    class ParentComponent extends React.Component {
      render() {
        return (
          <div>
            <ChildComponent name="John" age="30" />
            <ChildComponent name="Mary" age="25" />
          </div>
        );
      }
    }
    ```

    **Example: Props in Functional Component**

    ```jsx
    import React from "react";
    import ReactDOM from "react-dom";

    const ChildComponent = (props) => {
      return (
        <div>
          <p>{props.name}</p>
          <p>{props.age}</p>
        </div>
      );
    };

    const ParentComponent = () => {
      return (
        <div>
          <ChildComponent name="John" age="30" />
          <ChildComponent name="Mary" age="25" />
        </div>
      );
    };
    ```

    **[⬆ Back to Top](#table-of-contents)**

10. ### What is the difference between state and props?

    Both _props_ and _state_ are plain JavaScript objects. While both of them hold information that influences the output of render, they are different in their functionality with respect to component. Props get passed to the component similar to function parameters whereas state is managed within the component similar to variables declared within a function.

    **[⬆ Back to Top](#table-of-contents)**


## Disclaimer

The questions provided in this repository are the summary of frequently asked questions across numerous companies. We cannot guarantee that these questions will actually be asked during your interview process, nor should you focus on memorizing all of them. The primary purpose is for you to get a sense of what some companies might ask — do not get discouraged if you don't know the answer to all of them ⁠— that is ok!

Good luck with your interview 😊

---
```
