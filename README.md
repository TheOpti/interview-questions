# interview-questions

This document contains interview questions and tasks for Frontend Developer positions.
It contains different questions and tasks related to Javascript, HTML, CSS and all other
modern technologies used for frontend development.

Feel free to use it as well as add your suggestions.

Keywords: #javascript #interview #interview-questions #frontend #css #html

---

> Interviews should be like a first date, pretty awkward, a little challenging,
> yet you have to put your best face forward. At the end, do you think if it
> works out, that was really satisfying. I think I wanna continue on this journey
> with this person

> It [interview] should be challenging and rewarding at the same time, but it shouldn't
> be frustrating.

-- Jem Young, **Interviewing for Front-End Engineers**

---

## Prescreen JavaScript questions

### 1. What is the difference between `const`, `let`, and `var`?

- `var`:

  - scoped globally (if placed outside function) or per function
  - are hoisted (moved to the top of the scope)
  - can be re-declared and updated

- `let`:

  - block scoped
  - can be updated, but not re-declared
  - are not hoisted

- `const`:
  - cannot be updated or re-declared
  - constant value (or reference)

All declarations (`var`, `let`, `const`, `function`, `function*`, `class`) are
"hoisted" in JavaScript. This means that if a name is declared in a scope,
in that scope the identifier will always reference that particular variable:

```js
x = "global";
// function scope:
(function() {
  x; // not "global"
  var/let/… x;
}());

// block scope (not for `var`s):
{
  x; // not "global"
  let/const/… x;
}
```

### 2. Explain prototypical inheritance

JavaScript doesn’t use classical inheritance. Instead, it uses prototypal
inheritance i.e., an object can inherit properties from another object.
The prototypal inheritance is achieved via the prototype linkage.

When it comes to inheritance, JavaScript only has one construct: objects.
Each object has a private property which holds a link to another object
called its prototype. That prototype object has a prototype of its own,
and so on until an object is reached with null as its prototype.

By definition, null has no prototype, and acts as the final link in
this prototype chain.

### 3. What is `this` mean in JavaScript?

`this` represents a context in which a function was called. It can't be set
by assignment during execution, and it may be different each time the function is called.

It has different values depending on where it is used:

- Alone, this refers to the global object.
- In a method, this refers to the owner object.
- In a function, this refers to the global object.
- In a function, in strict mode, this is undefined.
- In an event, this refers to the element that received the event.
- Methods like `call()`, and `apply()` can refer this to any object.

Since the following code is not in strict mode, and because the value
of this is not set by the call, this will default to the global object, which is window in a browser:

```
function f1() {
  return this;
}

// In a browser:
f1() === window; // true

// In Node:
f1() === globalThis; // true
```

**Note**: ES6 (ES2015) introduced arrow functions which don't provide their own this binding (it retains the this value of the enclosing lexical context):

```
const myObject = {
  myMethod: () => {
    console.log(this);
  }
};

myObject.myMethod() // this === window or global object

const myMethod = myObject.myMethod;
myMethod() // this === window or global object
```

Differences & Limitations of arrow functions:

- Does not have its own bindings to `this` or `super`, and should not be used as methods.
- Does not have `new.target` keyword.
- Not suitable for `call`, `apply` and `bind` methods, which generally rely on establishing a scope.
- Can not be used as constructors.
- Can not use `yield`, within its body.

### 4. What is the data structure of the DOM?

The DOM (Document Object Model) is an API that represents and interacts with any HTML or XML document. The DOM is a document model loaded in the browser and representing the document as a node tree, where each node represents part of the document (e.g. an element, text string, or comment).

![DOM](/images/4_DOM.png)

The actual DOM hierarchy is composed of nodes with lists of child nodes and attributes. The lists are either double linked lists or arrays. Probably the latter, I'd imagine. The node also has properties for things like the parent node.

The document currently loaded in each one of your browser tabs is represented by a document object model. This is a "tree structure" representation created by the browser that enables the HTML structure to be easily accessed by programming languages.

Links:

- [Manipulating elements](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Client-side_web_APIs/Manipulating_documents).

### 5. What is a Stack and a Queue? How would you create those data structures in JavaScript?

#### Stack

Stack is an abstract data type that serves as a collection of elements, with two main principal operations:

- **Push**, which adds an element to the collection, and
- **Pop**, which removes the most recently added element that was not yet removed.

The order in which elements come off a stack gives rise to its alternative name, LIFO (last in, first out).

Implementation example:

```
var stack = [];
stack.push(2);       // stack is now [2]
stack.push(5);       // stack is now [2, 5]
var i = stack.pop(); // stack is now [2]
alert(i);            // displays 5
```

#### Queue

Queue is a collection of entities that are maintained in a sequence and can be modified by the addition of entities at one end of the sequence and the removal of entities from the other end of the sequence.

The operations of a queue make it a first-in-first-out (FIFO) data structure.

```
var queue = [];
queue.push(2);         // queue is now [2]
queue.push(5);         // queue is now [2, 5]
var i = queue.shift(); // queue is now [5]
alert(i);              // displays 2
```

Links:

- [Exploring Stacks and Queues via JavaScript](https://www.digitalocean.com/community/tutorials/js-stacks-queues)

### 6. How can you tell if an image element is loaded on a page?

Using `load` event:

```
var image = document.createElement("img");
image.src = "path/to/image1.jpg";
image.onload = function() {
  console.log("Image 1 ready to append");
  document.body.append(this);
};
```

Other solution is to use the HTMLImageElement interface’s complete attribute. It returns true if the image has completely loaded and false otherwise. We can use this with naturalWidth or naturalHeight properties, which would return 0 when the image failed to load.

```
window.addEventListener("load", event => {
  var image = document.querySelector('img');
  var isLoaded = image.complete && image.naturalHeight !== 0;
  alert(isLoaded);
});
```

### 7. What is `call()` and `apply()`?

`this` keyword - `this` is determined by how a function is called (runtime binding). It can't be set by assignment during execution, and it may be different each time the function is called.

#### `call()`

The `call()` method calls a function with a given this value and arguments **provided individually**.

Example:

```
fn.call(context, arg1, arg2, arg3, ...);
```

#### `apply()`

The `apply()` method calls a function with a given this value, and arguments **provided as an array** (or an array-like object).

Example:

```
fn.apply(context, [arg1, arg2, arg3, ...]);
```

#### Bonus - `bind()`

`bind()` - method creates a new function that, when called, has its this keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.

```
const module = {
  x: 42,
  getX: function() {
    return this.x;
  }
};

const unboundGetX = module.getX;
console.log(unboundGetX()); // The function gets invoked at the global scope
// expected output: undefined

const boundGetX = unboundGetX.bind(module);
console.log(boundGetX());
// expected output: 42
```

Links:

- [This is why we need to bind event handlers in Class Components in React](https://www.freecodecamp.org/news/this-is-why-we-need-to-bind-event-handlers-in-class-components-in-react-f7ea1a6f93eb/)

### 8. What is event delegation and what are the performance tradeoffs?

Event delegation allows to avoid adding event listeners to specific nodes. Instead, the event listener is added to one parent. Adding event handlers to each of the 1000 cells would be a major performance problem and, potentially, a source of browser-crashing memory leaks.

#### Event propagation - bubbling vs capturing

A click event propagates in 3 phases:

1. Capture phase — Starting from `window`, `document` and the root element, the event dives down through ancestors of the target element
2. Target phase — The event gets triggered on the element on which the user has clicked
3. Bubble phase — Finally, the event bubbles up through ancestors of the target element until the root element, `document`, and `window`.

![DOM](/images/8_event_delegation.webp)

#### `event.target` vs `event.currentTarget`

Difference between them:

- `target` is the element that triggered the event (e.g., the user clicked on)
- `currentTarget` is the element that the event listener is attached to.

#### document.fragment

Document Fragment is much faster when it is used to insert a set of elements in multiple places.

```
var fragment = new DocumentFragment();
...
fragment.appendChild(elements);
```

### 9. What is a Worker? When would you use one?

TODO

## Big O notation

## Interview tasks - exercises

### Remove duplicate Strings

```js
// Create a function that takes a string and returns a new string without duplicates

const str = "This is a test test string test exercise test is";
removeDuplicates(str); // This is a test string exercise
```

Solution:

```
function removeDuplicates(str) {
  const words = str.split(' ');
  const withNoDuplicates = new Set([...words]);
  return [...withNoDuplicates].join(' ');
}
```

### Flattening an Array

```js
// Without using .flat(), create a function to flatten an array

const arr = [1, 2, [3, 4, [5, 6, 7], 8], 9, 10];
flatten(arr); // [1,2,3,4,5,6,7,8,9,10]
```

Solution:

```js
function flatten(arr) {
  return arr.reduce((acc, value) => {
    if (Array.isArray(value)) {
      return [...acc, ...flatten(value)];
    }

    return [...acc, value];
  }, []);
}
```

### Writing your own Bind function

```js
// Implement Function.prototype.bind

const foo = function () {
  console.log(this.bar);
};

let baz = foo.bind({ bar: "hello" });
baz(); // hello
```

Solution:

```js
Function.prototype.bind = function (context) {
  return (...args) => {
    this.call(context, ...args);
  };
};
```

### Implement debounce

```js
const debounce = (delay, fn) => {
  let timer;

  return (...argList) => {
    if (timer) clearTimeout(timer);

    timer = setTimeout(() => {
      fn(...argList);
      timer = null;
    }, delay);
  };
};
```

### Tree exercise

```js
// We have 2 identical DOM trees, A and B. For DOM tree A, we have
// the location of an element. Create a function to find that same element
// in tree B.
```

Solution:

```js
function backwardsPath(element, root) {
  const path = [];
  let current = element;

  while (current.parentNode) {
    const index = [...current.parentNode.children].indexOf(current);
    path.push(index);
    current = current.parentNode;
  }

  current = root;
  while (path.length) {
    current = current.children[path.pop()];
  }

  return current;
}
```

### Rendering exercise

```js
// Create a function to move an element. The function args are:
// distance, duration, element to move

function moveElement(distance, duration, element) { ... }
```

Solution:

```js
function moveElement(duration, distance, element) {
  const start = performance.now();

  function move(currentTime) {
    const elapsedTime = currentTime - start;
    const progress = elapsedTime / duration;

    const amountToMove = progress * distance;
    element.style.transform = `translateX(${amountToMove}px)`;

    if (progress < 1) {
      requestAnimationFrame(move);
    }
  }

  move(performance.now());
}
```

### Promise exercise

```js
// Create a sleep function that takes one parameter (time)
// and will wait "time" ms
```

Solution:

```js
function sleep(time) {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve();
    }, time);
  });
}
```

Bonus:

```js
// Create a function to turn any function into a "promisified" function.
// Any function will have a callback as a last arg
const exampleFn = (x, y, callback) => { ... };

const promisedFn = promisify(exampleFn);

promisedFn().then(...).then(...);
```

Solution:

```js
function promisify(fn) {
  return function (...args) {
    return new Promise(function (resolve, reject) {
      function cb(result) {
        resolve(result);
      }

      fn.apply(this, args.concat(cb));
    });
  };
}
```
