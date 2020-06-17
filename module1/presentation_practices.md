<!-- .slide: data-background="#111111" -->

# Dobre praktyki

<a href="https://coders.school">
    <img width="500" data-src="../coders_school_logo.png" alt="Coders School" class="plain">
</a>

___

## Inicjalizowanie zmiennych. Praktycznie zawsze.

```cpp
int index = 0;  // ok
bool finished;  // bad
bool finished = false;  // ok

struct Node {
    Node* next = nullptr;   // ok
    int value = 0;
}
```

___

## Przekazywanie przez `const &` w celu unikania zbędnej kopii

___

## Czytanie i stosowanie [CppCoreGuidelines](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md)

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
* F.20: For "out" output values, prefer return values to output parameters
* F.21: To return multiple "out" values, prefer returning a struct or tuple
* F.60: Prefer T* over T& when "no argument" is a valid option
* F.26: Use a unique_ptr<T> to transfer ownership where a pointer is needed
* F.27: Use a shared_ptr<T> to share ownership

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
* Enum.8: Specify enumerator values only when necessary

___

## Q&A

___

## Zadanie domowe

Przejrzyj chociaż nagłówki z [CppCoreGuidelines](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md)
W wolnych chwilach czytaj ile się da :)
