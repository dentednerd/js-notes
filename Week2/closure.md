# Closure (Mauro's lecture notes)

Importance of scope and closure, understand the mechanics and the importance of them. If you don’t understand scope and closures, you are a junior developer, no matter how long you’ve been coding.


### Understanding Scope
Scope collects and maintains a look-up list of all the declared identifiers and enforces a strict set of rules as to how these are accessible to currently executing code. Different execution contexts have different variables in scope.


Recap: What variables are in scope? What will be shown?

```
var a = 8;
                    
function foo (a) {                         // this a is different to the global a set at the top
  a = 15;
}

function bar () {                         // impure function!
  a = 20;
}

bar();

foo(a);

console.log(a);                              // logs 20

```

### Lexical Scope
Scope based on where variables and blocks of code (code surrounded by `{}`) are authored, by the programmer, at write time, and thus is set in stone for the execution of the program.

**important** Start getting used to reading your code with its lifecycle in mind. Your code won’t necessarily execute in the order you wrote it.

### Collision Avoidance
Collision of identifiers results often in unexpected overwriting of values.


## Closure Enlightenment
Closure is not a special feature of the language that you choose to use when convenient. Closure is all around you in JavaScript, you just have to recognise it and embrace it. Closure happens as a result of writing code that relies on lexical scope. It just happens.

Look at this:

```javascript
function foo () {
  bar a = 5;
  function bar () {
    console.log(a);
  }

  bar();
}

foo()

```

Anything surprising? Nothing special, this is just scope in action.

Now look at this:

```javascript
function foo() {
  var a = 2;
  function bar() {
    console.log(a);
  }
  return bar;
}

var baz = foo();
baz(); // 2
```

`bar` has lexical scope access to the inner scope of `foo`. But then, we take `bar`, the function itself, and pass it as a value. In this case we `return` the function object itself that `bar` references.

After we call `foo`, we assign the value it returned (our inner `bar` ) to a variable called `baz`, and we actually invoke `baz`, which of course is invoking our inner function `bar`, just by a different identifier.

`bar` is executed, but outside of its declared lexical scope.

After `foo` executed, normally we would expect that the entirety of the inner scope of `foo` would go away, because we know that the engine employs a Garbage Collector that comes along and frees up memory once it’s no longer in use. Since it would appear that the contents of `foo` are no longer in use, it would seem natural that they should be considered gone.

But the “magic” of closures does not let this happen. That inner scope is in fact still “in use”, and thus does not go away. Who’s using it? The function `bar` itself, which we know in the global execution context as `baz`.

**Important:** `baz` still has a reference to its lexical scope, and that reference is called closure.

The function is being invoked well outside of its author-time lexical scope. Closure lets the function continue to access the lexical scope it was defined in at author-time.

**Definition:** Closure is when a function is able to remember and access its lexical scope even when that function is executing outside its lexical scope.

**Definition:** A closure is a function bundled together with references to  it’s surrounding state (lexical environment/scope). Simply define a function inside another function and expose the inner function. The inner function will have access to the variables in the outer function’s scope. Forever.

**Definition:** A closure is a stateful function. We usually think of functions as use once and discard pieces of code. Once they finish executing they are as good as dead. We can use them again, but they always start from a blank slate. With closure we can make functions “remember” the environment in which they were created.

Look back at this:

```javascript
function foo() {
  var a = 2;
  function bar () {
    console.log(a); // 2
  }
  bar ();
}
foo();
```

`bar` has access to the variable `a` in the outer enclosing scope because of lexical scope. Is this “closure”?

Maybe, but not exactly. Access via lexical scope is only part of what closure is. Technically speaking, `bar`  has a closure over the scope of `foo` . But, closure defined this way is not directly observable, because when we call `bar` we're still in the scope where `a` is accessible and we aren't witnessing anything surprising. What differentiates closure is what happens when you call `bar` somewhere else, where you might not expect it to have closure over `a`. 

## A useful example and a new principle

Here's an example of a function that returns a function which may only be called once:

Let's write a function that returns a copy of a function:

```javascript
function copy (func) {
  return function () {
    return func();
  };
}

function logger () {
    console.log('Hello world');
}

var singleLog = copy(logger);

singleLog();  // Hello world
singleLog();  // Hello world
```

Let's extend this to something useful. Let's make it so that the copied function can only be called once, after that it doesn't work.

```javascript
function callOnceOnly (func) {
  var isFirstTime = true;

  return function () {
    if (isFirstTime) {
        isFirstTime = false;
      return func();
    }
  };
}

function logger () {
    console.log('Hello world');
}

var singleLog = callOnceOnly(logger);

singleLog();  // Hello world
singleLog();  
```

Can we access `firstTime`?
Can someone change it from the outside?

In what lexical scope is `singleLog` called?
In what lexical scope is `singleLog` defined?

### Principle of Least Privilege
In the design of software, you should expose only what is minimally necessary and hide everything else.

Of course, any of the various ways that functions can be passed around as values, and indeed invoked in other locations, are all examples of observing/exercising closure.

```javascript
  function createMultiplier (m) {
    return function (n) {
      return m * n;
    };
  }
  var double = createMultiplier(2);
  var triple = createMultiplier(3);
  double(5); // 10
  triple(5); // 15
```

In this example, the anonymous function that we return has closure over the scope of `createMultiplier`

```javascript
  var createSecret = function (secret) {
    var secretHolder = {
      check: function (word) {
        return word === secret;
      }
    }

    return secretHolder;
  }

  var postItNote = createSecret('12345');

  postItNote.check('12345'); // true
```

In this example, the `.check` method is defined inside the scope of `createSecret` , which gives it access to any variables from `createSecret()`  and makes it a privileged method (i.e. it has access to private data through closure).


### Example:
Underscore’s `once()` and `after()`

### Sources:

- [Kyle Simpson’s YDKJS: Scope & Closures](https://github.com/getify/You-Dont-Know-JS/blob/master/scope%20%26%20closures/ch5.md)
- [Master the JS Interview: What is a Closure? by Eric Elliot](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-closure-b2f0d2152b36#.szp9dswih)