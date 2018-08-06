# Unit Testing Things that are difficult

## Testing motivation

Prove it works as it supposed to. Help us think about failure scenarios. Forces you to think about what could go wrong and how your code can break. Automates testing as much as possible.  Devops enablement... but it's about quality. We want to talk about the stuff that's difficult to test, how to isolate, etc. Let's talk about eliminating the manual aspect for the hard scenarios. There's tools out there to help! Tests are an early warning system; avoid turning them off or letting them go stale.

## Things hard to test

- static methods
- legacy code
- file operations
- http calls
- database calls

## Code

- insert : MOQ - mocks interfaces

    var m = new Mock<Interface>;
    m.Setup(...);

- insert: injecting interfaces

## Testing Static Methods

Like `DateTime.Today`

### Partial Mock Solution

- extract the call to the static method into a helper method on the class under test
- make sure the helper method is marked virtual, so you can mock it
- use a partial mock to substitute the value you want at test time
- example-ish:

    var moqDao = new Mock<IAppointmentDao>();
    var moq = new Mock<MyServicePartialMock>(mockDao.Object);
    mock.Setup(m => m.Today).Returns(today);

### Extract interface Solution

Something like `public interface IDateTimeProvider`; Keep the argumentless constructor so that you can use it in prod with default instances. Then use the argument constructure to provide mocks for everything.

## Testing File Operations

- CsvHelper is a great nuget package, CsvReader class
- lots of static calls involved with doing file ops
- System-IO-Abstractions is really a great package for file ops providing interfaces that you can mock. All the System.IO classes are wrapped.
  - create a MockFileSystem!
  - "what directory is it running in!?"; i.e. how to get the test file references!? MockFileSystem can help you create all that for the testing.
  - Virtual filesystem in memory that can do what you want it to

- This is more integration test stuff, but still... automated.

## HTTP Calls

- how do I test that i'm getting what I think I'm getting?
- how do I test timeouts?
- test status codes?

### Content

First thought might be to mock out an IHttpClient... but there's none of those. Understand a little about HttpClient arch. Message handlers are in there, so we can write fake message handlers and short circut the thing that you're trying to test. Generally you're doing this to cache values, but we can use them to send back fake data. Override `SendAync`. You have to do a bunch of stuff normally to do it right, so use a factory class to generate it with the right stuff. Generate HttpClient classes with the handlers in them.

This is money. Really helpful here for content testing.

### Timeouts

No such thing as a Timeout exception in the .NET HTTP client; they are `OperationCanceledException`.

## Pose

Library to replace ANY .NET method with a delegate! Similar to MS Fakes, but it's ENTRELY in managed code. Nuget github.com/tonerdo/pose. 

    Shim configShim = Shim.Replace( () => Configurationmanager.AppSettings)
        .With( () => new NameValueCollection());
    PoseContext.Isolate(() =>
    {
        // Act
        var actual = ConfigUtil.GetAppSettingWithDefault("SomeKey", "DefaultValue");
        //Assert
        ...
    })

- use it with AppSettings...
- You can do ANYTHING with this. Feels revolutionary.

## Data Access Code

I have a data reader and it's returning some sequence of records and I'm creating something from that. `Using (IDataReader...)`. Phil Haack, "Moq Sequences Revisisted". Uses a MOQ extension method that sets up the returns using a reader mock. You can use this same technique for iteratative streams.

(See EF or Dapper).

## Conclusions

Just because they appear hard to test doesn't mean that they can't be tested. Don't turn off tests. Automate as much as you can.