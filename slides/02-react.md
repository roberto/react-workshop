# React

---

## Agenda

* Concepts
* Components
* Properties
* Events
* State
* Lifecycle

---

## Concepts

* Virtual DOM
* HTML on JavaScript?

---
name: vdom

### Virtual DOM

---
template: vdom

```js
const vdom = div(                         // virtual DOM is created and saved on memory
  h1("hello world")
)

{{content}}
```

--
render(vdom, '#app')                      // virtual DOM is rendered on real DOM

{{content}}

--

const updatedVdom = div(                  // Create a new virtual DOM
  h1("hello everybody")
)

{{content}}

--

const diff = vdomDiff(vdom, updatedVdom)  // Generate diff comparing old vdom with the new one

{{content}}

--

patch(diff, '#app')                       // Diff is applied to the real DOM, ensuring the minimal changes possible

---
template: vdom

<div class="mermaid">
graph TD
    {{content}}
    subgraph Virtual DOM Tree
      vA((A))-->vB((B))
      vA-->vC((C))
      vB-->vD((D))
      vB-->vE((E))
      vC-->vG((G))
      vC-->vH((H))
      vD-->vI((I))
    end
</div>

--
subgraph Real DOM Tree
  rA((A))-->rB((B))
  rA-->rC((C))
  rB-->rD((D))
  rB-->rE((E))
  rC-->rG((G))
  rC-->rH((H))
  rD-->rI((I))
end
{{content}}
--
{{content}}
style vD fill:red
--
style rD fill:green
---
template: vdom

--

* Is updating Real DOM slow?

???
Nope, but the whole process also needs to re-calculate CSS, layout and repaint!
--

* Will Virtual DOM use more memory?

???
Batch updates

--

[The Secrets of React's Virtual DOM](https://youtu.be/-DX3vJiqxm4?t=1166)

---

### JSX: Syntax Extension

```jsx
const element = (
  <div>
    <h1>Hello!</h1>
    <h2 className="welcome">Good to see you here.</h2>
  </div>
)
```
???
Babel compiles JSX down to `React.createElement()` calls.

--

```js
const element = React.createElement("div", null,
  React.createElement("h1", null, "Hello!"),
  React.createElement("h2", {className: "welcome"}, "Good to see you here.")
)
```
???
`React.createElement()` performs a few checks and creates an object.

--

```js
const element = {
  type: "div",
  props: {
    children: [
      { type: "h1", props: { children: "Hello!" } },
      { type: "h2", props: { className: "welcome", children: "Good to see you here." } }
    ]
  }
)
```
???
These objects are called "React elements"

--

* [Introducing JSX](https://facebook.github.io/react/docs/introducing-jsx.html)

---
## Components

---
### Creating as functions

```js
function Card (props) {
  return (
    <div className="card">
      <h1>
        {props.name}
      </h1>
    </div>
  );
}
```
--

```js
const Card = (props) =>
  <div className="card">
    <h1>
      {props.name}
    </h1>
  </div>;
```
--
```js
import React from 'react';
```

---
### Creating as classes

```js
class Card extends React.Component {
{{content}} render () {
    return (
      <div className="card">
        <h1>
          {this.props.name}
        </h1>
      </div>
    );
  }
}
```
--
*
---

### Rendering

```js
import React from 'react';
import { render } from 'react-dom';
import Card from './Card';

const App = () => <Card name="Chris" />

*render(<App />, document.getElementById('root'));
```
---

## Properties

* props -> output
* Object
* Read only

--

```js
const Card = (props) => // ... props.name
```
--
```js
<Card name="Chris"{{content}} />
```
--
 visible editing={false} hobbies={['surfing', 'netflix']}
--
```js
const cardProps = {
  name: "Chris",
  visible: true,
  editing: false,
  hobbies: ['surfing', 'netflix']
}

<Card {...cardProps} />
```
--
```jsx
<Card name="Chris">
  <Avatar "image.png" />
</Card>

// props.children
```
---

## Properties

```js
class Card extends React.Component {
  render () {
    this.props.name
  }
}

{{content}}
```
--
Card.defaultProps = {
  name: 'Taylor'
}
--

Typechecking

```js
import PropTypes from 'prop-types';

Card.propTypes = {
  name: PropTypes.string.isRequired
}
```
* Only checked on development
* [Validators](https://facebook.github.io/react/docs/typechecking-with-proptypes.html#proptypes)
* Alternatives: [Flow](https://flow.org/) or [TypeScript](https://www.typescriptlang.org/)

---
## Events

```html
class App extends Component {
{{content}}  handleChange (event) {
    console.log(event.target.value)
  }

  render () {
    <div>
      <label>Username:</label>
{{content}}      <input type="text" onChange={this.handleChange} />
      <Card name="Chris" />
    </div>
  }
}
```
--
*
--

* [Supported Events](https://facebook.github.io/react/docs/events.html#supported-events)
---
## Events

```html
class UserInput extends Component {
  handleChange = event => {
    if (event.key === 'Enter') {
      this.props.onUpdate(event.target.value);
    }
  };
  render() {
    return (
      <div>
        <label>Username:</label>
        <input type="text" onKeyUp={this.handleChange} />
        <Card name="Chris" />
      </div>
    );
  }
}
```
--
```html
{{content}}  updateUser = (user) => console.log(event.target.value)

  <div>
    <UserInput onUpdate={this.updateUser} />
{{content}}    <Card name={?} />
  </div>
```
--
*
---

## State

```js
class App extends Component {
  constructor(props) {
    super(props);
    this.state = {
      user: props.user,
    };
  }
{{content}}
```
--

  changeUser = user => {
    this.setState({ user });
  };

{{content}}
--
  render() {
    return (
      <div>
        <UserInput onChange={this.changeUser} />
        <Card name={this.state.user} />
      </div>
    );
  }
}
---
## Lifecycle

<div class="mermaid">
graph TD
{{content}}
    subgraph Mounting
      A(constructor)-->B(componentWillMount)
      B-->C(render)
      C-->D(componentDidMount)
    end
</div>
--
    subgraph Updating
      uA(componentWillReceiveProps)-->uB(shouldComponentUpdate)
      uB-->uC(componentWillUpdate)
    end
    {{content}}
--
    subgraph Unmount
      eA(componentWillUnmount)
    end
---

## Lifecycle

```js
componentWillReceiveProps(newProps) {
  if (this.props.name !== newProps.name) {
    this.fetchUser(newProps.name);
  }
}
```
--
```js
fetchUser(username) {
  axios.get(`https://api.github.com/users/${username}`).then(response => {
*   this.setState({
      data: this.formatData(response.data),
    });
  });
}
```
---
## Resources

* Editor
  * https://codesandbox.io/
* Data
  * https://developer.github.com/v3/users/
  * http://avatars.adorable.io/
  * http://xoart.link/
  * http://lorempixel.com/
* Style
  * https://github.com/lepture/github-cards
* Slides
  * Remark
  * Backslide
  * gh-page
  * mermaid
