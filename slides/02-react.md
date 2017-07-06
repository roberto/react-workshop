# React

---

## Agenda

* Concepts
  * Virtual DOM
  * HTML on JavaScript: JSX
  * Server Side Rendering
* Components
  * Simplest one
  * Composing them
  * Rendering it
  * Event
* Features
  * Componentization
* State Management
  * State
  * Life cycle

---

## Concepts

* Virtual DOM
* HTML on JavaScript

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
    subgraph Real DOM Tree
      rA((A))-->rB((B))
      rA-->rC((C))
      rB-->rD((D))
      rB-->rE((E))
      rC-->rG((G))
      rC-->rH((H))
      rD-->rI((I))
    end
    subgraph Virtual DOM Tree
      vA((A))-->vB((B))
      vA-->vC((C))
      vB-->vD((D))
      vB-->vE((E))
      vC-->vG((G))
      vC-->vH((H))
      vD-->vI((I))
    end
    style vD fill:red
    style rD fill:green
</div>

---

### HTML on JavaScript: JSX

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

---
