# Javascript is weird

## Tricks and mysteries!

So in this lesson we are going to look a couple of tricks and mysteries. Let’s go!

### #1 IIFE

```jsx
const result = (function(a) {
  return a*a;
}(5.5));
console.log(result);
```

We have in the console ***30.25.***

This is because if you create a function and then involves into a parentheses and then we call the function automatically the result is generate just like this 👇🏻

```jsx
const result = a => a * a;  
console.log(result(5)) //output is the same
```

### #2 Rest parameters

```jsx
const b = [1, 2, 3];
const f = (a, ...b) => a + b;

console.log(f(1));
```

The output in console is **“1” as string** and this is because 3 reasons: 

1. Although we create a variable b and in the function is summated with a, doesn’t work, and this is because have rest parameter b.
2. Coercion in js
3. The rest parameter is just like an empty array but if you put data into the function work with the same data: 
    
    ```jsx
    const f = (a, ...b) => {console.log(b)}; //output: [10, 20, 40, 50]
    
    console.log(f(1, 10, 20, 40, 50));
    ```
    

So in this case we don’t have data and the behavior on the function is just like this: 

```jsx
console.log(1 + []) //output: '1'
```

### #3 Rest parameters, “legacy js” and methods

```jsx
const f = (...f) => f;
console.log(f(10));

const f = (...f) => f.reduce(f => f);
console.log(f(10));

function ff() {
  return arguments;
}
console.log(ff(10));

const f = f => f;
console.log(f(10));
```

The output is: [10], 10, [10], 10

1. First example: 
    1. We have an 10 as parameter but **rest parameter**, rest parameter is array and so therefore the output is [10]
2. Second example: 
    1. Reduce method sums all parameters in one variable just like this 
    
    ```jsx
    f.reduce((sum) => 0 + 10) // arr = [10] output: 10
    f.reduce((sum) => 0 + 10 + 20 + 40 + 50) //arr = [10, 20, 40, 50] output: 120
    ```
    
3. Third example: 
    1. Before ES6 we don’t have rest parameters and was our alternative, all parameters might be received in arguments object, but just like rest parameter, was an object 
    
    ```jsx
    console.log(ff(10)) // [10]
    console.log(ff(10, 20, 30, 40, 50)) // [10, 20, 30, 40, 50]
    ```
    
4. Fourth example: 
    1. Just like “normal javascript” it is strictlyt he same. Only an object, array, number, boolean, or string.

### #4 Field block and field global

```jsx
var foo = 10;
let bar = 3;
(function () {
  var foo = 2;
  bar = 1;
})()
bar = bar + foo;
console.log(bar);
```

The output is: 11

If into a IIFE just call to foo and no create the output will be 3, but in this case just reasigne bar to 1, and then sum with foo in global field. 10 + 1 

### #5 Don’t use var

```jsx
var x = 5;

(function () {
    console.log(x);
    var x = 10;
    console.log(x);
})();
```

Output is: undefined and 10

If I no create a new variable the output would be: 5, 5, but detect a new variable with the same name and TDZ (the death zone ([concept I learned in this course of js!](https://www.udemy.com/course/the-complete-javascript-course/)) or “hoisting”) is present, doesn’t have access to variables before creating them. And then second console shows new variable call x (10)

If we are use let then the output would be uncaught error, and this is best to undefined (prevent errors in production)

### #6 Numbers in js!

```jsx
console.log(0.1 + 0.2);
console.log(0.1 + 0.2 === 0.3);
console.log(9007199254740993 === 9007199254740992);
```

The output is: 0.3000000000000004, false and true.

Numbers in js are represented as [double-precision 64-bit binary format IEEE 754](https://medium.com/dailyjs/javascripts-number-type-8d59199db1b6) values, this would be generate errors equalitys, [Number.EPSILON](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/EPSILON) should be used to compare rounding values in strictly  equality. 

### #7 Chained compared

```jsx
console.log(1 < 2 < 2);
console.log(3 > 2 > 1);
```

The output is: true, false

How we learned, false is equal to zero and true is equal to 1, now we refresh that: 

We have our first value: 

```jsx
1 < 2 /* < 2 */ //true or one then
/* 1 <  2  => true => 1 */ 1 < 2 // false or zero
```

So, I hope this make sense 

```jsx
true >= 1 // true 
true > 1 // false
false >= 0 // true
false > 0 // false
10 > 100 > -1 // true
400 < 500 < 400 // true
```

So, I hope all of this you help it so much, thank you very much for read😊