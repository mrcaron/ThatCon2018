# Functional Javascript

John Ptacek, @jptacek, https://jptacek.com

## Intro

JS can do just about anything, lots of styles: procedural, oo, functional (especially with [ES6](https://es6.io/)). Developers need to challenge themselves to think functionallly, the language doesn't necessarily provide tools to do it.

### What

Paradigm/style in which computation is application of functions that supports and encurages the style. Like Lisp, Haskell, Erlang, F# are Functional languages.

Think math. It's going to do the one thing.

    f(x) = x + 1
    f(3) = 4
    cos(pi) = -1

It's not for all the things.

* Imperative - do this, then that
* OO - methods change state

It's good for:

* Stateless (FAAS; functions as a service; azure functions, google functions, etc)
* Algorithms
* Data Analysis & Transformation
* Testing

Not good for: (me: why?)

* State Machine
* Speed
* Learning Curve

### Highlights

* Eval of math functions
* MAIN DEAL: Avoid mutable state
* Referential transparency; if I call f1, f2 and f3, the order doesn't matter (linq)
* Avoid side effects
* Reusable functions over reusable objects
* Function composition over object composition

### Why

* Less bugs; state tends to create programming issues
* Less complex
* More readable code (b/c declarative)

#### Lambda calculus

Anonymous functions, unary... take one argument, return one value. Sudhagar an informal intro to lambda calc

### Functional Prog

* Functions are first class
  * Functions can have properties/methods
  * Can be passed
  * can be assigned to vars

Functions are called by references using `()`, like using `&` in PS

Clsure, functions have inner embedded functions of any depth; args and vars get captured in (re:Perl).

## Code Examples

First Class

    let fn1 = function() {
        ...
    }
    console.log(fn1);
    // vs
    console.log(fn1());

    let fn2 = function(fntocall) {
        fntocall();
    }

Closures

    const createAdder = (x) => {
        //HOF
        return (y) => x + y;
    }
    const add3 = createAdder(3);
    add3(2); // 5
    add3(3); // 6

    const countPlus = () => {
        let count = 0;
        return () => count++;
    }

    const counting = countPlus();
    // we preserve the value of the counting var in each call with the function being declared

    console.log(counting()); // 0
    console.log(counting()); // 1
    console.log(counting()); // 2

    // when we call the base function each time, var is reinitialized
    console.log(countPlus()()); // 0
    console.log(countPlus()()); // 0
    console.log(countPlus()()); // 0

    const add three numbers = (x) => (y) => { return(z) => x+y+z; }; // fat arrow says "here's a new function"

## Elements of Functional Prog

### Pure functions

returns same output for same input every time. only one result for any given set of args. reliable. Pure functions don't take into consideration anything from a scope outside itself. A lot of this is taken from old Perl stuff. YAPC (Secrets of the Ivory Tower).

| what's `const` vs `let` ?

* breaks purity: Changing variable property data structure globally, anytime you affect something outside the fn
* results are easy to reproduce and test
* can be called in parallel without altering results (no race cond)
* Memoization (caching)

### HoF

these are callbacks; functions can be template functions.

### ES5  - Map, Filter, Reduce

ES5 is the "official" js standard, ES6 is the next edition. Map, Filter, Reduce... these are Functional use concepts for composure.

#### Map

Used to apply a function on every element in an array. A foor loop for transforming values. Operates on collections with a function and returns a new collection.

    // map to create objects, i can be passed in
    newObject = arr.map( (val, i) => {
        return {value: val, loc:i};
    })

#### Filter

Again, like grep. Operates on a collection of size n, returns a new collection of n-x, where x = [0..n.length]

    let newArr = arr.filter((val) => {
        return val %2 == 0;
    })

#### Reduct

think accumulator

    let sumValue = oldArr.reduce( (acc, value, index, array) => {
        // return operation
    }, 0 /* default */);

    const sumInitValue = arr.reduce( (acc,value) => {
        return acc+value;
    }, 100);

    // we have functions, we can make it more intersting
    const average = arr.reduce((total, value, index) => {
        total += value;
        if (index === arr.length =1) {
            return total / arr.length;
        }
        else {
            return total;
        }
    });

| Javascript
| data = require('./data/periodic.json')
| // pulls in json data!

### Immutability

Not changing object state.

    let result = [1,2,3]
    .map ( x => x+1)
    .filter (x => ...)

### Currying

Reduces functions of multiple args to functions of one arg. Named after Haskell Curry. Partial Application. Essentially, pass all arguments and get result or pass subset and get a function awaiting input.

Like passing all the arguments to the function, or pass a subset of args and get a function back that you can finish adding arguments to later.

    const sum = (x,y) => x+y;
    const sumCurry = x => y => x+y;

    console.log (sum (2,1)); // 3
    console.log(sumCurry(2)(1)); // 3

    let partial = sumCurry(2); // this is the subset of args idea

### Recursion

Functional purists don't use loops. EVER. Recursion has action and stop. Tail call optimization in ES6. Graph theory applications.