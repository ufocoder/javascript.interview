# Javascript Closure Interview Questions

1. Given the following closure, what would be a possible implementation of `makeAdd` function?
```js
const addTwoThings = thingToAdd(2);
addTwo(3); // -> 5

const addTwoThings = thingToAdd(10);
addTwoThings(30); // -> 40
```


_One Solution_
```js
const makeAdd = (x) => (y) => x + y;
```
