# 💡 Ultimate JavaScript Prototype Interview Guide

This README is a comprehensive resource covering everything about JavaScript prototypes, prototype inheritance, tricky output-based questions, DOM challenges, and deep dive hacks. Ideal for interviews or mastering JS internals.

---

## 📚 Contents
1. [What is a Prototype?](#what-is-a-prototype)
2. [__proto__ vs prototype](#proto-vs-prototype)
3. [Prototype Chain](#prototype-chain)
4. [Prototype Inheritance](#prototype-inheritance)
5. [Constructor Functions & Inheritance](#constructor-functions--inheritance)
6. [Top 60+ Prototype Questions](#top-60-prototype-questions)
7. [Top 50 Hard JS Output-based Questions](#top-50-hard-js-output-based-questions)
8. [DOM Output-based Questions](#dom-output-based-questions)
9. [Tricky `this` Questions](#tricky-this-questions)
10. [Deep Dive Prototype Hacks](#deep-dive-prototype-hacks)

---

## 🔰 What is a Prototype?
Every JavaScript object has a hidden internal property `[[Prototype]]` (can be accessed via `__proto__`) which refers to another object. This forms a prototype chain.

```js
function Person(name) {
  this.name = name;
}
Person.prototype.sayHi = function () {
  console.log("Hi, I'm " + this.name);
};
const john = new Person("John");
john.sayHi();
```

## 🔀 __proto__ vs prototype
```js
function A() {}
const a = new A();
a.__proto__ === A.prototype; // true
```
- `prototype`: Property on functions used to build inheritance.
- `__proto__`: The actual internal pointer to the prototype of the object.

## 🧬 Prototype Chain
```js
const john = new Person("John");
// john → Person.prototype → Object.prototype → null
```

## 🧱 Prototype Inheritance
```js
function Animal(name) {
  this.name = name;
}
Animal.prototype.makeSound = function () {
  console.log("Sound");
};
function Dog(name) {
  Animal.call(this, name);
}
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;
Dog.prototype.bark = function () {
  console.log("Woof!");
};
```

---

## 🧠 Constructor Functions & Inheritance
```js
function ConstructorExample() {
  this.value = 10;
  console.log(this);
}
new ConstructorExample();
```

## ❓ Top 60+ Prototype Questions with Detailed Answers
All explained like a beginner would understand:
- Basic `prototype` concept
- Why `__proto__` exists
- Object chain traversal
- Difference in setting vs linking prototypes
- Prototype on built-in vs custom types
- Constructor vs Instance `prototype`
- Output: `new obj1.print()` behavior
- Multiple inheritance (mixin-like logic)
- `Object.create(null)` and its effects
- Object chaining & memory efficiency
- `Object.getPrototypeOf()` vs `__proto__`
- Difference in arrow functions and regular functions with `this`
- Building inheritance without `class`
- Custom `instanceof` implementation
- Polyfill for `Object.create`
- Behavior of prototype after reassignment

---

## 🧪 Top 50 Hard JS Output-based Questions
```js
function A() {}
A.prototype.x = 1;
const a = new A();
console.log(a.x); // 1
```
```js
function B() {}
const b = new B();
B.prototype = { y: 2 };
console.log(b.y); // undefined
```
- Covers: `__proto__`, shadowing, method overriding, reassignment traps
- Async output mixed with prototype methods
- New constructor hacks and prototype resets
- Hoisting tricks with prototype

---

## 🖱️ DOM Output-based Questions
```js
for (let i = 1; i <= 3; i++) {
  const btn = document.createElement("button");
  btn.innerText = `Button ${i}`;
  btn.addEventListener("click", () => {
    console.log(`You clicked button ${i}`);
  });
  document.body.appendChild(btn);
}
```
- Event listener memory leak traps
- `var` vs `let` behavior in event loops
- DOM insertion + prototype tracking
- Understanding button scoping

---

## 🎯 Tricky `this` Questions
```js
var obj = {
  value: 'hi',
  print: function() {
    console.log(this);
  },
};
new obj.print(); // Logs new object instance
```
- Constructor inside another object
- `this` context loss in setTimeout
- Arrow vs function context in prototype
- Using bind/apply in prototypal loops

---

## 🚀 Deep Dive Prototype Hacks
### 1. Prototype Pollution
```js
const payload = JSON.parse('{"__proto__": {"isAdmin": true}}');
console.log({}.isAdmin); // true (danger!)
```
### 2. Borrowing Methods
```js
const arrayLike = { 0: 'a', 1: 'b', length: 2 };
console.log(Array.prototype.slice.call(arrayLike)); // ["a", "b"]
```
### 3. Polyfill for Object.create
```js
function create(proto) {
  function F() {}
  F.prototype = proto;
  return new F();
}
```
### 4. Custom `instanceof`
```js
function customInstanceOf(obj, constructor) {
  let proto = Object.getPrototypeOf(obj);
  while (proto) {
    if (proto === constructor.prototype) return true;
    proto = Object.getPrototypeOf(proto);
  }
  return false;
}
```
### 5. Object.create(null)
```js
const obj = Object.create(null);
console.log(obj.toString); // undefined
```


📌 Happy Hacking!

