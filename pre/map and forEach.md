# .map and .forEach
array methods

example:
```javascript
var oldArray = [1,2,3,4,5];
```

## .map mutates the array
```javascript
var newArray = oldArray.map(function(num) {
  return num+3
;});

// returns [4,5,6,7,8]
```

## forEach just returns the array
```javascript
var newList = oldArray.forEach(function(num) {
    return num+3;
});

// returns:
//4
//5
//6
//7
//8
```