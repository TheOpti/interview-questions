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


###  3. What is `this` mean in JavaScript?

TODO
 
###  4. What is the data structure of the DOM?

TODO

###  5. What is a Stack and a Queue? How would you create those data structures in JavaScript?

TODO

###  6. How can you tell if an image element is loaded on a page?

TODO

###  7. What is `call()` and `apply()`?

TODO

###  8. What is event delegation and what are the performance tradeoffs?

TODO

###  9. What is a Worker? When would you use one?

TODO


## Big O notation


## Interview tasks - exercises

### Remove duplicate Strings 

```js
// Create a function that takes a string and returns a new string without duplicates

const str = 'This is a test test string test exercise test is';
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

const foo = function() {
  console.log(this.bar);
}

let baz = foo.bind({ bar: 'hello' });
baz(); // hello
```

Solution:
```js
Function.prototype.bind = function(context) {
  return (...args) => {
    this.call(context, ...args);
  };
}
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
function findElem(elem, root) {
  const path = [];
  let pointer = elem;
  
  while (pointer.parent) {
    const idx = pointer.parent.children.indexOf(pointer);
    path.push(index);
  
    pointer = pointer.parent;
  }

  pointer = root;
  
  while (path.length) {
    pointer = children[path.pop()];
  }
}
```
