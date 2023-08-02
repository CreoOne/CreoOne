# Macrostructura

&nbsp;

## Introduction

Design patterns are very well known in object oriented world. Over the years in corporate software engineering, i saw them being used sporadically correct or not used at all, but when used correctly they seem to organize themselves into neat and easy to replicate structures, which one could argue, become pattern themselves.

I've never found any resource online which would explain this phenomena, but it surely happens naturally in a lot of places where code quality is a priority.

Motivated by lack of tutorials - decided to describe all parts of this pattern, so they can be reused without thinking too much. Ordering of the parts is dictated by logical order in the hierarchy.

Name "Macrostructura" comes from the idea that small parts build up bigger and bigger structure, which then, at some point, becomes a building block of some larger system.

_All code examples are written in C#, but can easily be moved into any other object oriented language_

&nbsp;

## Interface

Builds application structure. This is what actual abstraction layer architecturally consists of.

> Do not mistake with `abstract` keyword which is used to reduce amount of code duplication by inheritance.

By design describes function it represents in the system as:

- stand-alone (free from external dependencies) - because dependencies are the thing of implementation, not interface
- minimum viable (as small as logically possible) - because complex interfaces are sign on inherent technical debt

### Justification

Use of interfaces [when done right] creates very strong separation between components.

- making code easier (or even possible) to automatically test
- allows for cheap replacement when current implementation does not meet expected requirements anymore
- gives possibility of deciding which implementation will be used when application is running

### Criticism

Defining good interfaces is an art of it's own. Requires domain knowledge and some software design excellence, which makes many engineers abandon the idea.

There exists this misconception in software engineering that small implementation doesn't need interface. Experience showed me that to be completely opposite. Small code snippets should especially be hidden behind interface because **they will** eventually change and they need to be automatically tested too to prevent buildup of technical debt.

Poorly designed interfaces introduce unnecessary complexity and destroy clarity of code.

### Why not `abstract class` instead?

Use of `abstract class` is not wrong, there are situations when it is very healthy, but not as a replacement for interface. Added implementation will sabotage our efforts by *welding* code into the structure of the application, making it a lot harder (sometimes even impossible) to replace and test.

### Example

```csharp
public interface ITea
{
    string Color { get; }
}
```

&nbsp;

## Implementation

_to be written_

### Example

```csharp
public sealed class Rooibos : ITea
{
    public Color => "Amber";
}
```

&nbsp;

## Factory

### Example

```csharp
public interface ITeaFactory
{
    ITea Create();
}

public sealed class RooibosFactory : ITeaFactory
{
    public ITea Create()
    {
        return new Rooibos();
    }
}
```

### Why not static factory?

```csharp
RooibosFactory.Create();
```

... is exactly the same as doing ...

```csharp
new Rooibos();
```

... with the only difference that creation logic is shifted away from constructor. Depending on the scenario that could be desirable, but it still creates hard dependency which we would like to remove.

&nbsp;

## Facade

Now lets also define:

```
ITeaCup
PorcelainTeaCup : ITeaCup

ITeaCupFactory
PorcelainTeaCupFactory : ITeaCupFactory
```

Then we can create `Facade` that will contain all the domain logic.

```csharp
public interface ITeaCeremony
{
    void Prepare();
}

public class AmberTeaCeremony : ITeaCeremony
{
    private ITeaCupFactory TeaCupFactory { get; }
    private ITeaFactory TeaFactory { get; }

    public AmberTeaCeremony(ITeaCupFactory teaCupFactory, ITeaFactory teaFactory)
    {
        TeaCupFactory = teaCupFactory;
        TeaFactory = teaFactory;
    }

    public ITeaCup Prepare()
    {
        var tea = TeaFactory.Create();
        var cup = TeaCupFactory.Create();

        if(tea.Color == "Amber")
            cup.Pour(tea);

        return cup;
    }
}
```

As shown above in preparation to `AmberTeaCeremony` only amber colored tea can be poured into the cup.

&nbsp;

## Builder

In all examples that were presented up to this moment we only have implemented `Rooibos` type of tea. It isn't so hard to imagine other types coming in as the time passes.

In each place where we prepare amber tea ceremony currently all implemented factories are going to be exactly the same, based on that `Builder` can be created which will accept current factories as default, but still allow to customize them when new requirements come.

### Examples

```csharp
public interface ITeaCeremonyBuilder
{
    void SetTeaFactory(ITeaFactory teaFactory);
    void SetTeaCupFactory(ITeaCupFactory teaCupFactory);
    ITeaCeremony Build();
}

public class DefaultAmberTeaCeremonyBuilder : ITeaCeremonyBuilder
{
    private ITeaCupFactory TeaCupFactory { get; } = new PorcelainTeaCupFactory();
    private ITeaFactory TeaFactory { get; } = new RooibosFactory();

    public void SetTeaFactory(ITeaFactory teaFactory);
    public void SetTeaCupFactory(ITeaCupFactory teaCupFactory);
    public ITeaCeremony Build()
    {
        var ceremony = new AmberTeaCeremony();
    }
}
```

... then ...

```csharp
var ceremonyBuilder = new DefaultAmberTeaCeremonyBuilder();
var ceremony = ceremonyBuilder.Build();
```

&nbsp;

## Current state

Those two lines in the last example contain all the business logic without cluttering the readability of the code.
Also any part of it can be replaced and customized during runtime and compile-time without much hassle.
Because we have all classes hidden behind interfaces we can test each class in isolation.

&nbsp;

## Unit Testing

We would of course write unit tests for each method and property in code. Covering all statements with unit tests will not exhaust all possible states that can happen in code, but will define very specific _state_ in which the code will be _frozen_. Having such mechanism prevents from unknowingly introducing breaking changes. As soon as breaking change goes into codebase, execution of tests is going to show it.

### Disadvantages

Unit tests are code too, so they too need the maintenance time. Creating well written test cases and whole scenarios requires some expertise too.

&nbsp;

## Conclusion

_to be written