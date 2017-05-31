# JavaScript classes
Unlike most formal OOP languages, JS didn't suport classes and classical inheritance as the primary way of defining similar and related objects when it was created  
ECMAScript 6 now supports them  

---

basic class declaration:  
```javascript
class PersonClass {
    constructor (name) {
        this.name = name;
    }
// no commas between elements
    sayName() {
        console.log(this.name);
    }
}

let person = new PersonClass('Joey');
person.sayName(); // -> 'Joey'

console.log(person instanceof PersonClass); // -> true
console.log(person instanceof Object); // -> true
console.log(typeof PersonClass); // -> function
console.log(typeof PersonClass.prototype.sayName); // -> function
```
  - read-only
  - not hoisted (works like let)
  - automatically in strict mode 
  - methods are nonenumerable, methods lack an internal `[[Construct]]` method
  - calling the constructor without `new` throws an error
  - attempting to overwrite the class name within a class method throws an error