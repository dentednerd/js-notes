# The Four Rules of .this
https://www.youtube.com/watch?v=zE9iro4r918

## 1. Implicit Binding
left of the dot at call time  
```javascript
var me = {
    name: 'Joey',
    age: 32,
    sayName: function() {
        console.log(this.name);
    }
}
// -> "Joey"
```
```javascript
var sayNameMixin = function(obj) {
    obj.sayName = function() {
        console.log(this.name);
    }
};

var me = {
    name: 'Joey',
    age: 32,
}

var you = {
    name: 'Charley',
    age: 8
}

me.sayName();       // -> "Joey"
you.sayName();      // -> "Charley"
```
```javascript
var Person = function(name, age) {
    return {
        name: name,
        age: age,
        sayName: function() {
            console.log(this.name);
        },
        mother: {
            name: 'Stacey',
            sayName: function() {
                console.log(this.name);
            }
        }
    };
};

var jim = Person('Jim', 42);
jim.sayName();              // -> "Jim"
jim.mother.sayName();       // -> "Stacey"
```

---

## 2. Explicit Binding
using .call, .apply and .bind

```javascript
var sayName = function() {
    console.log('My name is ' + this.name);
};

var joey = {
    name: 'Joey',
    age: 32
};

sayName.call(joey);     // -> "My name is Joey"
```

---

## 3. new Binding

---

## 4. Window Binding