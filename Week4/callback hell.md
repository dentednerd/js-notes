# Callback HELL AAAAAGH
yo dawg, i heard you like JS so i put callbacks in your callback so you can callback while you callback -- Xzibit  
callbackhell.com  

## async conditions to think about
Race conditions - where the code is dependent on the order in which the information comes back  
Nesting - a set of tasks with a known set of instructions that need to be run sequentially  

```javascript
[1, 2, 3, 4, 5]
// in series
// in parallel

function asyncEcho(data, cb) {
    setTimeout(function () {
        cb(null, data);
    }, Math.random() * 1000);
}

asyncEcho(1, function (err, data) {
    console.log(data);
    asyncEcho(2, function (err, data) {
        console.log(data);
        asyncEcho(3, function (err, data) {
            console.log(data);
            asyncEcho(4, function (err, data) {
                console.log(data);
                asyncEcho(5, function (err, data) {
                    console.log(data);
                })
            })
        });
    });
});
// AAAAAAAAAAAAA
// in series

asyncEcho(1, function (err, data1) {
    asyncEcho(2, function (err, data2) {
        asyncEcho(3, function (err, data3) {
            asyncEcho(4, function (err, data4) {
                asyncEcho(5, function (err, data5) {
                    console.log(data1, data2, data3, data4, data5);
                })
            })
        });
    });
});
// ...booyah?
// in parallel

function log(err, num) {
    console.log(num);
}

asyncEcho(1, log);
asyncEcho(2, log);
asyncEcho(3, log);
asyncEcho(4, log);
asyncEcho(5, log);
// doesn't guarantee that they'll log in order

function log1To5() {
    asyncEcho(1, log);
    asyncEcho(2, log);
    asyncEcho(3, log);
    asyncEcho(4, log);
    asyncEcho(5, log);
}
// still not guaranteed...

function log1To5() {
    var nums = [];
    asyncEcho(1, function log (err, num) {
        nums.push(num);
        if (nums.length === 5) {
            console.log(nums);
        }
    });
    asyncEcho(2, function log (err, num) {
        nums.push(num);
        if (nums.length === 5) {
            console.log(nums);
    });
    asyncEcho(3, function log (err, num) {
        nums.push(num);
        if (nums.length === 5) {
            console.log(nums);
    });
    asyncEcho(4, function log (err, num) {
        nums.push(num);
        if (nums.length === 5) {
            console.log(nums);
    });
    asyncEcho(5, function log (err, num) {
        nums.push(num);
        if (nums.length === 5) {
            console.log(nums);
    });
}
log1To5();
// doesn't even log all the numbers without the if logic
// with the if statement, all 5 will be returned but still not in order
```

## async.js
package for NPM

```javascript
var async = require('async');
var newNums = [];
async.map([1, 2, 3, 4], function(item, callback) {
    callback(null, 2 * item);
}, function (err, results) {
    console.log(results);
});
// -> [2, 4, 6]

function asyncDouble(num, cb) {
    setTimeout(function () {
        cb(null, 2 * num);
    }, Math.random * 500);
}
```
