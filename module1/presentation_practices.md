<!-- .slide: data-background="#111111" -->

# Dobre praktyki

<a href="https://coders.school">
    <img width="500" data-src="../coders_school_logo.png" alt="Coders School" class="plain">
</a>

___

## Zagadka

Tomek dostał 3 jabłka, ale 2 zjadł. Ile jabłek ma Tomek?
<!-- .element: class="fragment fade-in" -->

### Odpowiedź
<!-- .element: class="fragment fade-in" -->

Nie wiadomo, bo nie wiemy ile miał wcześniej zanim dostał 3 jabłka.
<!-- .element: class="fragment fade-in" -->

### Morał
<!-- .element: class="fragment fade-in" -->

Zawsze inicjalizuj zmienne.
<!-- .element: class="fragment fade-in" -->

```cpp
int a;
a += 3;
a -= 2;
std::cout << a << '\n';
```
<!-- .element: class="fragment fade-in" -->

___

## Zawsze inicjalizuj zmienne

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

## Definiuj własne typy

Kod pełny nazw domenowych (własnych typów) lepiej się czyta. Także osoby nie zajmujące się programowaniem na co dzień potrafią dużo na jego podstawie wydedukować.
<!-- .element: class="fragment fade-in" -->

Zobacz te 2 funkcje:
<!-- .element: class="fragment fade-in" -->

```cpp
std::vector<std::pair<uint8_t, uint8_t>> compressGrayscale(std::array<std::array<uint8_t, width>, height>&);
std::array<std::array<uint8_t, width>, height> decompressGrayscale(std::vector<std::pair<uint8_t, uint8_t>>&);
```
<!-- .element: class="fragment fade-in" -->

I zobacz je teraz:
<!-- .element: class="fragment fade-in" -->

```cpp
CompressedImage compressGrayscale(const Image& bitmap);
Image decompressGrayscale(const CompressedImage& compression);
```
<!-- .element: class="fragment fade-in" -->

Aby to osiągnąć wystarczy nadać inne nazwy typom w taki sposób:
<!-- .element: class="fragment fade-in" -->

```cpp
using Image = std::array<std::array<uint8_t, width>, height>;
using CompressedImage = std::vector<std::pair<uint8_t, uint8_t>>;
```
<!-- .element: class="fragment fade-in" -->

___

## Forward declarations

Używaj deklaracji zapowiadających tam gdzie to możliwe zamiast `#include`.
<!-- .element: class="fragment fade-in" -->

Kompilator, aby używać jakiegoś obiektu potrzebuje informacji o jego rozmiarze.
<!-- .element: class="fragment fade-in" -->

```cpp
#include "Fruit.hpp"

int main() {
    Fruit apple;
    // ...
}
```
<!-- .element: class="fragment fade-in" -->

Aby można było utworzyć zmienną lokalną potrzebuje więc znać jej rozmiar. Musi więc mieć odpowiedni nagłówek, w którym ta klasa jest zdefiniowana, aby znać rozmiar takiej zmiennej na stosie.
<!-- .element: class="fragment fade-in" -->

___

### Zagadka

* <!-- .element: class="fragment fade-in" --> Jaki rozmiar ma wskaźnik na <code>int</code>?
* <!-- .element: class="fragment fade-in" --> Jaki rozmiar ma wskaźnik na <code>Fruit</code>?

### Odpowiedź
<!-- .element: class="fragment fade-in" -->

Rozmiar wskaźnika nie zależy typu na który wskazuje. Zazwyczaj ma on 4 lub 8 bajtów (odpowiednio dla procesorów 32 i 64 bitowych).
<!-- .element: class="fragment fade-in" -->

___

### Nieznany rozmiar obiektu

Każdy wskaźnik oraz referencja mają ten sam rozmiar. Dopóki się nimi posługujemy i nie odwołujemy się do żadnych metod lub pól klasy, to informacja o jej rozmiarze lub zawartości nie jest nam potrzebna.
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

W takim przypadku wystarczy, że powiemy kompilatorowi, że typ wskaźnika jest naszą klasą za pomocą deklaracji zapowiadającej (forward declaration). Nie trzeba wtedy stosować `#include` i przyspieszamy dzięki temu kompilację.
<!-- .element: class="fragment fade-in" -->

___

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
<!-- .element: class="fragment fade-in" -->

W takim przypadku potrzeba dołączyć właściwy nagłówek.
<!-- .element: class="fragment fade-in" -->

___

## Unikamy niejawnych konwersji

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

### Zapobieganie niejawnym konwersjom

Słowo kluczowe `explicit` zabrania niejawnych konwersji. Stosuje się je przy konstruktorach, które mogą przypadkiem spowodować konwersję z typu argumentu który przyjmują.
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

Słowo kluczowe `explicit` stosujemy przy:

* konstruktorach jednoargumentowych
  * `explicit Apple(int weight);`
* konstruktorach wieloargumentowych, z jednym nie-domyślnym argumentem
  * `explicit Apple(int weight, int size = 1);`
* operatorach konwersji
  * `explicit operator int() const { return weight_; }`

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
