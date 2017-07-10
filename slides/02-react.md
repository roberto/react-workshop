# React

---

## Agenda

* Concepts
* Components

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

* [The Secrets of React's Virtual DOM](https://youtu.be/-DX3vJiqxm4?t=1166)

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

### Creating a component

#### Function

```js
const Welcome = (props) => {
  return <h1>Hello, {props.name}</h1>
}

```

--

#### Class


```js
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {props.name}</h1>
  }
}

```

---

### Rendering a component

```js
const element = <Welcome name="Sarah" />

ReactDOM.render(
  element,
  document.getElementById('root')
)
```

---

