# .sort
```javascript
var array = [1, 12, 21, 2];

array.sort(function(a,b) {return b - a;});
// returns [21,12,2,1]

array.sort(function(a,b) {return a - b;});
//returns [1,2,12,21]
```