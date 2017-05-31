# .reduce

## Mauro's tutorial:
our array:
```javascript
var nums = [1,2,3,4,5];
```
### to find the sum of all values in the array:
```javascript
var sum = nums.reduce(function(accumulator, num) {  // num == element
  return accumulator + num;
}, 0); // the 0 initialises the accumulator
```
### to double all values in the array:
```javascript
var doubles = nums.reduce(function (acc, num) {
  acc.push(num * 2);
  return acc;     // always return the accumulator!
  //OR return acc.concat(num * 2);
}, []);

//can't use "return acc.push(num * 2)" b/c .push returns length of array
```
### to find all even values in the array:
```javascript
var evens = nums.reduce(function (acc, num) {
  if (num % 2 === 0) {
    acc.push(num * 2);
  }
  return acc;
}, []);
```

### counting votes for the best football team:
```javascript
var votes = ['City','City','United','United','United','City','Bolton','United','Barcelona'];

var tally = votes.reduce(function(acc, team) {
  //check if acc has team
  if (acc[team]) // OR if (acc.hasOwnProperty(team)) {
    //if yes, add 1
      acc[team]++; 
      } else {
    //if no, set to 1
      acc[team] = 1; }
  return acc;
}, {})
```
### to add up all values below 100 in this array:
```javascript
var nums = [123,4,56,78,910,1112,13,14,151617,18,100]

var sumBelow100 = nums.reduce(function (acc, num) {
  if (num < 100) {
    acc += num;
  }
  return acc;
}, 0)

//or ternary operator: return num < 100 ? acc + num : acc;
//ternary operators are one-line if-else statements
// if statement ? if yes do this : if no do this
```
### reducing names:
```javascript
var names = ['Joey','Timmy','Rob','Charley','Hannah','Dorron']

var longNames = names.reduce(function (acc, name) {
  if (name.length >= 5) {acc.push(name.toUpperCase());}
  return acc;
}, [])

//OR return name.length >= 5 ? acc.concat(name.toUpperCase()) : acc;

var isLong = names.reduce(function (acc, name) {
  return name.length > 5 ? return acc = true; : acc; 
}, false)

//OR:
  if (acc) {
    return true;
  } else {
    return name.length > 5;
  }
```  
### chaining math functions:
```javascript
function increment(input) {return input + 1};
function decrement(input) {return input - 1};
function double(input) {return input * 2};
function halve(input) {return input / 2};

var functions = [increment, double, decrement, halve];
var result = functions.reduce(function (acc, fn) {
  return fn(acc);
}, 1);
// -> 1.5
```
### reduce without an accumulator:
```javascript
var array = [4,5,6,7,8];
var singleVal = 0;
singleVal = array.reduce(function(prevNum, currNum) {
  return prevNum + currNum;
});
// returns 30
```
----------
## Fun Fun Functional's Moar Reduce video:
```javascript
var text = "mark johansson\twaffle iron\t80\t2\nmark johansson\tblender\t200\t1\nmark johansson\tknife\t10\t4\nnikita smith\twaffle iron\t80\t1\nnikita smith\tknife\t10\t2\nnikita smith\tpot\t20\t3"

var output = text
                .trim()
                .split('\n')
                .map(function(line) {return line.split('\t');})
                .reduce(function(customers, line) {
                    customers[line[0]] = customers[line[0]] || [];
                    customers[line[0]].push({
                        name: line[1],
                        price: line[2],
                        quantity: line[3]
                    })
                    return customers;
                }, {})
                console.log(output);

/* returns:
{
  mark johansson: [ {
  name: "waffle iron",
  price: "80",
  quantity: "2"
},  {
  name: "blender",
  price: "200",
  quantity: "1"
},  {
  name: "knife",
  price: "10",
  quantity: "4"
}],
  nikita smith: [ {
  name: "waffle iron",
  price: "80",
  quantity: "1"
},  {
  name: "knife",
  price: "10",
  quantity: "2"
},  {
  name: "pot",
  price: "20",
  quantity: "3"
}]
}
*/
```