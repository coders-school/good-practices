<!-- .slide: data-background="#111111" -->

# Praktyki programistyczne

<a href="https://coders.school">
    <img width="500" data-src="../coders_school_logo.png" alt="Coders School" class="plain">
</a>

___

## Znane i lubiane praktyki

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

[Więcej na Wikipedii](https://en.wikipedia.org/wiki/Category:Programming_principles)
<!-- .element: class="fragment fade-in" -->

___

### To omówimy na Dobrych praktykach #2

* <!-- .element: class="fragment fade-in" --> SOLID
* <!-- .element: class="fragment fade-in" --> GRASP
* <!-- .element: class="fragment fade-in" --> STUPID

___
<!-- .slide: style="font-size: 0.8em" -->

## Fail-fast

Jak najszybciej ubijaj program w przypadku problemów. Lepsze to niż działanie i wykrzaczenie się go z powodu Undefined Behavior później. Powodzenia w szukaniu przyczyny w takim przypadku.
<!-- .element: class="fragment fade-in" -->

### Dozwolone rzeczy
<!-- .element: class="fragment fade-in" -->

* <!-- .element: class="fragment fade-in" -->  nieobsłużone wyjątki
* <!-- .element: class="fragment fade-in" -->  asercje (<code>assert</code>, <code>static_assert</code>)
* <!-- .element: class="fragment fade-in" -->  w funkcjach sprawdzanie koniecznych warunków na początku

```cpp
void process(std::shared_ptr<int> value) {
    if (!value) {
        return;
    }
    // process normally
}
```
<!-- .element: class="fragment fade-in" -->

### Plusy
<!-- .element: class="fragment fade-in" -->

* <!-- .element: class="fragment fade-in" --> minimalizowanie UB (Undefined Behavior)
* <!-- .element: class="fragment fade-in" --> łatwiejsze debugowanie i szukanie przyczyn problemów

___

## Scout rule - zasada skauta

> Zawsze zostawiaj obozowisko w co najmniej takim stanie w jakim je zastałeś.
<!-- .element: class="fragment fade-in" -->

Z kodem tak samo jak z biwakiem. Jeśli nabrudzisz w kodzie - musisz to posprzątać. Bardzo mile widziane jest też posprzątanie po innych.
<!-- .element: class="fragment fade-in" -->

Jeśli dotkniesz czyjegoś kodu, np. tylko dodając jedną linijkę - spróbuj go ulepszyć.
<!-- .element: class="fragment fade-in" -->

Sprzątanie ma być w osobnym commicie.
<!-- .element: class="fragment fade-in" -->

### Plusy
<!-- .element: class="fragment fade-in" -->

* <!-- .element: class="fragment fade-in" --> kod może być tylko coraz czytelniejszy
* <!-- .element: class="fragment fade-in" --> nie robimy długu technicznego, który kiedyś trzeba będzie spałcić

___

## DRY

### Don't Repeat Yourself
<!-- .element: class="fragment fade-in" -->

Często powielenia powstają wskutek prostej operacji "kopipasty".
<!-- .element: class="fragment fade-in" -->

Kod, który jest taki sam lub podobny w więcej niż 1 miejscu należy wydzielić do funkcji i wywoływać tę funkcję w tym miejscu
<!-- .element: class="fragment fade-in" -->

### Plusy
<!-- .element: class="fragment fade-in" -->

* <!-- .element: class="fragment fade-in" --> łatwiejszy refaktoring - zmiana tylko w jednym miejscu
* <!-- .element: class="fragment fade-in" --> mniej miejsca na błędy. Nie ma ryzyka, że po odkryciu błędu nie zmienimy wszystkich wystąpień

___

## DRTW

### Don't Reinvent The Wheel
<!-- .element: class="fragment fade-in" -->

Nie wynajduj koła na nowa i używaj gotowych bibliotek dostarczających daną funkcjonalność.
<!-- .element: class="fragment fade-in" -->

### Plusy
<!-- .element: class="fragment fade-in" -->

* <!-- .element: class="fragment fade-in" --> zazwyczaj używasz już przetestowanego kodu
* <!-- .element: class="fragment fade-in" --> mniej miejsca na błędne implementacje - możesz nie wymyślić wszystkich przypadków testowych
* <!-- .element: class="fragment fade-in" --> oszczędność czasu

___
<!-- .slide: style="font-size: 0.9em" -->

## KISS / BUZI

### Keep It Simple, Stupid
<!-- .element: class="fragment fade-in" -->

### Bez Udziwnień Zapisu, Idioto
<!-- .element: class="fragment fade-in" -->

Pisząc kod, nie wciskamy na siłę tricków i nowości, które może i uczynią go bardziej uniwersalnym i łatwym do przyszłego rozwijania, ale zmniejszą jego czytelność.
<!-- .element: class="fragment fade-in" -->

Wielu seniorów ma z tym problem i niepotrzebnie komplikuje kod. Na podstawie doświadczeń wiedzą, że dzięki temu kod będzie łatwiej modyfikować w przyszłości. A co w sytuacji, jeśli nie będzie on później nigdy modyfikowany, a będzie jednak czytany wiele razy?
<!-- .element: class="fragment fade-in" -->

Każde "usprawnienie" wprowadzamy dopiero wtedy, gdy zachodzi taka potrzeba. Nic nie piszemy "na zapas". Patrz - YAGNI.
<!-- .element: class="fragment fade-in" -->

### Plusy
<!-- .element: class="fragment fade-in" -->

* <!-- .element: class="fragment fade-in" --> kod łatwiejszy do zrozumienia, w szczególności dla juniorów

___
<!-- .slide: style="font-size: 0.9em" -->
## YAGNI

### You Aren't Gonna Need It
<!-- .element: class="fragment fade-in" -->

Nie będziesz tego potrzebować. Nie piszemy kod na zapas, myśląc, że to się wkrótce przyda. Generujemy w ten sposób martwy kod, który nigdy nie jest i raczej nie będzie używany.
<!-- .element: class="fragment fade-in" -->

Jeśli w przyszłości dana funkcjonalność będzie potrzebna to pewnie zaimplementuje ją inna osoba (nawet Ty po miesiącu zapomnisz, że coś już zdarzyło Ci się napisać) i napisze(sz) to ponownie.
<!-- .element: class="fragment fade-in" -->

### Plusy
<!-- .element: class="fragment fade-in" -->

Im mniej kodu tym lepiej:
<!-- .element: class="fragment fade-in" -->

* <!-- .element: class="fragment fade-in" --> krótszy czas kompilacji
* <!-- .element: class="fragment fade-in" --> mniej skomplikowane zależności
* <!-- .element: class="fragment fade-in" --> mniej do analizowania
* <!-- .element: class="fragment fade-in" --> mniej do pamiętania (że coś było zrobione na zapas)
* <!-- .element: class="fragment fade-in" --> szybsze użycie narzędzie (<code>grep</code> lub <code>Ctrl+F</code> mają mniej do skanowania)

___

## RTFM

### Read The F*cking Manual ;)
<!-- .element: class="fragment fade-in" -->

Zanim zasypiesz ludzi pytaniami o daną funkcjonalność / narzędzie przeczytaj instrukcję.
<!-- .element: class="fragment fade-in" -->

W Linuxie dla narzędzia `tool` używaj `tool --help` oraz `man tool`.
<!-- .element: class="fragment fade-in" -->

Jeśli po lekturze dokumentacji nadal nie wiesz co robić, wtedy zapytaj innych (osoby z zespołu, stackoverflow, inne forum, Discord Coders School 😉)
<!-- .element: class="fragment fade-in" -->

### Plusy
<!-- .element: class="fragment fade-in" -->

* <!-- .element: class="fragment fade-in" --> Bardziej doświadczone osoby często mają napięty kalendarz, więc będą wdzięczne jeśli znajdziesz rozwiązanie samodzielnie lub bardziej się streścisz ;)

___

## No Tests - Don't Touch

Jeśli chcesz poprawić jakiś kawałek kodu, ale nie jest on przetestowany, to najpierw napisz testy.
<!-- .element: class="fragment fade-in" -->

Jeśli "ulepszysz", czy też "poprawisz" kod, do którego nie było testów, to jak udowodnisz, że po Twoich zmianach jego zachowanie się nie zmieniło?
<!-- .element: class="fragment fade-in" -->

Nigdy nie zmieniaj jednocześnie implementacji oraz testów do niej. Jeśli testy przestaną przechodzić, to nie będziesz wiedzieć, czy to z powodu zepsutej implementacji czy zepsutych testów. Testy testują implementację, a implementacja testuje testy.
<!-- .element: class="fragment fade-in" -->

### Plusy
<!-- .element: class="fragment fade-in" -->

* <!-- .element: class="fragment fade-in" --> oszczędzanie sobie potencjalnych problemów i czasu
* <!-- .element: class="fragment fade-in" --> napisanie testów i refaktoring zajmie mniej czasu niż refaktoring bez testów (serio)

___

## CQRS

### Command Query Responsibility Segregation
<!-- .element: class="fragment fade-in" -->

Oddziel zapis od odczytu.
<!-- .element: class="fragment fade-in" -->

* <!-- .element: class="fragment fade-in" --> <strong>Query</strong> - pobranie (odczyt) danych - gettery
* <!-- .element: class="fragment fade-in" --> <strong>Command</strong> - działanie na danych (zapis)

Powinniśmy unikać metod, które robią jedno i drugie razem, ponieważ:
<!-- .element: class="fragment fade-in" -->

> Asking a question should not change the answer
>
> -- *Bertrand Meyer*
<!-- .element: class="fragment fade-in" -->

___

## Zasada 90-90

90% zadania wykonasz w ciągu 90% czasu na nie przeznaczone.
<!-- .element: class="fragment fade-in" -->

Pozostałe 10% zadania wykonasz przez pozostałe 90% czasu.
<!-- .element: class="fragment fade-in" -->

Przydatna przy ocenie postępów prac.
<!-- .element: class="fragment fade-in" -->

Na początku prace idą całkiem żwawo (ogólny zarys zadania), ale dopiero w trakcie odkrywane są nie przemyślane wcześniej przypadki brzegowe, przez które zadanie zajmie więcej czasu się spodziewano.
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

___

## Zadanie

Popraw kod stosując poznane zasady
