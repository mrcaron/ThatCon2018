# Correcting Common Async/Await Mistakes in .NET

Brandon Minnick
@TheCodeTraveler
https://www.codetraveler.io/THAT-2018-AsyncAwait/
This whole thing is recorded.

## Thread overview
... really high level overview

## IL
- .NET intermediate language

- Your async method gets turned into a class that models a state machine
- MoveNext, moves to next state when Await is called
- the whole MoveNext method body gets put into a big Try-Catch block which swallows up any exception that gets thrown from our code.

## Review
- Async keyword adds 100 bytes or so because every async method becomes a class
- Await every async method; non-awaited async methods hide exceptions!! (goes for ANY Task)

## Code Fix Example

- ICommand is for fire and forget methods
- Don't use Async void unless you're on the MAIN thread
  - Main thread can have async void functions because of it's unique exception bubbling
- NEVER NEVER NEVER use `.Wait()`
  - use `GetAwaiter().GetResult()` instead!! This will get the exception
  - `.Wait()` doesn't give you helpful exceptions, but `GetAwaiter().GetResult()` will unwrap inner exceptions
  - `GetAwaiter().GetResult()` does the same thing as `.Wait()` AND the same thing as `.GetResult()`. NEVER NEVER NEVER use `.GetResult()` on it's own, always preceed with `GetAwaiter()`
- `ConfigureAwait(false)`; avoids context switching

    async Task<> GoGetSomething(...)
    var info = await GoGetSomethingElse().ConfigureAwait(false);

  - configureawait is true by default, but it should be reversed. Gotta know when to use true, default to false though. Read up. Best practice.

- Red flag when you see `return await`, rather just return the task

## Best practices

- Never use `.Wait()` or `.Result()`
  - always use `await`
  - if synchronous, use `.GetAwaiter().GetResult()`
- Fire and forget tasks
  - don't do them unless you're using an ICommand
    - use ICommand as a wrapper
  - use `async void` only from the main thread
    - click handlers
    - async constructors
- Avoid `return await`
  - Remove `async` keyword
  - Except: in `try/catch` blocks
  - Except: in `using(...)` blocks because it won't destroy the stuff it needs to

## More

Xamarin University, CSC350: Using Async Await... tons of stuff to learn. This is some really good deep level stuff.

