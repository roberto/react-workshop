# React

---

## Agenda

* Concepts
* Components
* Patterns

---

## Concepts

* Virtual DOM
* HTML on JavaScript
* Server Side Rendering

---

### Virtual DOM

```js
const vdom = div(                         // virtual DOM is created and savend on memory
  h1("hello world")
)

{{content}}
```

--
render(vdom)                              // virtual DOM is rendered on real DOM

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

render(diff)                              // Diff is applied to the real DOM, ensuring the minimal changes possible

---

### Virtual DOM

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
{{content}}
style vD fill:red
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
style rD fill:green
---

### JSX: Syntax Extension

```jsx
const element = <h1>Hello, World!</h1>

{{content}}
```

--

const element2 = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
)

--

```js
const element = React.createElement("h1", null, "Hello, World!")

const element2 = React.createElement("div", null,
  React.createElement("h1", null, "Hello!"),
  React.createElement("h2", null, "Good to see you here.")
)
```

---

### Server Side Rendering - Usual Rendering

<div class="mermaid">
sequenceDiagram
    Browser->>Cache: request
    {{content}}
</div>

--
    Cache-->>Browser: "Empty" HTML
    Cache-->>Browser: app.js
    {{content}}
--
    Browser-->>Browser: initial state
    {{content}}
--
    Browser->>Server: AJAX[1]
    Server-->>Browser: data[1]
    Browser->>Server: AJAX[2]
    Server-->>Browser: data[2]
---

### Server Side Rendering

<div class="mermaid">
sequenceDiagram
    Browser->>Cache: request
    {{content}}
</div>

--
    Cache-->>Browser: HTML: initial + data[1]
    {{content}}
--
    Cache-->>Browser: app.js
    {{content}}
--
    Browser->>Server: AJAX[2]
    Server-->>Browser: data[2]
---

### Server Side Rendering

```js
const element = <h1>Hello World!</h1>

{{content}}
```

--
const html = ReactDOMServer.renderToString(element)

--

```js
const data1 = loadInformation()
const app = <App {..data1} />

const html = ReactDOMServer.renderToString(app)
```

[ReactDOMServer](https://facebook.github.io/react/docs/react-dom-server.html)

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

## Patterns

---

### Patterns - Composition with props children

```js
<Layout />
```
--

```js
<Layout>
  <Head />
  <Content>
    <MainTitle />
    <Articles />
  </Content>
  <Footer />
</Layout>
```
--

```js
<Layout>
  <Content>
    <Articles />
  </Content>
  <SideBar />
</Layout>
```

---

### Patterns - Naming

```js
onClick = () => {
handleClick = () => {
submit = () => {
```

--

Pick one (with prefix)

[Eslint rule: react/jsx-handler-names](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-handler-names.md)

---

### Patterns - Avoid complexity

```js
<div class={`header ${this.props.active ? 'on' : null} ${this.isEditing ?
'editing' : 'showing'}`} />
```

--

```js
const toggleEditorClass = isEditing ? 'editing' : 'showing'

const classes = {
  on: this.props.active,
  [toggleEditorClass]: true,
}

<div class={classNames('header', classes)} />
```

--

```js
const toggleEditorClass = isEditing ? 'editing' : 'showing'

<div class={classNames('header', toggleEditorClass, {on: this.props.active})} />
```

[package classnames](https://github.com/JedWatson/classnames)

<!-- TODO conditions -->

---

### Patterns - Event Switch

```js
handleClick() { /* action stuff */ }
handleMouseEnter() { this.setState({ hovered: true }) }
handleMouseLeave() { this.setState({ hovered: false }) }
```

--

```js
handleEvent({type}) {
  switch(type) {
    case "click":
      return /* action dates */
    case "mouseenter":
      return this.setState({ hovered: true })
    case "mouseleave":
      return this.setState({ hovered: false })
    default:
      return console.warn(`No case for event type "${type}"`)
  }
}
```

---

### Patterns - Layout/Style components

```js
class HorizontalSplit extends React.Component {
{{content}} shouldComponentUpdate() {
    return false
  }

  render() {
    <div class="horizontal">
      <div>{this.props.leftSide}</div>
      <div class="center">{this.props.children}</div>
      <div>{this.props.rightSide}</div>
    </div>
  }
}
```

--
*
---

### Patterns - High Order Components

* It takes a component and returns an "enhanced" component

--

```js
const Loading = <i class="loading"></i>

{{content}}
```

--
class Welcome extends React.Component {
  render () {
    return this.props.ready ? (...) : <Loading />
  }
}

--

```js
withLoading(Welcome)

{{content}}
```
--
class Welcome extends React.Component {
  render () {
    return (...)
  }
}
--

```js
const withLoading = (LoadComponent) =>
  (props) => props.ready ? <LoadComponent {...props} : <Loading />
```
--

```js
const withLoading = (LoadComponent) =>
  class extends React.Component {
    render () {
      return props.ready ? <LoadComponent {...props} : <Loading />
    }
  }
```
---
### Patterns - High Order Components

```js
connect(mapStateToProps)(Welcome)
```
--

```js
injectIntl(Welcome)
```

---

### Patterns - Less Conditionals Hell

```js
buildEditor () {
  return this.props.isVisible
    ? <Editor />
    : null
}

```

--

```js
buildEditor () {
  if(this.isEditing() && this.props.isVisible) {
    return <Editor />
  }

  return null
}

```
--

```js
buildEditor () {
  return renderWhen(this.props.isVisible, () => <Editor />)
}

{{content}}
```
--
const renderWhen(condition, renderComponent) =>
  return condition ? renderComponent() : null

---

### Patterns - Less Conditionals Hell with Recompose

```js
const renderWhen = condition =>
  branch(
    condition,
    renderNothing
  )
{{content}}
```
--

buildEditor () =>
  renderWhen(this.props.isVisible)(() => <Editor />)

--
```js
buildEditor () => {
  const editor = withProps({title})(Editor)
  renderWhen(this.props.isVisible)(editor)
}
```
--

[package recompose, API](https://github.com/acdlite/recompose/blob/master/docs/API.md)

---


# References

* https://facebook.github.io/react/docs/hello-world.html
* https://github.com/planningcenter/react-patterns
* http://reactpatterns.com/
