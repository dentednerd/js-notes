# Sorting
### stable sort vs unstable sort:  
stable sort: if the algorithm finds values in the place that they should be, the sort will leave them where they are  
unstable sort: puts elements in unpredictable order

expectation of input; want to avoid overflow with large inputs

---
## Bubble sort
Completely useless in the real world

```javascript
[7, 2, 5, 4, 1, 3, 6]
// loops over array and compares current val with next val
// if out of order, switch
// if in order, continue
// is 7 less than 2? no
// switch 7 and 2 around
[2, 7, 5, 4, 1, 3, 6]
// by the end of the search, 7 will have bubbled up to the end of the array
// is 2 less than 5? yes, stays in place
// is 5 less than 4? no, so it bubbles up
[2, 4, 1, 3, 5, 6, 7]
// 4 is next value to bubble
```

In this case, use a `while` loop, because you don't know how many times you'll need to loop through the data  
Complexity is higher than O(n), worst case scenario is O(n^2)
A `for` loop is necessary inside the `while` loop

---
## Selection sort
Closest to how you would sort by hand

```javascript
[5, 1, 3, 4, 2]
// 5 is the new smallest one
// then 1: 1 is the new smallest one!
// then 3: 3 is not the smallest one
// then 4: 4 is not the smallest one
// then 2: 2 is not the smallest one, but is smaller than the others - it's the next smallest one
```

---
## Quicksort
Recursive  
Introduces the concept of a pivot

```javascript
[5, 1, 3, 2, 4]
// choose the last element as the pivot
var pivot = 4;
// create two new arrays, one of numbers bigger than pivot, one of numbers smaller than pivot
[1, 3, 2] [5]
// 5 doesn't need sorting, it's only one element
// recursively run function on left array
quickSort(left).concat(pivot).concat(quickSort(right));
```
Worst-case scenario would be to either sort an already sorted array, or to pick a pivot at either end of an array
```javascript
// advanced quicksort
//grabs first, middle and last item of array and uses middle item as pivot
[5, 1, 3, 2, 4]
// 4 is the pivot
[1,3,2] 4 [5]
```
Complexity between O(n) and O(log^n)  
Could blow the stack with recursion