# Big O Notation and Algorithms
sprint today on array algorithms  
Monday's sprint on data structures  
another sprint on searching objects

---
## What is an algorithm?
any program is an algorithm  
today looking at binary search  
computer science is a science of trade-offs; sometimes the most efficient code is not the best code for the situation  
always err on the side of readability; code is for people to read, not computers!

## Big O notation
how do you measure if one algorithm is faster than another? time!  
depends on the size of the inputs that it receives though  
```
f(x) = x^2 + x + 1
f(2) = 4 + 2 + 1 = 7
f(10) = 100 + 10 + 1 = 111
f(100) = 10000 + 100 + 1 = 10101
```
Big O only cares about the orders of magnitude, the x^2 part of the algorithm  

```javascript
[2, 4, 1, 7, 5]
// we want to find 1
// is 2 === 1? no
// is 4 === 1? no
// is 1 === 1? yes, found it on step 3
// but what if there are a million items in the list?
```
the worst thing that could happen is that we'd need to look at all the items in the input  
```
O(n)
// this is linear, size of input directly proportional to operations
```
another example:
```javascript
[2, 3, 7, 1, 5, 6]
// we want to find pairs of numbers in this array that add up to 8
// fix on one number, then loop over the rest to see which adds to 8
for (var i in nums) {
    var a = nums[i];
    for (var j in nums) {
        var b = nums[j];
        if a + b === sum return foo;
    }
}
```
you would need to run this algorithm n^2 times  
O(n^2) grows exponentially  
what could be a better algorithm than n?  
could have an algorithm that's slow for small inputs, but super fast for big inputs  
we want something between O(1) and O(n)  

---
## the travelling salesman problem
What is the shortest path between all the points?  
To start, there are 7 options
From the first point, there are 6 options
From the second, 5 options
From the third, 4 options...
```
7 + 6 + 5 + 4 + 3 + 2 + 1
// factorial of 7
O(n!)
```
The worst option for an algorithm, even worse than O(n^2)!

---
First sprint today: simple search  
Assumptions can reduce complexity of algorithms (provided it's a correct assumption)  
for example, a sorted list of numbers  
e.g. guess the number from 0  to 100 -- takes around 7 guesses
can do it in three guesses for a number less than 10  
halving the input with every guess, narrowing it down  
a logarithm, the inverse of squaring a number
if 2^2 = 4, log2 4 = 2, log2 8 = 3
```
O(log2n)
```
---
whiteboarding a problem is really useful

Make it work  
Make it right  
THEN make it fast