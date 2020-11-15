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
