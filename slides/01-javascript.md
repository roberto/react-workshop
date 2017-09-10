# Intro to "Modern" JavaScript

---

## Agenda

* Brief History
* Features
* Ecosystem

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

???
Ecma examples of specifications: CD-ROM, Office Open XML, JSON

---

## Features

* (Usually) Interpreted
* Dynamic typing
    * type checking at run time
* Weakly typing

```js
  "10" + 1 // "101"
  "10" / 1 // 10
```
* ~~Prototype Based~~

---

## Ecosystem

* Engines
  * [V8](https://github.com/v8/v8/wiki)
--

* [Node.s](https://nodejs.org/en/): V8 + event loop + C
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

* Declaring functions
* Using Object
* Handling Promises

---

## Exercises

* [Example 01](https://codepen.io/r_soares/pen/NvQJPL?editors=1010)


### Resources

* [Document API](https://developer.mozilla.org/en-US/docs/Web/API/Document)

---

## Functions

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

## Object

---

## String

---

# Resources

* [The Modern JavaScript Tutorial](https://javascript.info/)
* [Weak And Strong Typing](http://wiki.c2.com/?WeakAndStrongTyping)
