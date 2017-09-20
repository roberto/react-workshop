# Intro to "Modern" JavaScript

---

## Agenda

* Brief History
* Overview
* Ecosystem
* Features

---

## Brief History

* 1995
  * Netscape recruited [Breadan Eich](https://en.wikipedia.org/wiki/Brendan_Eich)
  to create:
      * a Java young brother
      * written directly in the HTML
      * prototype made in 10 days
--
* 1996
  * Nestscape submitted Javascript to Ecma International
      * former European Computer Manufacturers Association
* 1997: EcmaScript 1
* 1998: EcmaScript 2
* 1999: EcmaScript 3
* ????: EcmaScript 4
--

* 2009: EcmaScript 5 (Harmony)
* 2011: EcmaScript 5.1
--

* 2015: EcmaScript 2015
* 2016: EcmaScript 2016
* 2017: EcmaScript 2017

[ECMAScript proposals](https://github.com/tc39/proposals)

???
Ecma examples of specifications: CD-ROM, Office Open XML, JSON

---

## Overview

* (Usually) Interpreted
* Dynamic typing
    * type checking at run time
* Weakly typed
    * operations without defined types for the operands in question
    * implicit type conversions

```js
  "10" + 1 // "101"
  "10" / 1 // 10
```
* ~~Prototype Based~~

???
Weakly typed: implicit type conversions

---

## Ecosystem

* Engines
  * [V8](https://github.com/v8/v8/wiki)
  * [Rhino](https://developer.mozilla.org/es/docs/Rhino)
--

* Runtimes
  * Browsers
  * [Node.js](https://nodejs.org/en/): V8 + event loop + C
    * [Ryan Dahl: Node JS](https://www.youtube.com/watch?v=EeYvFl7li9E)
--

* Package Manager
  * [npm](https://www.npmjs.com/)
--

* Transpilers
  * [Babel](https://babeljs.io/)
--

* Linters
  * [ESLint](https://eslint.org/)
--

* Bundlers
  * [Webpack](https://webpack.js.org/)
---

## Syntax

* Declaring constants/variables
* Declaring functions
* Using Object
* Handling Promises

---

## Exercises

* [Example 01](https://codepen.io/r_soares/pen/NvQJPL?editors=1010)


### Resources

* [Document API](https://developer.mozilla.org/en-US/docs/Web/API/Document)

---

## Code Structure

```js
console.log('Hello'); console.log('World');
// Hello World
```

```js
console.log('Hello')
console.log('World')
/* Hello World */
```

---

## Constants and variables

```js
let name
name = 'Tomato'
name = 'Tomato'
```

```js
const name2 = 'Potato'
```

---

## Data types

```js
let a // undefined
a = null
a = 2
a = '2'
a = true

console.log(typeof a) // "boolean"
```

---

## Arrays

```js
const animals = ['Giraffe', 'Cat']
```

--

```js
console.log(animails[1]) // 'Cat'
```

--

```js
animals.push('Dog')
```

[MDN - Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)

---

## Objects

```js
const logins = {
  test: 'test123',
  admin: 'admin'
}
```

---

## Declaring functions

```js
function sum (a, b) {
  return a + b
}
```
--
```js
const sum = (a, b) => {
  return a + b
}
```
--
```js
const sum = (a, b) => a + b
```

---

# Resources

* [The Modern JavaScript Tutorial](https://javascript.info/)
* [Weak And Strong Typing](http://wiki.c2.com/?WeakAndStrongTyping)
