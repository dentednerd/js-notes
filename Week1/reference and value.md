# Reference and value
```javascript
var a = 3
var b = a

>a
3

>b
3

>b++
3

>b
4

>a
3                                   
// primitive values aren't affected by change to another variable -- a holds a different 3 to b's 3
```
---
```javascript
var a = [1,2,3]
var b = a

>a
[1,2,3]
>b
[1,2,3]
>a.push(4)
4
>a
[1,2,3,4]
>b
[1,2,3,4]                         
// objects are affected as the two variables point to the same object -- a and b both point to the same array [1,2,3,4]

// a wants what's in his lunchbox, even though b has the same in her lunchbox!
```
---
```javascript
function doubleArray (arr) {
     for (var i = 0; i < arr.length; i++) {
          arr[i] = arr[i] * 2;
     }
     return arr;
}

var original = [1,2,3]

var doubles = doubleArray(original);

console.log('doubles: ' + doubles);
console.log('original: ' + original);                
// both log the same array, because original has been changed too
```
---
```javascript
choosing to be immutable:

function doubleArray (arr) {
     var arr = arguments[0];
     var result = [];
     for (var i = 0; i < arr.length; i++) {
          result.push(arr[i] * 2 )
     }
     return result;
}

var original = [1,2,3];
var doubles = doubleArray(original);

console.log('doubles: ' + doubles);
console.log('original: ' + original);               
// now they don't log the same array
```
---
```javascript
function identity (x) {
     return x;
}

var input = {name: 'Mauro'}
var output = identity(input);
console.log(input === output)                    // would be true

expect (identity(input)).to.equal(input)          // not to.eql!!!
```