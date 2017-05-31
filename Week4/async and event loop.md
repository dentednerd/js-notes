# Async and the Event Loop

## advanced setTimeout examples:
```javascript
setTimeout(function () {
    console.log(1);
}, 0);
console.log(2);
// what order will they log in?
// 2, 1
```
```javascript
console.log(1);
setTimeout(function () {
    console.log(2);
    setTimeout(function () {
        console.log(3)
    }, 0)
    console.log(4);
}, 0)
console.log(5);
// 1,5,2,4,3
```
Heap  
Stack  
Queue  
Loop

loop pulls from queue to stack

```javascript
function logNums(n) {
    for (var i = 1; i <= n; i++) {
        setTimeout(function () {
            console.log(i);
        }, 500);
    }
}

logNums(5);
// logs 6,6,6,6,6...??
```