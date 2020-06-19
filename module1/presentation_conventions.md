<!-- .slide: data-background="#111111" -->

# Konwencje nazewnicze

<a href="https://coders.school">
    <img width="500" data-src="../coders_school_logo.png" alt="Coders School" class="plain">
</a>

___

## Długość linii

Max 120 znaków

## Długość funkcji

Do 10 linii (+/- 5).

Jeśli jest więcej to trzeba wydzielić funkcjonalności do mniejszych funkcji.

___

## Każdy blok (scope) = wcięcie

Każdy zakres rozpoczynający się od nawiasu `{` (nawet jeśli go nie ma np. przy jednolinijkowych `if`, `for`) musi mieć dodatkowy poziom wcięcia.

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

### Wyjątki

* Często przy instrukcji `switch/case` spotkacie się z tym, że case jest na tym samym poziomie co switch. Nie uznajemy tego za błąd.
  
```cpp
switch (value) {
case 1: doSth();
        break;
default: doSthElse();
}
```

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

## Typu konwencji nazewniczych

* lowerCamelCase
* UpperCamelCase (PascalCase)
* snake_case (konwencja Pythona)
* kebab-case (rzadko spotykana w C++, często we front-endzie)

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

___

## Nazwy zmiennych z prefixami - raczej zła praktyka

* zmienna lokalna `l_variable`
* parametr funkcji `p_variable`
* pole klasy `m_variable`
* zmienne globalne `g_variable`
* zmienne statyczne `s_variable`

To może wydawać się fajne, ale niepotrzebnie dodaje 2 znaki do nazwy zmiennej. Zamiast tego lepiej stosować to co na kolejnym slajdzie.

___

## Unikanie prefixów

Uwaga, to są moje opinie na podstawie moich doświadczeń.

* zmienna lokalna `variable`
  * Funkcje/bloki kodu mają być małe (do 10 linii). Wtedy bez trudu znajdujemy zmienne lokalne kilka linijek wyżej
* parametr funkcji `variable`
  * Dla małych funkcji parametry również znajdujemy parę linijek wyżej bez scrollowania
* pole klasy `variable_`
  * Zmienne klasy siedzą w pliku nagłówkowym i musielibyśmy się przełączyć na inny plik, aby upewnić się, że to pole klasy. Tutaj konwencją jest `_`
* zmienne globalne `VARIABLE`
  * Zmienne/stałe pisane dużymi literami są globalne. Są argumenty, aby też tego nie robić, ale ich nie pamiętam.
* zmienne statyczne `s_variable`
  * Tutaj prefix `s_` może zostać, bo inne sposoby są już zajęte :)

__

## Co jak nazywać?

Wszystko to kwestia przyjętej konwencji i może różnić się między projektami. Najważniejsze, to aby w całym projekcie było jednolicie.
My przyjmujemy następujące założenia

### Klasy i struktury

* UpperCamelCase
* rzeczownik + przymiotniki (opcjonalnie)

```cpp
class SuperWarrior {};  // ok
class listenMusic {};   // bad, verb instead of noun. Maybe MusicPlayer?
```

### Zmienne

* lowerCamelCase
* rzeczownik + przymiotniki (opcjonalnie)

```cpp
SuperWarrior mightyBarbarian;   // ok
int clickCounter;               // ok
```

### Funkcje

* lowerCamelCase
* czasownik + przysłówki lub rzeczowniki (opcjonalnie)

```cpp
void generateStructure();       // ok
int calculateCommonSum();       // ok
```

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

```cpp
int counter = 0;
bool isValid = false;

bool compare(int lhs, int rhs);
```

### Dozwolone krótkie nazwy

* `i`, `j` - jako indeksy w pętlach
* `it` - jako skrót od `iterator`
* `el`, `elem` - jako skrót od `element` w pętlach po kolekcji
* `lhs`, `rhs` - jako skrót od `leftHandSide` i `rightHandSide` w funkcjach porównujących

___

## Rodzaje nawiasów

### Egipskie (K&R, Stroustrup)

```cpp
while (x == y) {
    // do sth;
}
```

### Allman

```cpp
while (x == y)
{
    // do sth;
}
```

[Zobacz inne na Wiki i nigdy nie stosuj](https://en.wikipedia.org/wiki/Indentation_style)

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

* left
* center
* right

___

## Autoformatowanie

### `clang-format`

___

## Q&A
