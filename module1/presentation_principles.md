<!-- .slide: data-background="#111111" -->

# Praktyki programistyczne

<a href="https://coders.school">
    <img width="500" data-src="../coders_school_logo.png" alt="Coders School" class="plain">
</a>

___

## Znane i lubiane praktyki

* Fail-fast
* Scout rule
* DRY
* DRTW
* KISS
* YAGNI
* RTFM
* No Tests - Don't Touch
* Law of Demeter
* CQRS
* 90-90 rule
* Zen of Python

[Więcej na Wikipedii](https://en.wikipedia.org/wiki/Category:Programming_principles)

* SOLID - omówimy na dobrych praktykach #2
* GRASP - omówimy na dobrych praktykach #2
* STUPID - omówimy na dobrych praktykach #2

___

## Fail-fast

Jak najszybciej ubijaj program w przypadku problemów. Lepsze to niż działanie i wykrzaczenie się go z powodu Undefined Behavior później. Powodzenia w szukaniu przyczyny w takim przypadku.

### Dozwolone rzeczy

* nieobsłużone wyjątki
* asercje (`assert`, `static_assert`)
* w funkcjach sprawdzanie koniecznych warunków na początku

```cpp
void process(std::shared_ptr<int> value) {
    if (!value) {
        return;
    }
    // process normally
}
```

#### Plusy

* minimalizowanie UB (Undefined Behavior)
* łatwiejsze debugowanie i szukanie przyczyn problemów

___

## Scout rule - zasada skauta

Z kodem tak samo jak z biwakiem. Zawsze zostawiaj obozowisko w co najmniej takim stanie jak je zastałeś.

Jeśli nabrudzisz w kodzie - musisz to posprzątać. Bardzo mile widziane jest też posprzątanie po innych.

Jeśli dotkniesz czyjegoś kodu, np tylko dodając jedną linijkę - zobacz czy nie można do ulepszyć.

Sprzątanie ma być w osobnym commicie.

#### Plusy

* kod może być tylko coraz czytelniejszy
* nie robimy długu technicznego, który kiedyś trzeba będzie spałcić

___

## DRY

### Don't Repeat Yourself

Często powielenia powstają wskutek prostej operacji kopipasty.

Kod, który jest taki sam lub podobny w więcej niż 1 miejscu należy wydzielić do funkcji i wywoływać tę funkcję w tym miejscu

#### Plusy

* łatwiejszy refaktoring - zmiana tylko w jednym miejscu
* mniej miejsca na błędy. Nie ma ryzyka, że po odkryciu błędu nie zmienimy wszystkich wystąpień

___

## DRTW

### Don't Reinvent The Wheel

Nie wynajduj koła na nowa i używaj gotowych bibliotek dostarczających daną funkcjonalność. 

Plusy:

* zazwyczaj używasz już przetestowanego kodu
* mniej miejsca na błędne implementacje - możesz nie wymyślić wszystkich przypadków testowych
* oszczędność czasu

___

## KISS

### Keep It Simple, Stupid

___

### Tautologie

___

## YAGNI

### You Aren't Gonna Need It

___

## RTFM

### Read The F*cking Manual ;)

___

## No Tests - Don't Touch

Jeśli chcesz poprawić jakiś kawałek kodu, ale nie jest on przetestowany, to najpierw napisz testy.

Jeśli "ulepszysz", czy też "poprawisz" kod, do którego nie było testów, to jak udowodnisz, ze po Twoich zmianach jego zachowanie się nie zmieniło?

Nigdy nie zmieniaj na raz implementacji oraz testów do niej. Jeśli testy przestaną przechodzić, to nie będziesz wiedzieć, czy to z powodu zepsutej implementacji czy zepsutych testów. Testy testują implementację, a implementacja testuje testy.

___

## Prawo Demeter

___

## CQRS

### Command Query Responsibility Segregation

___

## Zasada 90-90

Przydatna przy ocenie postępów prac.

___

## Zen of Python

> Beautiful is better than ugly.
> Explicit is better than implicit.
> Simple is better than complex.
> Complex is better than complicated.
> Flat is better than nested.
> Sparse is better than dense.
> Readability counts.
> Special cases aren't special enough to break the rules.
> Although practicality beats purity.
> Errors should never pass silently.
> Unless explicitly silenced.
> In the face of ambiguity, refuse the temptation to guess.
> There should be one—and preferably only one—obvious way to do it.
> Although that way may not be obvious at first unless you're Dutch.
> Now is better than never.
> Although never is often better than right now.
> If the implementation is hard to explain, it's a bad idea.
> If the implementation is easy to explain, it may be a good idea.
> Namespaces are one honking great idea—let's do more of those!

___

## Q&A

___

## Zadanie

Popraw kod stosując poznane zasady
