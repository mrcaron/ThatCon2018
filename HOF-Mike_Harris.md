# Say Goodbye to For Loops; HOF for the Win

- pop quiz about random loops in C++
- for loops don't reveal intentions well; not telling anything about what it's trying to do
- Covering MAP, FILTER and FOLD ideas

## Problem Statement

How to find the total for MKE zipcode

    Order
     + zip
     + price
     + quanity

Defines question and solution with For loop in C#; find the running total of all orders from MKE.

    var total = 0.0;
    foreach (var order in orders)
    {
        if (orer.Zip = MKE.zip) {
            total += order.Price * order.Quantity;
        }
    }

or more generally,

    var total = Initial;
    foreach (var order in orders)
    {
        if (Predicate)
            Accumulator += Mapping;
    }

## For Loop Grammar

- Predicate (limiting the zips to look at)
- Mapping (function to get the iteration value)
- Accumulator (accumulating running total )
- Initial

## Linq

    var total = orders
        .Where(Predicate)
        .Select(Mapping)
        .Aggregate(Initial, Accumulator);

The linq solution has a bit more words that help us see what's happening. Compare to for loop.

For:

- more classic
- easier to debug step

Linq:

- descriptive
- Monads (big term)
  - composable, you can rearrange it.

- looks like SQL (also declarative), keywords chosen to make it look like SQL, so that it's declarative in nature
- collection of extension methods (fluid)
- it's the reson we have lambdas in C#
- Less complex, cyclomatically; a For loop is twice as hard to understand
- Data flow is clear, linear.

(anything like this for C++?)

## Flow

    ORDERS -> Predicate -> Filter
    ORDERS -> mapping -> Filter

## Higher Order Functions (HOF)

consume or produce a function

### Map

Map is a transform operation.

    [a] -> (a -> b) -> [b]

The idea is to map one thing to another. It takes one thing from the first collection and makes an item in the second one.

Naieve implementation:

    foreach(var item in source)
    {
        result.Add(MyMap(item));
        // refactor to 
        // result.Add(Mapping);
    }

### Filter

Who is and is not allowed into the collection (think grep).

    [a] -> (a -> bool) -> [a]

Naive implementation:

    foreach(var item in source)
    {
        if (predicate(item))
            result.Add(item);
        // if (PREDICATE)
        //    ADD
    }

### Fold

This is the accumulator part. hree pieces... data, seed, accumulator

    [a] -> state -> (state -> a -> state) -> state

    a[1] state[0] -[fold]> a[n] state[n-1] -[fold]>

This is about changing the state of an aggregate based on the chain in the collection.

Naieve Implementation:

    var result = initial;
    foreach( var item in source)
    {
        result = accumulate(result, item);
    }

Note the Initial value and the Accumulation. If you see this, you can refactor it into a fold.

## HOF in C#

Remember GoF Iterator pattern. (pic). The Aggregate knows how to store the accumulated data; its independent. The iterator knows how to traverse through the Aggregate; that's all it does. In C# the iterator pattern is implemented through IEnumerator.

    IEnumerator
    + Current  // GoF: Next
    + MoveNext() // GoF: HasNext()
    + Reset()

We can create an extension method:

    public static void Iterate<T>(
        this IEnumerator<T> source, Action<T> f)
        .... // see slides?
    )
    {
        // see slides
    }

### Implementation of Linq

Explore Map, Filter and Fold in C#. (Explore this further) (where, select and aggregate). Use a spy list to see when and where the Where, Select and Aggregate of Linq are called.

### Fusion Property of Iterator

google. it.

## Conclusions

This is very powerful. Allows us to process massive amounts of data in a declarative way. Can focus on the problem domain rather than the technical domain. Being able to communicate using the same language as your business partners gives huge amounts of help. Learn once, use everywhere. HUGE for cloud computing. It's a very old idea (lisp, scheme, recursion). Once you understand these things, you can bring them to different languages and technologies (list comprehensions, powershell, f#, tSQL, etc).

HOF vs. Imperative. HOF is way easier to grasp.