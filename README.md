

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

✅ Next up: Questions 61–100 (DOM & tricky output-based questions)? Say "continue" to proceed!

