<!-- .slide: data-background="#111111" -->

# Konwencje

<a href="https://coders.school">
    <img width="500" data-src="../coders_school_logo.png" alt="Coders School" class="plain">
</a>

___

## Długość linii

Max 120 znaków
<!-- .element: class="fragment fade-in" -->

## Długość funkcji

Do 10 linii (+/- 5).
<!-- .element: class="fragment fade-in" -->

Jeśli jest więcej to trzeba wydzielić funkcjonalności do mniejszych funkcji.
<!-- .element: class="fragment fade-in" -->

___
<!-- .slide: style="font-size: 0.75em" -->

## Każdy blok (scope) = wcięcie

Każdy zakres rozpoczynający się od nawiasu `{` - nawet jeśli go nie ma np. przy jednolinijkowych `if`, `for` - musi mieć dodatkowy poziom wcięcia.

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

### Wyjątki - `switch/case`

Często przy instrukcji `switch/case` spotkacie się z tym, że `case` jest na tym samym poziomie co `switch`. Nie uznajemy tego za błąd.

```cpp
switch (value) {
case 1: doSth();
        break;
default: doSthElse();
}
```

___

### Wyjątki cd.

* `namespace`
* modyfikatory dostępu `public`, `protected`, `private`

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

## Typy konwencji nazewniczych

* <!-- .element: class="fragment fade-in" --> lowerCamelCase
* <!-- .element: class="fragment fade-in" --> UpperCamelCase (PascalCase)
* <!-- .element: class="fragment fade-in" --> snake_case (konwencja Pythona)
* <!-- .element: class="fragment fade-in" --> kebab-case (rzadko spotykana w C++, często we front-endzie)

___

## Notacja węgierska - zła praktyka

W notacji węgierskiej informacja o typie zawiera się w nazwie zmiennej. [Poczytaj na Wiki i nigdy nie stosuj](https://pl.wikipedia.org/wiki/Notacja_węgierska)

* ~~`iNumber`~~
* ~~`szName`~~
* ~~`lpcszText`~~

___

## Konwencje dla pól klasy

* postfix _underscore_ `_` za nazwą
* prefix `m_` przed nazwą

Nie wolno stosować prefixów `_`. Każda nazwa zaczynająca się od _underscore_ jest zarezerwowana dla kompilatora.

[stackoverflow.com](https://stackoverflow.com/questions/228783/what-are-the-rules-about-using-an-underscore-in-a-c-identifier)

___

## Nazwy zmiennych z prefixami - raczej zła praktyka

* <!-- .element: class="fragment fade-in" --> zmienna lokalna `l_variable`
* <!-- .element: class="fragment fade-in" --> parametr funkcji `p_variable`
* <!-- .element: class="fragment fade-in" --> pole klasy `m_variable`
* <!-- .element: class="fragment fade-in" --> zmienne globalne `g_variable`
* <!-- .element: class="fragment fade-in" --> zmienne statyczne `s_variable`

To może wydawać się fajne, ale niepotrzebnie dodaje 2 znaki do nazwy zmiennej. Zamiast tego lepiej stosować to co na kolejnym slajdzie.
<!-- .element: class="fragment fade-in" -->

___

## Unikanie prefixów

Uwaga, to są moje opinie na podstawie moich doświadczeń.

* <!-- .element: class="fragment fade-in" --> zmienna lokalna: <code>variable</code>
  * Funkcje/bloki kodu mają być małe (do 10 linii). Wtedy bez trudu znajdujemy zmienne lokalne kilka linijek wyżej
* <!-- .element: class="fragment fade-in" --> parametr funkcji: <code>variable</code>
  * Dla małych funkcji parametry również znajdujemy parę linijek wyżej bez scrollowania
* <!-- .element: class="fragment fade-in" --> pole klasy: <code>variable_</code>
  * Zmienne klasy siedzą w pliku nagłówkowym i musielibyśmy się przełączyć na inny plik, aby upewnić się, że to pole klasy. Tutaj konwencją jest postfix `_`
* <!-- .element: class="fragment fade-in" --> zmienne globalne: <code>VARIABLE</code>
  * Zmienne/stałe pisane dużymi literami są globalne. Są argumenty, aby też tego nie robić, ale ich nie pamiętam.
* <!-- .element: class="fragment fade-in" --> zmienne statyczne: <code>s_variable</code>
  * Tutaj prefix `s_` może zostać, bo inne sposoby są już zajęte :)

___

## Co jak nazywać?

Wszystko to kwestia przyjętej konwencji i może różnić się między projektami. Najważniejsze, to aby w całym projekcie było jednolicie.
My przyjmujemy następujące założenia.

___

### Klasy i struktury

* UpperCamelCase
* rzeczownik + przymiotniki (opcjonalnie)

```cpp
class SuperWarrior {};  // ok
class listenMusic {};   // bad, verb instead of noun. Maybe MusicPlayer?
```

___

### Zmienne

* lowerCamelCase
* rzeczownik(i) + przymiotniki (opcjonalnie)

```cpp
SuperWarrior mightyBarbarian;   // ok
int clickCounter;               // ok
```

___

### Funkcje

* lowerCamelCase
* czasownik + przysłówki lub rzeczowniki (opcjonalnie)

```cpp
void generateStructure();       // ok
int calculateCommonSum();       // ok
```

___

### Pola klasy

* jak zwykłe zmienne
* dodatkowo za nazwą _underscore_ `_`

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

### Nazwy plików

* lowerCamelCase
* nazwa pliku = nazwa klasy

`class SuperWarrior` -> superWarrior.hpp / superWarrior.cpp

___

## Opisowe nazwy zmiennych

Nie nazywajmy zmiennych tak:

```cpp
int a = 0;          // what is a?
bool b = false;     // what is b?

bool compare(int a, int b);   // what does a and b represent?
```

Gdy po miesiącu spojrzysz na ten kod też nie będziesz wiedzieć co on robi. Tak jest znacznie lepiej:
<!-- .element: class="fragment fade-in" -->

```cpp
int counter = 0;
bool isValid = false;

bool compare(int lhs, int rhs);
```
<!-- .element: class="fragment fade-in" -->
___

### Dozwolone krótkie nazwy

* `i`, `j` - jako indeksy w pętlach
* `it` - jako skrót od `iterator`
* `el`, `elem` - jako skrót od `element` w pętlach po kolekcji
* `lhs`, `rhs` - jako skrót od `leftHandSide` i `rightHandSide` w funkcjach porównujących

___

## Rodzaje nawiasów

### Egipskie (K&R, Stroustrup)
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

[Zobacz inne na Wiki i nigdy nie stosuj](https://en.wikipedia.org/wiki/Indentation_style)
<!-- .element: class="fragment fade-in" -->

___

### Moje ulubione formatowanie

Uwaga, to jest opinia! Dla funkcji - Allman. Dla pętli, if - egipskie. Dla klas - whatever. Powód:

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

Listy inicjalizacyjne konstruktorów lub zbyt długie nazwy i typy parametrów funkcji trochę psują czytelność bloków kodu.

Dla kontrastu:

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

## Doklejanie `&` i `*`

* <!-- .element: class="fragment fade-in" --> left <code>int& ref</code>
  * ok :)
* <!-- .element: class="fragment fade-in" --> center <code>int & ref</code>
  * osobiście to lubię
* <!-- .element: class="fragment fade-in" --> right <code>int &ref</code>
  * unikać

___

## Operator trójargumentowy `?:`

Zapis całości w jednej linii zazwyczaj jest nieczytelny
<!-- .element: class="fragment fade-in" -->

```cpp
lhs.size() == rhs.size() ? lhs < rhs : lhs.size() < rhs.size()
```
<!-- .element: class="fragment fade-in" -->

Lepiej zapisać go w dwóch liniach.
<!-- .element: class="fragment fade-in" -->

```cpp
lhs.size() == rhs.size() ? lhs < rhs
                         : lhs.size() < rhs.size()
```
<!-- .element: class="fragment fade-in" -->

A czasami nawet 3, jeśli warunek jest długi.
<!-- .element: class="fragment fade-in" -->

```cpp
lhs.name == rhs.name && lhs.amount == rhs.amount && lhs.price == rhs.price
    ? lhs.value < rhs.value
    : lhs.price < rhs.price
```
<!-- .element: class="fragment fade-in" -->

Chociaż IMO lepiej już w ostatnim przypadku używać zwykłego `if`.
<!-- .element: class="fragment fade-in" -->

___

## Autoformatowanie

### `clang-format`

W projekcie powinien być wkomitowany plik `.clang-format`, który zapewni, że każdy może zastosować opisane w nim formatowanie automatycznie

```bash
clang-format -style=.clang-format -i *.cpp *.hpp
```

___

## Q&A
