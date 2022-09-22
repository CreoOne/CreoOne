# Macrostructura 01 - Single unit of work

## Single unit of work

> Small set of atomic operations that help with achieving simply defined goal

Very open and vague definition. When we define goal as _"Place an apple in the basket"_ as our end goal, then whole single unit of work would consist of those atomic operations:

- Move arm close to the apple
- Pick up an apple
- Move arm above the basket
- Place down an apple

When considering that scenario we can see that it consists of some operations that themselves could be defined as single unit of work. Set inside the set, like in mathematics. Let's exercise this thought. _Moving arm above the basket_ as described above seems like very intuitive and straightforward process, but when we inspect how it really happens, then it's true complexity surfaces:

- Identify where an apple is
- Contract specific muscles to move arm in general direction of an apple
- Observe how arm moves in relation to the apple
- Correct muscle contraction
- Predict if arm velocity will make an arm hit an apple
- Contract specific muscles to prevent it
- etc.

As we can see, this is not as easy as it seems. Each of this operation described above can be divided into smaller tasks, then those tasks can be divided too, until we discover the very fabric of the universe, if such a thing even exists. Maybe we can do it infinitely. Anyway, our job, when it comes to software engineering is to identify those small units of work and force them to work in our favor.

## Primitive

Concept of a primitive is not hard to identify in examples described above. Obviously an apple is a primitive. It doesn't matter what color it is or what kind of flavours it contains, but it's position is very important factor in accomplishing our goal. This is exactly how we can define this primitive. 

Currently we can define an apple by this it's size and position, but in the future when new goals become a requirement we can expand this primitive so we can accomplish whatever was expected.

Only appropriate cause that would justify removing any kind of property from primitive would be situation when it is no longer needed for completion any action/operation.

## State

While moving arm in general direction above the basket, arm's muscles contain _contraction amount_ state - meaning that this concrete value will decide how arm moves, with what speed and will this movement cause any collision. It is hard to relate and predict exact amount that needs to be set (amount of muscle contraction) in order to accomplish the task successfully, it is also not clear if just by setting those values once we can achieve the goal. Maybe precise coordination of small changes in muscle contraction is required.

That mechanism suggests that state cannot always be ignored, but it can always be hidden behind single unit of work and inside contain all feedback-loop logic to accomplish the task.

## Complexity

To get rid of arm movement complexity while still being able to do what is required we can replace need for an arm completely by using, lets say, air-pressurized apple canon. That introduces new set of problems for consideration, like: how much air pressure we need in relation to apple mass, where to point the canon, will apple survive this at all?

We removed the need for feedback-loop system, but complexity of relocating an apple stays. No matter how much we try, we will never remove this complexity entirely.

Also creating robotic air canon is an over-engineered solution for our problem. Time spent on developing this out of the box solution would be better spent somewhere else. Only justification for it would be situation when we can accurately predict how this problem will evolve in the future. No-one can do it perfectly, but having some experience in the field can help, especially when it is something that was done before.

## Unit testing

How can one validate this single unit of work? How can one be sure it works as expected?

Simply, by checking if apple is inside the basket. There are problems with this simple approach obviously:

- Was an apple inside the basket before this whole operation?
- Is this the same apple in the basket that was picked from outside it?
- How much time does it take to put it?
- Is it in yet?

All those scenarios can be valid unit tests that test exactly **one unit of work**.

```lua
-- arrange

apple = Apple.create();
basket = Basket.createEmpty();
appleMover = AppleMover.create();

-- act

appleMover.moveInto(apple, basket);

-- assert

Assert.that(apple).is.inside(basket);
```