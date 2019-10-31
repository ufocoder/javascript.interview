JavaScript Interview
====================

This documents contains the most actual and important questions for JavaScript developer position. 
It will helps you to compose question list for your own interview or prepare to interview.

Table of contents:

* [Inheritance in JavaScript](#inheritance-in-javascript):
    * [Theory](#theory):
      - [What is functional inheritance pattern? How to create protected methods and private properties?](#question-i1-what-is-functional-inheritance-pattern-how-to-create-protected-methods-and-private-properties)
    * [Practice](#practice):
      - [Write `Object.create` polyfill](#question-i2-write-objectcreate-polyfill)
      - [What will output the following code and why?](#question-i3-what-will-output-the-following-code-and-why)
* [Closure in JavaScript](#closure-in-javascript):
    * [Theory](#theory-1):
      - [What is Closure in JavaScript?](#question-c1-what-is-closure-in-javascript)
      - [Does any currying function have a closure?](#questions-c2-does-any-currying-function-have-a-closure-give-an-example-please)
    * [Practice](#practice-1):
      - [What will output the following code and why?](#question-c3-what-will-output-the-following-code-and-why)
      - [Resolving example of problem code](#question-c4-resolving-example-of-problem-code)
      - [Write `nextID` function](#question-c5-write-nextid-function-that-will-generate-id-incrementally-after-each-calling)
* [Bind, apply and call function methods](#bind-apply-and-call-function-methods) 
    * [Practice](#practice-2):
      - [Write `sum` function](#question-b1-write-sum-function)
* [Hoisting in JavaScript](#hoisting-in-javascript):
    * [Theory](#theory-2):
      - [What is a hoisting in JavaScript](#question-h1-explain-what-is-hoisting-in-JavaScript)
    * [Practice](#practice-3):
      - [What will output the following code and why?](#question-h2-what-will-output-the-following-code-and-why)
      - [What will output the following code and why?](#question-h3-what-will-output-the-following-code-and-why)
      - [What will output the following code and why?](#question-h4-what-will-output-the-following-code-and-why)
* [Event Loop](#event-loop)
    * [Theory](#theory-3):
      - [How works event loop in the browser JavaScript?](#question-el1-how-works-event-loop-in-the-browser-javascript)
    * [Practice](#practice-4):
      - [What will output the following code and why?](#question-el2-what-will-output-the-following-code-and-why)
* [Scope in JavaScript](#scope-in-javascript)
    * [Practice](#practice-5):
      - [What will output the following code and why?](#question-s1-what-will-be-the-output-of-the-following-code-and-why)



## Inheritance in JavaScript

### **Theory**

### Question i1: What is functional inheritance pattern? How to create protected methods and private properties?

### **Practice**

### Question i2: Write `Object.create` polyfill
For implementing use this [kata](https://www.codewars.com/kata/58b3e68aa68b70accb000614) please.

### Question i3: What will output the following code and why?

```js
var baseObject = {
  prop: 'Base value',
  getProp: function() {
    return this.prop;
  }
};

var otherObject = Object.create(baseObject);

otherObject.prop = "Other value";

console.log(otherObject.getProp());
delete otherObject.prop;
console.log(otherObject.getProp()); 
```

**Answer**

Console will output:

```
Other value
Base value
```

## Closure in JavaScript

### **Theory**

### Question c1: What is Closure in JavaScript?

[MDN definition](https://developer.mozilla.org/en/docs/Web/JavaScript/Closures):
Closures are functions that refer to independent (free) variables (variables that are used locally, but defined in an enclosing scope). In other words, these functions 'remember' the environment in which they were created.

[JavaScript.isSexy](http://javascriptissexy.com/understand-javascript-closures-with-ease/): A closure is an function that has access to the outer (enclosing) function’s variables-scope chain.

### Questions c2. Does any currying function have a closure? Give an example, please.

**Example**

```js
const addTwoThings = thingToAdd(2);
addTwoThings(3); // -> 5

const addTwoThings = thingToAdd(10);
addTwoThings(30); // -> 40
```

**Answer**

Currying functions consist of chaining closures that return inner functions. So in the case of `thingToAdd` you will have two separate closures that each return a single value that gets evaluated sequentially.

#### Example implementation using ES6

```js
const thingToAdd = (a) => (b) => a + b;
```

#### Example implementation showing Closures

```js
let thingToAdd = function (a) {
    return function (b) {
        return a + b;
    }
}
```

### **Practice**

### Question c3: What will output the following code and why?

```js
function outerFunction() {
    var flag = undefined;

    function innerFunction() {
      if (true) {
        flag = true;
      } else {
        var flag = false;
      }

      console.log(flag);
    }

    console.log(flag);
    innerFunction();
}

outerFunction();
```

**Answer**

Console will output the followings:

```
undefined
true
```

### Question c4: Resolving example of problem code

What will output these example? 

```js
for (var i = 0; i < 10; i++) {
    setTimeout(function() {
        console.log(i);
    }, 1000);
}
```

How to fix it to output numbers from 0 to 9?

**Answer**

They're several ways to resolve code above.

1) By creating a [IIFE](https://en.wikipedia.org/wiki/Immediately-invoked_function_expression) (Immediately Invoked Function Expression):

```js
for (var i = 0; i < 10; i++) {
    setTimeout((function(param) {
        console.log(i);
    })(i), 1000);
}
```

2) By using ES6 feature, by using [let syntax](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Statements/let) particularly:

```js
for (let i = 0; i < 10; i++) {
    setTimeout(function() {
        console.log(i);
    }, 1000);
}
```

3) By [binding](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Function/bind) `console.log` function: 

```js
for (var i = 0; i < 10; i++) {
    setTimeout(console.log.bind(console, i), 1000);
}
```

### Question c5: Write `nextID` function that will generate ID incrementally after each calling

There's an example of function output:

```js
nextID(); // output: 1
nextID(); // output: 2
nextID(); // output: 3
```

**Answer**

We should use closure in [IIFE](https://en.wikipedia.org/wiki/Immediately-invoked_function_expression):

```js
var nextID = (function() {
    var id = 0;
    return function() {
        console.log(++id);
    }
})();
```


## Bind, apply and call function methods

### **Practice**

### Question b1: Write `sum` function

This function must meet conditions:

```js
typeof sum(1) === 'function'
typeof sum(1)(2) === 'function'
typeof sum(1)(2)() === 'number'

sum(1)() === 1
sum(1,2)(3)() == 6
sum(1,2)(3,4)() === 10
```

**Answer**

```js
function sum (fn) {
  var sumArguments = Array.prototype.slice.call(arguments);
    
  return function sumInner() {
      if (arguments.length) {
          sumArguments = sumArguments.concat(Array.prototype.slice.call(arguments));

          return sumInner;
      } else {
          return sumArguments.reduce(function(total, arg) {
            return total + arg;
          }, 0);
      }
  };
}
```

## Hoisting in JavaScript

### **Theory**

### Question h1: Explain what is hoisting in JavaScript

**Answer**

[W3School](https://www.w3schools.com/js/js_hoisting.asp) Hoisting is JavaScript's default behavior of moving declarations to the top. In JavaScript, a variable can be declared after it has been used. In other words; a variable can be used before it has been declared.

### **Practice**

### Question h2: What will output the following code and why?

```js
var a = 1; 
function bar() { 
    if (!a) { 
        var a = 10; 
    } 
    console.log(a); 
} 
bar();
```

**Answer**

Console will output:

```
10
```

### Question h3: What will output the following code and why?

```js
var a = 1;
function b() {
    a = 10;
    return;
    function a() {}
} 
b(); 
console.log(a);
```

**Answer**

Console will output:

```
1
```
### Question h4: What will output the following code and why?

```js
function test() { 
    foo(); 
    bar();
    function foo() { 
        console.log('foo'); 
    }
    var bar = function() { 
        console.log('bar'); 
    } 
} 
test(); 
```

**Answer**

Console will output:

```
foo
TypeError: bar is not a function
```

## Event Loop

### **Theory**

### Question el1: How works event loop in the browser JavaScript?

**Answer**

Event Loop in the browser could be represented as the following code:

```js
while (eventLoop.waitForTask()) {  
  const taskQueue = eventLoop.selectTaskQueue();
  if (taskQueue.hasNextTask()) {
    taskQueue.processNextTask();
  }

  const microtaskQueue = eventLoop.microTaskQueue;
  while (microtaskQueue.hasNextMicrotask()) {
    microtaskQueue.processNextMicrotask();
  }

  if (eventLoop.shouldRender()) {
    eventLoop.render();
  }
}
```

[Check current presentation](http://slides.com/xufocoder/event-loop-in-the-browser-javascript)

### **Practice**

### Question el2: What will output the following code and why?

```js
console.log('script start');

setTimeout(function() {
  console.log('setTimeout');
}, 0);

Promise.resolve().then(function() {
  console.log('promise1');
}).then(function() {
  console.log('promise2');
});

console.log('script end');
```

**Answer**

Console will output:

```
script start
script end
promise1
promise2
setTimeout
```

## Scope in JavaScript

### **Practice**

### Question s1: What will be the output of the following code and why?

```js
try {
  console.log(a);
} catch (e) {
  try {
    a = 10;
    console.log(a);
  } catch (e) {
    console.log('bar');
  }
}
let a = 1;
```

**Answer**

Console will output:

```
bar
```

Reason:

Since `let` is uninitialized at any time until being declared (unlike `var` which is always initialized but with value `undefined`), the first attempt to `console.log(a)` will raise an error which will be caught by the catch block. Then, inside that catch block, there's `a = 10` inside a try block again. This will also raise an error because there's still no variable named `a` so the catch block will catch the error once again so the output will be `bar`.

## Contributing

I would be thankful for your [issues](https://github.com/ufocoder/javascript.interview/issues) and [pull requests](https://github.com/ufocoder/javascript.interview/pulls).
