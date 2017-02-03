Javascript Interview
====================

This documents contains the most actual and important questions for Javascript developer position. 
It will helps you to compose question list for your own interview or prepare to inverview.

Table of contents:

* [Inheritance in Javascript](#inheritance-in-javascript):
   * [What will output the following code](#question-1-what-will-output-the-following-code-and-why)
* [Closure in Javascript](#closure-in-javascript):
    * [What is Closure in Javascript?](#question-1-what-is-closure-in-javascript)
    * [What will output the following code](#question-2-what-will-output-the-following-code-and-why)
    * [Resolving example of problem code](#question-3-resolving-example-of-problem-code)
    * [Write nextID function](#question-3-resolving-example-of-problem-code)

## Inheritance in Javascript

### Question 1: What will output the following code and why:
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

### Question 1: What is Closure in Javascript?

[MDN definition](https://developer.mozilla.org/en/docs/Web/JavaScript/Closures):
Closures are functions that refer to independent (free) variables (variables that are used locally, but defined in an enclosing scope). In other words, these functions 'remember' the environment in which they were created.

[Javascript.isSexy](http://javascriptissexy.com/understand-javascript-closures-with-ease/): A closure is an function that has access to the outer (enclosing) function’s variables-scope chain.


### Question 2: What will output the following code and why:

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

    innerFunction();
}

outerFunction();
```

**Answer**

Console will output `true`

### Question 3: Resolving example of problem code

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

### Question 4: Write `nextID` function that will generate ID incrementally after each calling
There's an exmpale of function output:
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

# Contributing

I would be thankful for your [issues](https://github.com/ufocoder/javascript.interview/issues) and [pull requests](https://github.com/ufocoder/javascript.interview/pulls)
