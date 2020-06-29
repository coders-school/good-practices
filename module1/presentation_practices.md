<!-- .slide: data-background="#111111" -->

# Dobre praktyki

<a href="https://coders.school">
    <img width="500" data-src="../coders_school_logo.png" alt="Coders School" class="plain">
</a>

___

## Zagadka

Tomek dostał 3 jabłka, ale 2 zjadł. Ile jabłek ma Tomek?

### Odpowiedź

Nie wiadomo, bo nie wiemy ile miał wcześniej zanim dostał 3 jabłka.

### Morał

Zawsze inicjalizuj zmienne.

___

## Zawsze inicjalizuj zmienne

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

## Definiuj własne typy

Kod pełny nazw domenowych (własnych typów) lepiej się czyta. Także osoby nie zajmujące się programowaniem na co dzień potrafią dużo na jego podstawie wydedukować.

Zobacze te 2 funkcje:

```cpp
std::vector<std::pair<uint8_t, uint8_t>> compressGrayscale(std::array<std::array<uint8_t, width>, height>&);
std::array<std::array<uint8_t, width>, height> decompressGrayscale(std::vector<std::pair<uint8_t, uint8_t>>&);
```

I zobacz je teraz:

```cpp
CompressedImage compressGrayscale(const Image& bitmap);
Image decompressGrayscale(const CompressedImage& compression);
```

Aby to osiągnąć wystarczy nadać inne nazwy typom w taki sposób:

```cpp
using Image =  std::array<std::array<uint8_t, width>, height>;
using CompressedImage =  std::vector<std::pair<uint8_t, uint8_t>>;
```

___

## Używaj deklaracji zapowiadających tam gdzie to możliwe zamiast #include

Kompilator, aby używać jakiegoś obiektu potrzebuje informacji o jego rozmiarze.

```cpp
#include "Fruit.hpp"
Fruit apple;
```

Aby można było utworzyć zmienną lokalną potrzebuje więc znać jej rozmiar, a więc musi być odpowiedni `#include`, w którym ta klasa jest zdefiniowana.

### Zagadka

Jaki rozmiar ma wskaźnik na int?

A jaki rozmiar ma wskaźnik na Fruit?

### Nieznany rozmiar obiektu

Każdy wskaźnik oraz referencja mają ten sam rozmiar. Dopóki się nimi posługujemy i nie odwołujemy się do żadnych metod lub pól klasy, to informacja o jej rozmiarze lub zawartości nie jest nam potrzebne.

```cpp
class Fruit;

void pass(Fruit* fruit) {
    if (!fruit) {
        return;
    }
    // do sth;
}
```

W takim przypadku wystarczy, że powiemy kompilatorowi, że ten typ jest naszą klasą za pomocą deklaracji zapowiadającej (forward declaration). Nie trzeba wtedy stosować `#include` i przyspieszamy dzięki temu kompilację.

Jeśli jednak odwołamy się do jakiegoś pola lub metody tego obiektu to kompilator powie nam, że ma niepełne informacje.

```cpp
class Fruit;

unsigned getFruitPrice(Fruit* fruit) {
    if (!fruit) {
        return 0u;
    }
    return fruit->getPrice();  // compilation error
}
```

___

## Przekazuj przez `const &` w celu unikania zbędnej kopii

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
