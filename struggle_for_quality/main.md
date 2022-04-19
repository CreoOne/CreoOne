# Struggle for quality

## Stuck with bad software

After seeing uncountable LOC and using hundreds or maybe thousands different apps daily, i came to not surprising realization that:

> All code is bad

and unfortunately it's not going to change soon. It's not like i do better myself. No, i look at my code minutes or even seconds after writing it and immediately comes the feeling of overwhelming disappointment. Always can do better and always try, but wanting doesn't even points towards the goal, quite the opposite, either:

- fail to produce anything because it's impossible to deliver perfect code  
- get stuck in a loop of infinite refactoring
- give up and say to myself "good enough for now, will improve later" (which of course said improvement rarely happens)

While last option is something that actually gets you closer into accomplishing anything, result is miles away from satisfactory. It's fine when prototyping, but how are you supposed to make quality production software like this?

Taught by experience (as probably many of you) i start with solution that is **good enough** and iteratively try to make it closer into **high performance**, **easily scalable**, **readable**, **understandable**, **testable**, **elastic**, **frictionless** (that one surely is funny word we have in business), **bullet proof** masterpiece, but as i said before, this actually occurring is legendary level rare. You end up with code that does the job and move on. This is how money is made today and this is reality for decades now.

## Tools that change fate

So now, how do we flip tables around? Trough experience, negligibly mine and mostly many intelligent people in the field, came up tools that manage to move us closer to perfection, one LOC at the time. Unsurprisingly it's not easy to use them, it's not easy to integrate them, they do not make us richer in any way besides knowledge, they seem to sometimes make more mess than expected. What am i talking about? Of course im talking about:

- multiple levels/layers of testing and coverage (at least octuple)
- self-documenting code
- benchmarking, loading, spiking
- diagnostics (memory, cpu, trace)
- static analysis
- telemetry
- clearly defined patterns in code
- words passed down from generation to generation
- getting yelled at by the client(s) (as absolute form of enlightenment)

All those things get us closer to perfection, mostly trough struggle. If you don't do any of this you are objectively speaking going the wrong path. Your creation may potentially work, like 90% of 20% of the time. Will perform - spectacular production incidents and respond within 30 seconds timeout window when on the happy path. Trust me, you need those more than you think, i'm not overdramatizing, you can thank me later.

Now that we established what is needed, we can talk about what we will get:

- testable, understandable and high performing code
- clearly stated data inputs and outputs (very important)
- always missing deadline
- getting burned out

## Getting things done

Why is it so hard to apply all those great tools in practice? From what i gathered it does not only require military grade self-discipline and academic level competencies, but it's also catastrophically boring for most engineers when performing it on all sources that are produced. You may be passionate about load testing for few months (at best), but you will not be passionate about everything all the time.

Funny thing that happened while learning design patterns is realization that i am no longer able to write another builder or factory. Enough is enough. Then again another time, i already did a very good job applying SOLID and KISS, why do i need to torture myself trough another million keystrokes writing obvious test cases for it? I couldn't force myself to write another boring, plain simple, naively looking piece of code. Years after that experiences, it came to me like lightening from the clear sky.

> That absolutely boring software is exactly what im striving to accomplish

Which neatly blasts the ground for the next section.

## Technical debt

Term technical debt is well known and well explained. You can read multiple good pieces about it online. Basically execute gymnastic dodge on integration tests or performance tests to save time hoping that everything will be fine. No failed tests equals no issues in the code right? Wrong! You are now in dept, deep in it. How deep? Ask yourself after few years when fixing it on production having completely no idea what this piece of complete software poem does. You borrowed not only time, but also a lot of sanity from yourself or whoever comes after you to clean up the mess. At worst you just got there unknowingly and this falling construct is coming down on your unsuspecting self leaving you with feeling of not wanting to write anything anymore ... "maybe i should have become beekeeper instead".

Sources of technical debt:
1. internally - by either distractions, laziness, being burned out or sloppiness, ignorance, incompetence and so on.
2. externally - by incompetent management, bad capacity organization, distractions and surprisingly by fellow software engineers not recognizing need for it (yes, believe me)

It is very important to recognize technical debt early on, even in the planning stage. You can find it hidden under "it should work" or "good enough for now" wording. At this stage it's not actually bad, now it's like business plan, you know that debt is required, to not make it into real problem there needs to be will and ability to pay borrowed price. Otherwise you're truly screwed and bankrupt. Fixing it on production will look like bucketing out water from burning and sinking oil rig - not so professional.

Your colleges and superiors will sometimes think that you are fixing the problem before it occurs opposing your worries. They are semi-right, other part is that they do not trust your instinct and competencies. Writing about it somewhere early, will eventually protect you from blame shift while you are all sinking and burning.

By self-inflicting technical debt and then **learning from it** (which is also necessary) one can be truly motivated to invest in those miraculous tools of trade described earlier.

> Repetitiveness boredom can no longer cause psychical pain if you know what kind of soul crushing problems it will shield from.

This applies equally to all the offline things in life like chores, physical activity, etc. It actually forms good habits! Yes, you will no longer think about how much philosophical suffering it inflicts upon your being! Very important caveat here is that you need to keep doing it, like a metric fabulous ton of it to achieve such proficiency.

Eventually it becomes like breathing, but then produced code still sucks anyway.