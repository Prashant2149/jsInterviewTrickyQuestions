

## 🔁 Section 1: Deep Dive into `this` in JavaScript (51–60)

### 51. What is `this` in JavaScript?
`this` refers to the object that is executing the current function.

---

### 52. What does `this` refer to in the global context?
In a browser, `this` refers to the `window` object.
```js
console.log(this); // window
```

---

### 53. What does `this` refer to inside an object method?
It refers to the object itself.
```js
const obj = {
  name: 'A',
  show: function() { console.log(this.name); }
};
obj.show(); // 'A'
```

---

### 54. What does `this` refer to in an event listener?
It refers to the HTML element that triggered the event.
```js
<button onclick="console.log(this)">Click</button>
```

---

### 55. What about `this` inside an arrow function?
Arrow functions do **not** bind their own `this`. They inherit `this` from the enclosing scope.
```js
const obj = {
  name: 'B',
  show: () => console.log(this.name)
};
obj.show(); // undefined (because `this` refers to window)
```

---

### 56. How does `this` behave in constructor functions?
It refers to the newly created object.
```js
function Person(name) {
  this.name = name;
  console.log(this);
}
new Person('Alex');
```

---

### 57. What happens with `this` in a class method?
Same as objects — `this` refers to the instance.
```js
class Car {
  constructor(name) {
    this.name = name;
  }
  drive() {
    console.log(this.name);
  }
}
```

---

### 58. How do `call`, `apply`, and `bind` affect `this`?
- `call`: invokes function with a specific `this`
- `apply`: same, but with arguments as an array
- `bind`: returns a new function with bound `this`

```js
function greet() {
  console.log(this.name);
}
const user = { name: 'Luna' };
greet.call(user); // Luna
```

---

### 59. What does `this` refer to in setTimeout/setInterval?
In non-arrow functions, it's `window`.
```js
setTimeout(function() { console.log(this); }, 1000); // window
```

---

### 60. How do you fix `this` in callbacks?
Use arrow functions or bind `this` explicitly.
```js
setTimeout(() => console.log(this), 1000); // inherits from parent
```

---
# 💡 JavaScript Prototype Interview Questions (1–100)

A beginner-to-advanced level list of questions covering **JavaScript Prototypes**, inheritance, `this`, DOM, and output-based tricky interview questions. Each question is answered in a clear, beginner-friendly way.


---

## 🧩 Section 2: DOM Interview Questions (61–80)

### 61. What is the DOM?
The DOM (Document Object Model) is a programming interface for HTML and XML documents. It represents the structure as a tree of objects.

---

### 62. How do you access an element by ID?
```js
document.getElementById("myId")
```

---

### 63. How do you select multiple elements?
```js
document.querySelectorAll("div") // returns a NodeList
```

---

### 64. What’s the difference between `querySelector` and `getElementById`?
- `getElementById` only fetches by ID.
- `querySelector` uses CSS-style selectors and works for classes, tags, etc.

---

### 65. How do you change the inner text of an element?
```js
document.getElementById("demo").innerText = "Hello World";
```

---

### 66. How do you change HTML content of an element?
```js
document.getElementById("demo").innerHTML = "<b>Bold</b>";
```

---

### 67. How to add a new element to the DOM?
```js
const newEl = document.createElement("p");
newEl.textContent = "I’m new!";
document.body.appendChild(newEl);
```

---

### 68. How to remove an element?
```js
document.getElementById("demo").remove();
```

---

### 69. What is `addEventListener`?
It allows you to attach multiple event handlers to an element.
```js
btn.addEventListener("click", () => console.log("Clicked"));
```

---

### 70. Difference between `textContent`, `innerText`, and `innerHTML`?
- `textContent`: gets all text including hidden
- `innerText`: gets only visible text
- `innerHTML`: includes HTML tags

---

### 71. How do you create buttons in JS and add them to the DOM?
```js
for (let i = 1; i <= 3; i++) {
  const btn = document.createElement("button");
  btn.innerText = `Button ${i}`;
  btn.addEventListener("click", () => alert(`You clicked Button ${i}`));
  document.body.appendChild(btn);
}
```

---

### 72. How do you fetch API data and show it in HTML?
```js
async function fetchData() {
  const res = await fetch("https://jsonplaceholder.typicode.com/users");
  const data = await res.json();
  data.forEach(user => {
    document.body.innerHTML += `<p><strong>${user.name}</strong> - ${user.email}</p>`;
  });
}
fetchData();
```

---

### 73. What is event delegation?
Attaching one event handler to a parent instead of many children.
```js
document.getElementById("parent").addEventListener("click", e => {
  if (e.target.tagName === "BUTTON") alert("Button clicked!");
});
```

---

### 74. What are data attributes?
Custom attributes in HTML used to store extra data.
```html
<button data-user-id="123">Click Me</button>
```
```js
const id = e.target.dataset.userId;
```

---

### 75. Difference between `e.target` and `e.currentTarget`?
- `target`: actual clicked element
- `currentTarget`: the element the event was attached to

---

### 76. What is the DOMContentLoaded event?
It fires when the initial HTML document has been completely loaded and parsed.
```js
document.addEventListener("DOMContentLoaded", () => {
  console.log("DOM fully loaded");
});
```

---

### 77. What is the difference between `==` and `===` in JS?
- `==` checks value (loose equality)
- `===` checks value + type (strict equality)

---

### 78. How to loop over DOM elements?
```js
document.querySelectorAll("button").forEach(btn => {
  btn.addEventListener("click", () => alert(btn.innerText));
});
```

---

### 79. Can you explain the event bubbling and capturing?
- **Bubbling**: event goes from child up to parent.
- **Capturing**: event goes from parent to child.

---

### 80. What is `preventDefault()` and `stopPropagation()`?
- `preventDefault()`: stops default action
- `stopPropagation()`: stops event from bubbling

---

# 💡 JavaScript Prototype Interview Questions (1–100)

A beginner-to-advanced level list of questions covering **JavaScript Prototypes**, inheritance, `this`, DOM, and output-based tricky interview questions. Each question is answered in a clear, beginner-friendly way.


---

## 🧠 Section 3: Output-Based Hard Questions (81–100)

### 81. What will be the output?
```js
const obj = {
  a: 10,
  getA: function () {
    return this.a;
  },
};

const copy = obj.getA;
console.log(copy());
```
**Output:** `undefined`
**Explanation:** `copy()` is called without an object, so `this` refers to `window` (in browser), which has no `a`.

---

### 82. Output?
```js
const obj = {
  val: 'Hello',
  print: function () {
    console.log(this.val);
  },
};
setTimeout(obj.print, 0);
```
**Output:** `undefined`
**Why?** `this` loses context in `setTimeout`. Fix with bind:
```js
setTimeout(obj.print.bind(obj), 0);
```

---

### 83. Output?
```js
function A() {
  this.value = 42;
}
const a = new A();
console.log(a.__proto__ === A.prototype);
```
**Output:** `true`

---

### 84. Output?
```js
function Parent() {
  this.name = 'Parent';
}
Parent.prototype.say = function () {
  return 'Hello from ' + this.name;
};

function Child() {
  this.name = 'Child';
}
Child.prototype = Object.create(Parent.prototype);
const c = new Child();
console.log(c.say());
```
**Output:** `Hello from Child`

---

### 85. Output?
```js
const user = {
  name: 'Amit',
  greet() {
    return `Hello, ${this.name}`;
  },
};
const greet = user.greet;
console.log(greet());
```
**Output:** `Hello, undefined`

---

### 86. Output?
```js
function User(name) {
  this.name = name;
}
User.prototype.sayHi = function () {
  console.log(`Hi, ${this.name}`);
};

const u1 = new User('Max');
setTimeout(u1.sayHi, 0);
```
**Output:** `Hi, undefined`
**Fix:** `setTimeout(u1.sayHi.bind(u1), 0);`

---

### 87. Output?
```js
const A = function () {
  this.name = 'A';
};
const a1 = new A();
A.prototype.name = 'B';
console.log(a1.name);
```
**Output:** `A` (because instance property shadows prototype)

---

### 88. Output?
```js
const A = function () {};
const B = function () {};
A.prototype = B.prototype;
const a = new A();
console.log(a instanceof B);
```
**Output:** `true`

---

### 89. Output?
```js
function X() {}
const x = new X();
console.log(x.constructor === X);
```
**Output:** `true`

---

### 90. Output?
```js
function Dog() {}
const dog1 = new Dog();
Dog.prototype.bark = function () {
  return 'woof';
};
console.log(dog1.bark());
```
**Output:** `woof`

---

### 91. Output?
```js
function Fn() {}
Fn.prototype = {
  greet: function () {
    return 'Hello';
  },
};
const f = new Fn();
console.log(f.greet());
```
**Output:** `Hello`

---

### 92. Output?
```js
function A() {}
A.prototype = {};
const a = new A();
console.log(a.constructor === A);
```
**Output:** `false` because constructor is not reset after prototype reassignment

---

### 93. Output?
```js
function Test() {}
Test.prototype.say = function () {
  return this.name;
};
const t = new Test();
t.name = 'Prototype';
console.log(t.say());
```
**Output:** `Prototype`

---

### 94. Output?
```js
let p = { name: 'A' };
let c = Object.create(p);
console.log(c.name);
```
**Output:** `A`

---

### 95. Output?
```js
let a = { x: 1 };
let b = Object.create(a);
b.x = 2;
console.log(a.x, b.x);
```
**Output:** `1 2`

---

### 96. Output?
```js
function P() {}
const p = new P();
console.log(Object.getPrototypeOf(p) === P.prototype);
```
**Output:** `true`

---

### 97. Output?
```js
const o = {};
o.__proto__.hello = 'world';
console.log({}.hello);
```
**Output:** `world`

---

### 98. Output?
```js
function A() {}
A.prototype = { a: 1 };
const a = new A();
console.log(a.__proto__ === A.prototype);
```
**Output:** `true`

---

### 99. Output?
```js
let x = { a: 1 };
let y = Object.create(x);
delete y.a;
console.log(y.a);
```
**Output:** `1`

---

### 100. Output?
```js
const proto = {
  speak() {
    return 'hello';
  },
};
const obj = Object.create(proto);
console.log(obj.speak());
```
**Output:** `hello`






