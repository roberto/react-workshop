# Good Practices

---

## Composition with props children

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

## Naming

```js
onClick = () => {
handleClick = () => {
submit = () => {
```

--

Pick one (with prefix)

[Eslint rule: react/jsx-handler-names](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-handler-names.md)

---

## Avoid complexity

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

## Event Switch

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

## Layout/Style components

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

## High Order Components

* It takes a component and returns an "enhanced" component

--

```elm
type awesome = (Component) -> AwesomeComponent
```
---

## High Order Components

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
## High Order Components

```js
connect(mapStateToProps)(Welcome)
```
--

```js
injectIntl(Welcome)
```

---

## Less Conditionals Hell

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

## Less Conditionals Hell with Recompose

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

## References

* https://facebook.github.io/react/docs/hello-world.html
* https://github.com/planningcenter/react-patterns
* http://reactpatterns.com/
