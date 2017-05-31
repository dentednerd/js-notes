# Async
this week entirely on asynchronous programming  
project phase is now 2 weeks  
now booking one-on-ones rather than being called out for them  

---

## What is asynchronicity?
Where a piece of code will be run at some point in the future  
code written in an order will not necessarily execute in that order

### Sources of asynchronicity:
1. user interactions (event handlers)
2. network I/O (making requests to o(ther sites)
3. disk I/O (making requests to local storage)
4. IPC - interprocess communication i.e. web workers
5. timers

### examples of setTimeout:

```javascript
setTimeout(function() {
    console.log('woo');
}, 1000);
// last argument is time in milliseconds
```
```javascript
console.log(1);
setTimeout(function () {
    console.log(2);
}, 1000);
console.log(3);
// what order will they run in?
// 1, 3, 2
```
```javascript
console.log(1);
setTimeout(function () {
    console.log(2);
    setTimeout(function () {
        console.log(3);
    }, 1000);
    console.log(4);
}, 1000);
console.log(5);
// what order will they run in?
// 1, 5, 2, 4, 3
```

---

### examples of a click event:
```javascript
document.getElementById('test').addEventListener('click', function () {
    console.log('I was clicked');
});
```

---

## What are callbacks?
can be synchronous and asynchronous  
functions that may be executed at some point in the future
forEach is a synchronous callback

```javascript
function getTweets() {
    setTimeout(function() {
        return {tweets: ['lonely tweet']};
    }, 1000);
}

console.log(getTweets());
// undefined

function getTweets(cb) {
    return setTimeout(function() {
        cb(null, {tweets: ['lonely tweet']});
    }, 1000);
}

console.log(getTweets());
// returns Timeout object

getTweets(function (err, tweets) {
    if (err) {console.log('IT\'S GONE BAD')}
    else {console.log(tweets)};
}) // <- callback function, error-first callback
// eventually returns tweets object
```
```javascript
function fakeDbRequest() {
    setTimeout(function () {
        return 5;
    }, 1000);
}
// pass it a callback to get it to work
function fakeDbRequest(cb) {
    setTimeout(function () {
        cb(null, 5;
    }, 1000);
}
fakeDbRequest(function(err, num) {

});

// use done(); and it('bla', function (done) {}) with Mocha to stop it waiting for tests; Mocha only waits 2000ms for async requests
```
sprint!