# Prototypal Object Creation
What does it mean that objects have prototypes?  
use the Object function to create new objects  
there are prototype functions built into JS, e.g. toString(), hasOwnProperty()  
delegation !== inheritance  
No such thing as inheritance in JS, exists in OOPLs like Java and C#  
don't overwrite properties that live on Object.prototype  
```javascript
Object.prototype.length = function () {
    return Object.keys(this).length;
}
```
```javascript
Object.create(createNewSpecies.prototype);
```