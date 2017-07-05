# React

---

## Agenda

* Concepts
  * Virtual DOM
* Components
  * Simplest one
  * Composing them
  * Rendering it
  * Event
* Features
  * Virtual DOM
  * Componentization
  * JSX
  * Server-Side Rendering
* State Management
  * State
  * Life cycle

---

## Concepts

* Virtual DOM

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
