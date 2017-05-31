# Pure functions
## What is a pure function?
A pure function doesn't depend on and doesn't modify the states of variables outside of its scope  
Always returns the same result given the same parameters  
Its execution doesn't depend on the state of the system  
They don't have any side effects outside of themselves  
input -> process -> output

Types of functions:
  - mapping (most likely to be pure function)
  - process
  - i/o (input/output)

```javascript
function double (num) { return 2 * num; }
double(2)   // 4
```

```javascript
function mouseOnLeftSide (mouseXPosition) {
    return mouseXPosition < window.innerWidth / 2;
}

function mouseOnLeftSide (mouseXPosition, windowWidth) {
    return mouseXPosition < windowWidth / 2;
}
// which one is pure?
```

## Why use pure functions?
  - predictability
  - testability
  - reusability
  - self-documentation
  - concurrency (threading)
  - asynchronicity

```
  Object.assign()
```
starts on the left;

```javascript
function cap (arr) {
    return arr.map(function(item, i) {
        return Object.assign({}, item, {
            type: item,.type.toUpperCase()
        })
    })
}
```
```javascript
function sayHi (name1, name2, name3) {
    console.log('Hi ' + name1, name2, name3);
}

sayHi.call(null, 'Daryl', 'Sam', 'Harriet')    // always use .call with the first argument as null, for now

sayHi.apply(null, ['Daryl', 'Sam', 'Harriet'])  //  .apply expects an array whereas call expects a comma-separated list

var sayHiDaryl = sayHi.bind(null, 'Daryl', 'Sam', 'Harriet')    // .bind binds the function to a variable that can then be called as a function
```

```javascript
function once (fn) {
    // know if it's been called
    // return answer if not called
    var called = false;
    // higher order function and closure
    return function() {
        if (!called) {
            called = true;
            return fn.apply(null, arguments);
        }
    }
}

var res = once();
res();