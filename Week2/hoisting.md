# Hoisting
How the JS interpreter reads your code in the background

Doesn't get executed line-by-line

1.
```javascript
var a = 'foo';               // defines a global execution context; defines variable a
console.log(a);               
// is there a global variable called a? yes - go ahead and log it to console - console logs 'foo'
```
2.
```javascript
console.log(a);          
// is there a global variable called a? no - ReferenceError: a is not defined
```
3.
```javascript
console.log(a);
console.log('hello');          
// 'hello' will never print to console; the ReferenceError stops the script
```
4.
```javascript
console.log(a);
var a = 'foo';
console.log(a);               
// log reads undefined, foo -- this is hoisting!
var a;                    
// the interpreter will set place in memory for variable a once it knows it's coming up
console.log(a);     
// this will read undefined because variable a isn't defined yet
a = 'foo';               
// now we have a definition for variable a
console.log(a);     
// so console will log 'foo' here

// null has to be explicitly given to a variable; undefined is an empty variable's default state - subtle difference
```
5.
```javascript
animal = 'cat';                    
// defined before it's declared!
var animal;                         
// JS will hoist this line above the first one by setting it in memory before running
console.log(animal);          
// will log 'cat'
```
6.
```javascript 
animal = 'cat';
console.log(animal);
var animal;                         
// this will still run!
```
7.
```javascript
console.log(animal);
animal = 'cat';                                                       // assignment
var animal;                         
// will log undefined               
// declaration
```
8.
```javascript
console.log(animal);
var animal = 'cat';               
// will log undefined
```
9.
```javascript
console.log(animal);
let animal = 'cat';               
// ReferenceError; let and const don't get hoisted! enforcing good practices
// can set linter to disallow var now
```
10a.
```javascript
// function declaration
function foo () {}

// function expression
var foo = function () {}
```
10b.
```javascript
console.log(foo);                         // logs undefined
foo();                                        // TypeError
var foo = function() {
console.log('foo');
}
```
11.
```javascript
console.log(foo);
var foo = function() {...}
foo();                                        // logs 'foo' now
```
12.
```javascript
console.log(foo);
foo();
function foo () {
     console.log('foo');
}                                             // logs [Function: foo], foo -- function has been hoisted
```
13.
```javascript
function bar () {
     console.log(a);
}
bar();
var a = 12;                              // logs undefined
```
---
## Hoisting and scope
```javascript
function foo () {
     bar()

     function bar () {
          console.log('cats');
     }
}

foo();                                   
// will log 'cats'; bar function gets hoisted
```
14.
```javascript
function bar () {
     a = 23;                              // this a is local
     console.log(a);
}

var a = 42;         // this a is global
bar();              //logs 23
console.log(a);     // logs 42

(move the var a = 42 to the bottom, and log will read 23, 23)

(functions will get hoisted before variables)

function add (a,b) {
     console.log(arguments);                    
     // arguments is created by the function keyword... looks like an array
     return a + b;
}

return arguments[0] + arguments[1]          
// would return the same thing

function add () {
     var total = 0;
     for (var i = 0; i < arguments.length; i++) {
          total += arguments[i];
     }
     return total;
}                                                                 
// useful if you don't know how many arguments you'll receive


function increment(num, inc) {               
    // or inc = 1 within arguments ()
     if (!inc) inc = 1;                    
     // or inc = inc || 1; <-- best practice
     return num + inc;
}

console.log(increment(1));
```
---

functions have their own methods

e.g. .call();

```javascript
increment.call(null, 1, 2);                    
// will return 3
```
```javascript
function add () {
     var total = 0;
     for (var i = 0; i < arguments.length; i++) {
          total += arguments[i];
     }
     return total;
}   

var nums = [1,2,3,4];
add.apply(null, nums)               
// turns array elements into separate arguments
// first argument in this case has to be null

```