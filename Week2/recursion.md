# Recursion
Defining something in terms of itself

There are iterative functions that loop, and there are recursive functions.

```javascript
function log (n, msg) {
     for (let i = 0;i < n; i++) {
          console.log(msg);
     }
}

log(5, 'Logging iteratively');
```
If this were recursive...

     1. Where should it end? The base case
     2. Diminish the counting argument with each recursion (the recursive case) to reach the base case
     3. Then build the functionality around these two scaffolds

```javascript
function log (n, msg) {
     // Base case
     if (n === 0) return;

     // Functionality
     console.log(msg);     

     // Recursive case
     log(n - 1, msg);
}
```
---
```javascript
function sumNumbers(n) {
     if (n  < 2) return n;
     
     return n + sumNumbers(n - 1);
}

sumNumbers(5); // 15
```
---
```javascript
function count (str) {
     if (str.length === 0) return 0;
     return 1 + count(Str.slice(1));
     count(str.slice(1));
}

console.log(count 'hello world');
```
---
```javascript
function reverse (str) {
     // base case
     if (str.length < 2) return str;
     
     // functionality
     let lastChar = str.slice(-1);
     
   // recursive case
     return lastChar + reverse(str.slice(0, -1));
}
```
---
```javascript
function instanceCounter (arr, value) {
     let counter = 0;
     for (let i = 0; i < arr.length; i++) {
          if (arr[i] === value) counter++;

          // recursive call
          if (Array.isArray(arr[i])) counter += instanceCounter (arr[i], value);
     }
     return counter;
}

console.log(instanceCounter([1,2,3,4], 4));
```
---
```javascript
const obj = {
a: 1,
b: 2,
c: {
  d:5,
  e:{
    f:7,
    g:9
  },
  i:9
  }
};

const obj2 = {
d:5,
e:{
  f:7,
  g:9
  },
i:9
}

function traverse (obj) {
     // loop through the object
     // if we encounter a nested object, recursively pass on that part of the problem to the traverse function
     for (let key in obj) {
          if (typeof obj[key] === 'object') {traverse(obj[key])}
          else {console.log(obj[key]);}
}
```
---
```javascript
function search (obj, searchTerm) {
     for (let key in obj) {
          // is it the primitive value I'm looking for?          
          if (obj[key] === searchTerm) return true;

          // do we need to pass the problem on?
          if (typeof obj[key] === 'object') {
               const found = search(obj[key], searchTerm);
               if (found) return true;          
     }
     return false;
}
```