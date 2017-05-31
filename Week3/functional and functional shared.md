# Functional and functional shared

2-day sprint on data structures  
building functions that spit out data structures  
stacks, queues and sets  - study closures some more
releasing screencasts of lectures  
spiking is an exploratory way of working on your own before pairing

---
## Learning objectives
  - Fully understand the different ways that you can create objects on JavaScript, together with their pros and cons
  - Learn, throughout the sprint, about the 4 rules of `this` in JavaScript
  - Introduce yourself to data structures

---  
## Creation
Object literals are created on the spot within braces:
```javascript
var obj = {
    name: 'Joey';
}
Empty objects can be filled from within the program via either dot or bracket notation:
```javascript
var obj = {};
obj.name = 'Joey';
```
Values can be accessed the same way too:
```javascript
return obj.name;
// -> Joey
```
Third and fourth methods of creation:
```javascript
var obj = new Object({name: 'Joey'});
var obj2 = Object.create(null);
```

---
## Creating multiple similar objects

### the literal pattern

```javascript
const angelFish = {
    section: 'aquatic',
    species: 'angel fish',
    manager: 'Gertie',
    family: 'fish',
    food: 'angel flakes',
    lifespan: 4,
    orderFood: function(n) {
        return 'Please can we have ' + n + 'packs of ' + angelFish.food;
    }
}

const catFish = {
    section: 'aquatic',
    species: 'catfish',
    manager: 'Gertie',
    family: 'fish',
    food: 'algae wafers',
    lifespan: 20,
    orderFood: function(n) {
        return 'Please can we have ' + n + 'packs of ' + catFish.food;
    }
}

const whitelegShrimp = {
    section: 'aquatic',
    species: 'whiteleg shrimp',
    manager: 'Gertie',
    family: 'invertebrate',
    food: 'shrimp paste',
    lifespan: 2,
    orderFood: function(n) {
        return 'Please can we have ' + n + 'packs of ' + whitelegShrimp.food;
    }
}
// takes a long time to create these object literals
// repetitive and time consuming
// easy to make mistakes or miss out data points
```

### the functional pattern

```javascript
function createNewSpecies (species, family, lifespan, food) {
    const obj = {
        section: 'aquatic',
        manager: 'Gertie',
        family: family,
        species: species,
        lifespan: lifespan,
        food: food,
        orderFood: function (n) {
            return 'Please send ' + n + ' packets of ' + obj.food;
        }
    };
    return obj;
}

const catFish = createNewSpecies('catfish', 'fish', 20, 'algae wafers');
const angelFish = createNewSpecies('angel fish', 'fish', 4, 'angel flakes');
const whitelegShrimp = createNewSpecies('whiteleg shrimp', 'invertebrate', 2, 'shrimp paste');

// much less code
// objects created more quickly
```

### the closure method for private data

```javascript
function createNewSpecies (speices, family, lifespan, food, keycode) {
    const obj = {
        section: 'aquatic',
        manager: 'Gertie',
        family: family,
        species: species,
        lifespan: lifespan,
        food: food,
        orderFood: function (n) {
            return 'Please send ' + n + ' packets of ' + obj.food;
        }
        validateKeycode: function(code) {
            return code === keycode;
        }
    };
    return obj;
}


const whitelegShrimp = createNewSpecies('whiteleg shrimp', 'invertebrate', 2, 'shrimp paste', 4025);

whitelegShrimp.keycode; // returns undefined, out of scope, so private data
whitelegShrimp.validateKeycode(222); // false
whitelegShrimp.validateKeycode(4025); // true

// any methods created on the object are created afresh every time the function is called e.g. 1000s of instances of orderFood
```

### the functional shared pattern

```javascript
function createNewSpecies (speices, family, lifespan, food, keycode) {
    const obj = {
        section: 'aquatic',
        manager: 'Gertie',
        family: family,
        species: species,
        lifespan: lifespan,
        food: food,
        orderFood: sharedMethods.orderFood,
        validateKeycode: sharedMethods.validateKeycode
    };
    return obj;
}

const sharedMethods = {
        orderFood: function (n) {
            return 'Please send ' + n + ' packets of ' + this.food; // use this to refer to the function's owner
        }
         validateKeycode: function(code) {
            return code === this._keycode; // the underscore denotes that this is private
        }
}

const angelFish = createNewSpecies('angel fish', 'fish', 4, 'angel flakes', 4025);

angelFish.keycode;          // undefined
angelFish.orderFood(4);     // ReferenceError unless orderFood refers to this instead of obj
angelFish.validateKeycode(999); // ReferenceError; it's not in scope, a downfall of the functional shared method, but using this can access it

```