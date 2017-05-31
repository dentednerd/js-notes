# .some and .every
array methods

example:
```javascript
var ages = [3, 10, 18, 20];
```
## .some
```javascript
ages.some(function(age) {
    return age >= 18;
});
//returns true; some of these values are 18 or over
```
## .every
```javascript
ages.every(function(age) {
    return age >= 18;
});
//returns false; not all of these values are 18 or over
```