# .filter

example:
```javascript
var arr = [1,2,3,4,5,6,7,8,9,10];
```
## to filter numbers 5 or less:
```javascript
var lessThanFive = arr.filter(function(num) {
  return num <= 5;
});
// returns [1,2,3,4,5]
```
## to filter even numbers:
```javascript
var evens = arr.filter(function(num) {
  return (num%2 === 0);
});
//returns [2,4,6,8,10]
```