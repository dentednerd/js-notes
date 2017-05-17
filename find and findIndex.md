# find and findIndex

## find

```javascript
var ages = [3, 10, 18, 20];
ages.find(function(age) {
    return age >= 18;
});
//returns 18; first value in array to match condition
```

## findIndex

```javascript
ages.findIndex(function(age) {
    return age >= 18;
});
//returns 2; index of first value in array to match condition
```
