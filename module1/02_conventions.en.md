<!-- .slide: data-background="#111111" -->

# Conventions

<a href="https://coders.school">
    <img width="500" data-src="../coders_school_logo.png" alt="Coders School" class="plain">
</a>

___

## Line length

Max 120 characters
<!-- .element: class="fragment fade-in" -->

## Length of the function

Up to 10 lines (+/- 5).
<!-- .element: class="fragment fade-in" -->

If there is more then you need to separate the functionalities into smaller functions.
<!-- .element: class="fragment fade-in" -->

___
<!-- .slide: style="font-size: 0.75em" -->

## Each block (scope) = indent

Any range that begins with parentheses `{` - even if it is not present, e.g. for one-line ones `if`, `for` - must have an additional level of indentation.

```cpp
int addEven(const std::vector<int>& numbers)
{
    int sum{};
    for (const auto& el: numbers)
    {
        if(el % 2 == 0)
        sum = sum + el;     // bad, no additional indentation
    }
    return sum;
 }
 ```

 ```cpp
int addEven(const std::vector<int>& numbers)
{
    int sum{};
    for (const auto& el: numbers)
    {
        if(el % 2 == 0)
        {
            sum = sum + el;     // indentation ok, braces added
        }
    }
    return sum;
 }
 ```

___

### Exceptions - `switch/case`

Often with instructions `switch/case` you will meet with that `case` is on the same level as `switch`. We do not consider this a mistake.

```cpp
switch (value) {
case 1: doSth();
        break;
default: doSthElse();
}
```

___

### Exceptions cont.

* `namespace`
* access modifiers `public`, `protected`, `private`

```cpp
namespace shm {

class Ship {
public:
    Ship() = default;
    // ...

private:
    size_t maxCrew;
    // ...
}

} // namespace shm
```

___

## Types of naming conventions

* <!-- .element: class="fragment fade-in" --> lowerCamelCase
* <!-- .element: class="fragment fade-in" --> UpperCamelCase (PascalCase)
* <!-- .element: class="fragment fade-in" --> snake_case (Python convention)
* <!-- .element: class="fragment fade-in" --> kebab-case (rare in C++, often in the front-end)

___

## Hungarian notation - bad practice

In Hungarian notation, type information is contained in the variable name. [Read on the Wiki and never use it](https://pl.wikipedia.org/wiki/Notacja_węgierska)

* ~~`iNumber`~~
* ~~`szName`~~
* ~~`lpcszText`~~

___

## Conventions for class members

* postfix _underscore_ `_` behind the name
* prefix `m_` before the name

Prefixes cannot be used `_`. Any name starting with _underscore_ is reserved for the compiler.

[stackoverflow.com](https://stackoverflow.com/questions/228783/what-are-the-rules-about-using-an-underscore-in-a-c-identifier)

___

## Variable names with prefixes - rather bad practice

* <!-- .element: class="fragment fade-in" --> local variable <code>l_variable</code>
* <!-- .element: class="fragment fade-in" --> function parameter <code>p_variable</code>
* <!-- .element: class="fragment fade-in" --> class field <code>m_variable</code>
* <!-- .element: class="fragment fade-in" --> global variables <code>g_variable</code>
* <!-- .element: class="fragment fade-in" --> static variables <code>s_variable</code>

This may seem cool, but it unnecessarily adds 2 characters to the variable name. Instead, it's better to use what's on the next slide.
<!-- .element: class="fragment fade-in" -->

___

## Avoiding prefixes

Note, these are my opinions based on my experience.

* <!-- .element: class="fragment fade-in" --> local variable: <code>variable</code>
  * Functions/code blocks should be small (up to 10 lines). Then we easily find local variables a few lines higher
* <!-- .element: class="fragment fade-in" --> function parameter: <code>variable</code>
  * For small functions, the parameters are also found a few lines higher without scrolling
* <!-- .element: class="fragment fade-in" --> class member: <code>variable_</code>
  * The class variables sit in the header file and we would have to switch to a different file to make sure it's a class field. The convention here is postfix `_`
* <!-- .element: class="fragment fade-in" --> global variables: <code>VARIABLE</code>
  * Uppercase variables/constants are global. There are arguments for not doing this either, but I don't remember them.
* <!-- .element: class="fragment fade-in" --> static variables: <code>s_variable</code>
  * Prefix here `s_` can stay, because other ways are already taken :)

___

## How to name what?

All this is a matter of convention and may differ from project to project. The most important thing is that it is uniform throughout the project.
We make the following assumptions.

___

### Classes and structures

* UpperCamelCase
* noun + adjectives (optional)

```cpp
class SuperWarrior {};  // ok
class listenMusic {};   // bad, verb instead of noun. Maybe MusicPlayer?
```

___

### Variables

* lowerCamelCase
* noun(s) + adjectives (optional)

```cpp
SuperWarrior mightyBarbarian;   // ok
int clickCounter;               // ok
```

___

### Functions

* lowerCamelCase
* verb + adverbs or nouns (optional)

```cpp
void generateStructure();       // ok
int calculateCommonSum();       // ok
```

___

### Class members

* as normal variables
* additionally _underscore_ `_` after the name

```cpp
class SuperWarrior
{
    int level_ = 1;
    int strength_ = 50;
    int dexterity_ = 10;
    int mana_ = 0;
};
```

___

### Filenames

* file name = class name
* UpperCamelCase / lowerCamelCase / snake_case / kebab-case

`class SuperWarrior` -> SuperWarrior.hpp / SuperWarrior.cpp

___

## Descriptive variable names

Don't name variables like this:

```cpp
int a = 0;          // what is a?
bool b = false;     // what is b?

bool compare(int a, int b);   // what does a and b represent?
```

If you look at this code after a month, you won't know what it does either. This is much better:
<!-- .element: class="fragment fade-in" -->

```cpp
int counter = 0;
bool isValid = false;

bool compare(int lhs, int rhs);
```
<!-- .element: class="fragment fade-in" -->
___

### Allowed short names

* `i`, `j` - as indexes in loops
* `it` - as an abbreviation of `iterator`
* `el`, `elem` - as an abbreviation of `element` in loops over collection
* `lhs`, `rhs` - as an abbreviation of `leftHandSide` and `rightHandSide` in comparing functions

___

## Types of parentheses

### Egyptian (K&R, Stroustrup)
<!-- .element: class="fragment fade-in" -->

```cpp
while (x == y) {
    // do sth;
}
```
<!-- .element: class="fragment fade-in" -->

### Allman
<!-- .element: class="fragment fade-in" -->

```cpp
while (x == y)
{
    // do sth;
}
```
<!-- .element: class="fragment fade-in" -->

[See others on the wiki and never apply](https://en.wikipedia.org/wiki/Indentation_style)
<!-- .element: class="fragment fade-in" -->

___

### My favorite formatting

Note that this is an opinion! For functions - Allman. For loops and ifs - Egyptian. For classes - whatever. Reason:

```cpp
class SuperWarrior
{
public:
    SuperWarrior(int level, int strength, int dexterity)
        : level_(level)
        , strength_(strength)
        , dexterity(dexterity)
    {
        if (level_ >= 10) {
            mana_ = 50;
        }
    }

private:
    int level_ = 1;
    int strength_ = 50;
    int dexterity_ = 10;
    int mana_ = 0;
};
```

___

Constructor initialization lists or too long names and types of function parameters spoil the readability of the code blocks a little.

For contrast:

```cpp
class SuperWarrior {
public:
    SuperWarrior(int level, int strength, int dexterity)
            : level_(level)
            , strength_(strength)
            , dexterity(dexterity) {
        if (level_ >= 10) {
            mana_ = 50;
        }
    }

private:
    int level_ = 1;
    int strength_ = 50;
    int dexterity_ = 10;
    int mana_ = 0;
};
```

___

## Sticking `&` and `*`

* <!-- .element: class="fragment fade-in" --> left <code>int& ref</code>
  * okay :)
* <!-- .element: class="fragment fade-in" --> center <code>int & ref</code>
  * I personally like it
* <!-- .element: class="fragment fade-in" --> right <code>int &ref</code>
  * avoid

___

## The ternary operator `?:`

One line notation is usually unreadable
<!-- .element: class="fragment fade-in" -->

```cpp
lhs.size() == rhs.size() ? lhs < rhs : lhs.size() < rhs.size()
```
<!-- .element: class="fragment fade-in" -->

It is better to write it in two lines.
<!-- .element: class="fragment fade-in" -->

```cpp
lhs.size() == rhs.size() ? lhs < rhs
                         : lhs.size() < rhs.size()
```
<!-- .element: class="fragment fade-in" -->

And sometimes even 3 if the condition is long.
<!-- .element: class="fragment fade-in" -->

```cpp
lhs.name == rhs.name && lhs.amount == rhs.amount && lhs.price == rhs.price
    ? lhs.value < rhs.value
    : lhs.price < rhs.price
```
<!-- .element: class="fragment fade-in" -->

Although IMO its better to use the usual one in the last `if` case.
<!-- .element: class="fragment fade-in" -->

___

## AutoFormat

### `clang-format`

The project should include a file `.clang-format` which will ensure that anyone can apply the formatting it describes automatically

```bash
clang-format -style=.clang-format -i *.cpp *.hpp
```

___

## Q&A
