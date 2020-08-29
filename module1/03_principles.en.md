<!-- .slide: data-background="#111111" -->

# Programming principles

<a href="https://coders.school">
    <img width="500" data-src="../coders_school_logo.png" alt="Coders School" class="plain">
</a>

___

## Known and liked principles

* <!-- .element: class="fragment fade-in" --> Fail-fast
* <!-- .element: class="fragment fade-in" --> Scout rule
* <!-- .element: class="fragment fade-in" --> DRY
* <!-- .element: class="fragment fade-in" --> DRTW
* <!-- .element: class="fragment fade-in" --> KISS
* <!-- .element: class="fragment fade-in" --> YAGNI
* <!-- .element: class="fragment fade-in" --> RTFM
* <!-- .element: class="fragment fade-in" --> No Tests - Don't Touch
* <!-- .element: class="fragment fade-in" --> CQRS
* <!-- .element: class="fragment fade-in" --> 90-90 rule
* <!-- .element: class="fragment fade-in" --> Zen of Python

[More on Wikipedia](https://en.wikipedia.org/wiki/Category:Programming_principles)
<!-- .element: class="fragment fade-in" -->

___

### We will cover this in Best Practice #2

* <!-- .element: class="fragment fade-in" --> SOLID
* <!-- .element: class="fragment fade-in" --> GRASP
* <!-- .element: class="fragment fade-in" --> STUPID

___
<!-- .slide: style="font-size: 0.8em" -->

## Fail-fast

Stop the program as soon as possible in case of problems. It's better than it running and crashing due to Undefined Behavior later. Good luck finding the cause in that case.
<!-- .element: class="fragment fade-in" -->

### Allowed things
<!-- .element: class="fragment fade-in" -->

* <!-- .element: class="fragment fade-in" -->  unhandled exceptions
* <!-- .element: class="fragment fade-in" -->  assertions (<code>assert</code>, <code>static_assert</code>)
* <!-- .element: class="fragment fade-in" -->  in functions, checking necessary conditions at the beginning

```cpp
void process(std::shared_ptr<int> value) {
    if (!value) {
        return;
    }
    // process normally
}
```
<!-- .element: class="fragment fade-in" -->

### Pros
<!-- .element: class="fragment fade-in" -->

* <!-- .element: class="fragment fade-in" --> minimizing UB (Undefined Behavior)
* <!-- .element: class="fragment fade-in" --> easier debugging and finding the causes of problems

___

## Scout rule

> Always leave the campsite in the same state as you found it.
<!-- .element: class="fragment fade-in" -->

Same with the code as with the camping. If you do mess in the code - you have to clean it up. Cleaning up after others is also very welcome.
<!-- .element: class="fragment fade-in" -->

If you touch someone's code, e.g. by just adding one line - try to improve it.
<!-- .element: class="fragment fade-in" -->

Cleaning should be in a separate commit.
<!-- .element: class="fragment fade-in" -->

### Pros
<!-- .element: class="fragment fade-in" -->

* <!-- .element: class="fragment fade-in" --> the code can only get more readable
* <!-- .element: class="fragment fade-in" --> we are not making a technical debt that we will have to pay someday

___

## DRY

### Don't Repeat Yourself
<!-- .element: class="fragment fade-in" -->

Often, duplications are caused by a simple copy-paste operation.
<!-- .element: class="fragment fade-in" -->

Code that is the same or similar in more than 1 place should be extracted into a function and call that function in this place
<!-- .element: class="fragment fade-in" -->

### Pros
<!-- .element: class="fragment fade-in" -->

* <!-- .element: class="fragment fade-in" --> easier refactoring - change only in one place
* <!-- .element: class="fragment fade-in" --> less room for mistakes. There is no risk that we will forget some occurrences once we discover a bug

___

## DRTW

### Don't Reinvent The Wheel
<!-- .element: class="fragment fade-in" -->

Do not reinvent the wheel and use already made libraries that provide given functionality.
<!-- .element: class="fragment fade-in" -->

### Pros
<!-- .element: class="fragment fade-in" -->

* <!-- .element: class="fragment fade-in" --> usually you are using already tested code
* <!-- .element: class="fragment fade-in" --> less room for incorrect implementations - you may not come up with all test cases
* <!-- .element: class="fragment fade-in" --> saving time

___
<!-- .slide: style="font-size: 0.9em" -->

## KISS

### Keep It Simple, Stupid
<!-- .element: class="fragment fade-in" -->

When writing the code, we do not force the tricks and novelties that may make it more universal and easy for future development, but will reduce its readability.
<!-- .element: class="fragment fade-in" -->

Many seniors have a problem with this and complicate the code unnecessarily. They know from experience that this will make the code easier to modify in the future. What if it will never be modified afterwards, but still read many times?
<!-- .element: class="fragment fade-in" -->

We introduce each "improvement" only when there is such a need. We don't write anything "in advance". See - YAGNI.
<!-- .element: class="fragment fade-in" -->

### Pros
<!-- .element: class="fragment fade-in" -->

* <!-- .element: class="fragment fade-in" --> easier to understand code, especially for juniors

___
<!-- .slide: style="font-size: 0.9em" -->
## YAGNI

### You Aren't Gonna Need It
<!-- .element: class="fragment fade-in" -->

You won't need this. We don't write code in advance, thinking it will come in handy soon. In this way, we generate dead code that is never and probably will not be used.
<!-- .element: class="fragment fade-in" -->

If in the future when a given functionality will be needed, another person will probably implement it (even you will forget that you have already written something after a month and will write it again).
<!-- .element: class="fragment fade-in" -->

### Pros
<!-- .element: class="fragment fade-in" -->

The less code the better:
<!-- .element: class="fragment fade-in" -->

* <!-- .element: class="fragment fade-in" --> shorter compilation time
* <!-- .element: class="fragment fade-in" --> less complicated dependencies
* <!-- .element: class="fragment fade-in" --> less to analyze
* <!-- .element: class="fragment fade-in" --> less to remember (that something was made in advance)
* <!-- .element: class="fragment fade-in" --> faster tool use (<code>grep</code> or <code>Ctrl+F</code> have less to scan)

___

## RTFM

### Read The F*cking Manual 😉
<!-- .element: class="fragment fade-in" -->

Before you start spamming people with questions about a given functionality/tool, read the manual.
<!-- .element: class="fragment fade-in" -->

In Linux, for the tool `tool` use `tool --help` and `man tool`.
<!-- .element: class="fragment fade-in" -->

If, after reading the documentation, you still don't know what to do, then ask others (team members, stackoverflow, other forum, Discord Coders School 😉)
<!-- .element: class="fragment fade-in" -->

### Pros
<!-- .element: class="fragment fade-in" -->

* <!-- .element: class="fragment fade-in" --> More experienced people often have a tight calendar, so they will be grateful if you find a solution on your own or briefly explain problem 😉

___

## No Tests - Don't Touch

If you want to fix a piece of code but it's not tested, write some tests first.
<!-- .element: class="fragment fade-in" -->

If you "improve" or "correct" code that has not been tested, how do you prove that its behavior has not changed after your changes?
<!-- .element: class="fragment fade-in" -->

Never change the implementation and tests for it at the same time. If the tests stop passing, you won't know whether it's because of a broken implementation or broken tests. Tests test the implementation, and the implementation tests the tests.
<!-- .element: class="fragment fade-in" -->

### Pros
<!-- .element: class="fragment fade-in" -->

* <!-- .element: class="fragment fade-in" --> saving yourself potential problems and time
* <!-- .element: class="fragment fade-in" --> writing tests and refactoring will take less time than refactoring without tests (seriously)

___

## CQRS

### Command Query Responsibility Segregation
<!-- .element: class="fragment fade-in" -->

Separate writing from reading.
<!-- .element: class="fragment fade-in" -->

* <!-- .element: class="fragment fade-in" --> <strong>Query</strong> - getting (reading) data - getters
* <!-- .element: class="fragment fade-in" --> <strong>Command</strong> - working on data (write)

We should avoid methods that do both because:
<!-- .element: class="fragment fade-in" -->

> Asking a question should not change the answer
>
> -- * Bertrand Meyer *
<!-- .element: class="fragment fade-in" -->

___

## Rule 90-90

You will complete 90% of the tasks within 90% of the time allocated to them.
<!-- .element: class="fragment fade-in" -->

The remaining 10% of the tasks will be completed in the remaining 90% of the time.
<!-- .element: class="fragment fade-in" -->

Useful when assessing the progress of work.
<!-- .element: class="fragment fade-in" -->

At first the work goes quite easy (the general outline of the task), but then edge cases get discovered which were unthought of before, due to which the task will take longer time expected.
<!-- .element: class="fragment fade-in" -->

___
<!-- .slide: style="font-size: 0.9em" -->

## Zen of Python

```python
import this
```
<!-- .element: class="fragment fade-in" -->

```text
The Zen of Python, by Tim Peters

Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!
```
<!-- .element: class="fragment fade-in" -->

___

## Q&A
