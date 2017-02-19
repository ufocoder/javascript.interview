Javascript Interview
====================

This documents contains the most actual and important questions for Javascript developer position. 
It will helps you to compose question list for your own interview or prepare to inverview.

Table of contents:

* [Inheritance in Javascript](#inheritance-in-javascript):
   * [Write `Object.create` polyfill](#question-i1-write-object-create-polyfill)
   * [What is functional inherence pattern? How to create protected methods and private propreties?](#question-what-is-functional-inherence-pattern-how-to-create-protected-methods-and-private-propreties)
   * [What will output the following code](#question-i3-what-will-output-the-following-code-and-why)
* [Closure in Javascript](#closure-in-javascript):
    * [What is Closure in Javascript?](#question-c1-what-is-closure-in-javascript)
    * [What will output the following code](#question-c2-what-will-output-the-following-code-and-why)
    * [Resolving example of problem code](#question-c3-resolving-example-of-problem-code)
    * [Write `nextID` function](#question-c4-write-nextid-function-that-will-generate-id-incrementally-after-each-calling)
* [Bind, apply and call function methods](#bind-apply-and-call-function-methods) 
    * [Write `sum` function](#question-b1-write-sum-function)
* [Hoisting in Javascript](#hoisting-in-javascript):
   * [What is a hoisting in Javascript](#question-h1-explain-what-is-hoisting-in-Javascript)
   * [What will output the following code](#question-h2-what-will-output-the-following-code-and-why)
   * [What will output the following code](#question-h3-what-will-output-the-following-code-and-why)

## Inheritance in Javascript

### Question i1: Write `Object.create` polyfill

### Question i2: What is functional inherence pattern? How to create protected methods and private propreties?

### Question i3: What will output the following code and why:
```
var baseObject = {
  prop: "Base value",
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

Console will output 
```
Other value
Base value
```

## Closure in Javascript

### Question c1: What is Closure in Javascript?

[MDN definition](https://developer.mozilla.org/en/docs/Web/JavaScript/Closures):
Closures are functions that refer to independent (free) variables (variables that are used locally, but defined in an enclosing scope). In other words, these functions 'remember' the environment in which they were created.

[Javascript.isSexy](http://javascriptissexy.com/understand-javascript-closures-with-ease/): A closure is an function that has access to the outer (enclosing) function’s variables-scope chain.


### Question c2: What will output the following code and why:

```
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
true
undefined
```

### Question c3: Resolving example of problem code

What will output these example? 

```
for (var i=0; i < 10; i++){
    setTimeout(function(){
        console.log(i);
    }, 1000);
}
```

How to fix it to output numbers from 0 to 9?

**Answer**

Ther're several ways to resolve code above.

1) By creating a [IIFE](https://en.wikipedia.org/wiki/Immediately-invoked_function_expression) (Immediately Invoked Function Expression):
```
for (var i=0; i < 10; i++){
    setTimeout((function(param){
        console.log(i);
    })(i), 1000);
}
```

2) By using ES6 feature, by using [let syntax](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Statements/let) particularly:
```
for (let i=0; i < 10; i++){
    setTimeout(function(){
        console.log(i);
    }, 1000);
}
```

3) By [binding](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Function/bind) `console.log` function: 
```
for (var i=0; i < 10; i++){
    setTimeout(console.log.bind(console, i), 1000);
}
```

### Question c4: Write `nextID` function that will generate ID incrementally after each calling
There's an example of function output:
```
nextID(); // output: 1
nextID(); // output: 2
nextID(); // output: 3
```

**Answer**

We should use closure in [IIFE](https://en.wikipedia.org/wiki/Immediately-invoked_function_expression):
```
var nextID = (function() {
   var id = 0;
   return function() {
   		console.log(++id);
   }
})();
```


## Bind, apply and call function methods

### Question b1: Write `sum` function

This function must meet conditions:

```
typeof sum(1) === 'function'
typeof sum(1)(2) === 'function'
typeof sum(1)(2)() === 'number'

sum(1)() === 1
sum(1,2)(3)() == 6
sum(1,2)(3,4)() === 10
```

**Answer**

```
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


## Hoisting in Javascript

### Question h1: Explain what is hoisting in Javascript

**Answer**

[W3School](https://www.w3schools.com/js/js_hoisting.asp) Hoisting is JavaScript's default behavior of moving declarations to the top. In JavaScript, a variable can be declared after it has been used. In other words; a variable can be used before it has been declared.

### Question h2: What will output the following code and why:

```
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

Console will output :
```
10
```


### Question h3: What will output the following code and why:

```
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

Console will output :
```
1
```

# Contributing

I would be thankful for your [issues](https://github.com/ufocoder/javascript.interview/issues) and [pull requests](https://github.com/ufocoder/javascript.interview/pulls)
