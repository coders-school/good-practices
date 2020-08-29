<!-- .slide: data-background="#111111" -->

# Good practices

<a href="https://coders.school">
    <img width="500" data-src="../coders_school_logo.png" alt="Coders School" class="plain">
</a>

___

## Mystery

Tomek got 3 apples, but he ate 2. How many apples does Tom have?
<!-- .element: class="fragment fade-in" -->

### Reply
<!-- .element: class="fragment fade-in" -->

We don't know, because we don't know how many he had before he got 3 apples.
<!-- .element: class="fragment fade-in" -->

### Moral
<!-- .element: class="fragment fade-in" -->

Always initialize variables.
<!-- .element: class="fragment fade-in" -->

```cpp
int a;
a += 3;
a -= 2;
std::cout << a << '\n';
```
<!-- .element: class="fragment fade-in" -->

___

## Always initialize variables

```cpp
int index = 0;              // ok
bool completed;             // bad
bool finished = false;      // ok

if (completed) {            // very bad
    // ...
}

struct Node {
    Node* next = nullptr;   // ok
    int value = 0;
}
```

___

## Define your own types

Code full of domain names (own types) is easier to read. Also people who do not deal with programming on a daily basis can deduce a lot from it.
<!-- .element: class="fragment fade-in" -->

Check out these 2 features:
<!-- .element: class="fragment fade-in" -->

```cpp
std::vector<std::pair<uint8_t, uint8_t>> compressGrayscale(std::array<std::array<uint8_t, width>, height>&);
std::array<std::array<uint8_t, width>, height> decompressGrayscale(std::vector<std::pair<uint8_t, uint8_t>>&);
```
<!-- .element: class="fragment fade-in" -->

And see them now:
<!-- .element: class="fragment fade-in" -->

```cpp
CompressedImage compressGrayscale(const Image& bitmap);
Image decompressGrayscale(const CompressedImage& compression);
```
<!-- .element: class="fragment fade-in" -->

To achieve this, it is enough to give different names to the types like this:
<!-- .element: class="fragment fade-in" -->

```cpp
using Image = std::array<std::array<uint8_t, width>, height>;
using CompressedImage = std::vector<std::pair<uint8_t, uint8_t>>;
```
<!-- .element: class="fragment fade-in" -->

___

## Forward declarations

Use forward declarations where possible instead `#include`.
<!-- .element: class="fragment fade-in" -->

In order to use an object, the compiler needs information about its size.
<!-- .element: class="fragment fade-in" -->

```cpp
#include "Fruit.hpp"

int main() {
    Fruit apple;
    // ...
}
```
<!-- .element: class="fragment fade-in" -->

So in order to be able to create a local variable, I need to know its size. So it must have a proper header where this class is defined to know the size of such a variable on the stack.
<!-- .element: class="fragment fade-in" -->

___

### Mystery

* <!-- .element: class="fragment fade-in" --> What size is the pointer on <code>int</code>?
* <!-- .element: class="fragment fade-in" --> What size is the pointer on <code>Fruit</code>?

### Reply
<!-- .element: class="fragment fade-in" -->

The size of the pointer does not depend on the type it points to. Usually it is 4 or 8 bytes long (for 32 and 64 bit processors respectively).
<!-- .element: class="fragment fade-in" -->

___

### Object size unknown

Each indicator and reference are of the same size. As long as we use them and do not refer to any methods or fields of the class, we do not need information about its size or content.
<!-- .element: class="fragment fade-in" -->

```cpp
class Fruit;    // class forward declaration

void pass(Fruit* fruit) {
    if (!fruit) {
        return;
    }
    // do sth;
}
```
<!-- .element: class="fragment fade-in" -->

In that case, we just need to tell the compiler that the pointer type is our class by means of a forward declaration. You do not need to apply then `#include` and we speed up compilation.
<!-- .element: class="fragment fade-in" -->

___

However, if we refer to a field or method of this object, the compiler tells us that it has incomplete information.

```cpp
class Fruit;

unsigned getFruitPrice(Fruit* fruit) {
    if (!fruit) {
        return 0u;
    }
    return fruit->getPrice();  // compilation error
}
```
<!-- .element: class="fragment fade-in" -->

In this case, the correct heading must be attached.
<!-- .element: class="fragment fade-in" -->

___

## We avoid implicit conversions

```cpp
class Apple {
    int weight_;
public:
    Apple(int weight);  // possible conversion from int to Apple
};

void takeApple(Apple a);

int main() {
    takeApple(150);     // int converted implicitly into Apple
}
```
<!-- .element: class="fragment fade-in" -->

___

### Avoiding Implicit Conversions

Key word `explicit` prohibits implicit conversions. They are used with constructors that may accidentally convert from the type of argument they take.
<!-- .element: class="fragment fade-in" -->


```cpp
class Apple {
    int weight_;
public:
    explicit Apple(int weight);
};

void takeApple(Apple a);

int main() {
    takeApple(150);     // compilation error, expected Apple, got int
}
```
<!-- .element: class="fragment fade-in" -->

___

## `explicit`

Key word `explicit` we use for:

* unary constructors
  * `explicit Apple(int weight);`
* multi-argument constructors, with one non-default argument
  * `explicit Apple(int weight, int size = 1);`
* conversion operators
  * `explicit operator int() const { return weight_; }`

___

## Reading and application [CppCoreGuidelines](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md)

___

## F: Functions

* F.1: "Package" meaningful operations as carefully named functions
* F.2: A function should perform a single logical operation
* F.3: Keep functions short and simple
* F.4: If a function may have to be evaluated at compile time, declare it constexpr
* F.5: If a function is very small and time-critical, declare it inline
* F.6: If your function may not throw, declare it noexcept
* F.9: Unused parameters should be unnamed
* F.16: For "in" parameters, pass cheaply-copied types by value and others by reference to const
* F.17: For "in-out" parameters, pass by reference to non-const
* F.20: For "out" output values, prefer return values ​​to output parameters
* F.21: To return multiple "out" values, prefer returning a struct or tuple
* F.60: Prefer T * over T & when "no argument" is a valid option
* F.26: Use a unique_ptr <T> to transfer ownership where a pointer is needed
* F.27: Use a shared_ptr <T> to share ownership

___

## C: Classes and class hierarchies

* C.1: Organize related data into structures (structs or classes)
* C.2: Use class if the class has an invariant; use struct if the data members can vary independently
* C.7: Don't define a class or enum and declare a variable of its type in the same statement
* C.8: Use class rather than struct if any member is non-public
* C.9: Minimize exposure of members

___

## Enum: Enumerations

* Enum.1: Prefer enumerations over macros
* Enum.2: Use enumerations to represent sets of related named constants
* Enum.3: Prefer enum classes over "plain" enums
* Enum.4: Define operations on enumerations for safe and simple use
* Enum.5: Don't use ALL_CAPS for enumerators
* Enum.6: Avoid unnamed enumerations
* Enum.7: Specify the underlying type of an enumeration only when necessary
* Enum.8: Specify enumerator values ​​only when necessary

___

## Q&A
