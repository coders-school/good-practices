<!-- .slide: data-background="#111111" -->

# Współpraca grupowa

<a href="https://coders.school">
    <img width="500" data-src="../coders_school_logo.png" alt="Coders School" class="plain">
</a>

___

## Filozoficzne pytania

### a.k.a. wspólne retro

* <!-- .element: class="fragment fade-in" --> Jak się czuliście podczas współpracy?
* <!-- .element: class="fragment fade-in" --> Czy były problemy, których nie przewidzieliście na początku?
* <!-- .element: class="fragment fade-in" --> Czy oszacowany czas zadań był zgodny z rzeczywistością?
* <!-- .element: class="fragment fade-in" --> Co poszło nie tak?
* <!-- .element: class="fragment fade-in" --> A co fajnie zadziałało i moglibyście zasugerować wdrożenie tego innym grupom?

___

## Niespodziewane problemy

To, że tak trochę rzuciliśmy was w ten projekt i zmusiliśmy do samoorganizacji było zabiegiem celowym.
<!-- .element: class="fragment fade-in" -->

Chcieliśmy wam pokazać, ilu rzeczy na początku w ogóle się nie uwzględnia przed rozpoczęciem prac nad projektem.
<!-- .element: class="fragment fade-in" -->

I nawet mając kilkuletnie doświadczenie w zarządzaniu projektami, pewnych rzeczy nie da się uniknąć.
<!-- .element: class="fragment fade-in" -->

* <!-- .element: class="fragment fade-in" --> choroby członków zespołu
* <!-- .element: class="fragment fade-in" --> niespodziewane wyjazdy
* <!-- .element: class="fragment fade-in" --> dodatkowe, niezaplanowane zadania
* <!-- .element: class="fragment fade-in" --> źle oszacowany czas zadań
* <!-- .element: class="fragment fade-in" --> problemy techniczne (restartujący się komputer, git - konflikty, przerywający internet)
* <!-- .element: class="fragment fade-in" --> zmieniające się wymagania lub ich interpretacje

___

## Estymowanie zadań

Teoria wskazuje, że dość fajnym sposobem na lepsze szacowanie zadań jest pomnożenie początkowej estymaty przez PI 😄
<!-- .element: class="fragment fade-in" -->

Inne źródła wskazują, że należy zwiększyć rząd wielkości (np. z 5 godzin na 5 dni, z 3 dni na 3 tygodnie, itp.) 😄
<!-- .element: class="fragment fade-in" -->

W praktyce do estymacji wykorzystuje się pokera
<!-- .element: class="fragment fade-in" -->

## 🃏
<!-- .element: class="fragment fade-in" -->
___

## Scrum poker

### Zasady

* <!-- .element: class="fragment fade-in" --> Zadań nie estymujemy w jednostkach czasu.
* <!-- .element: class="fragment fade-in" --> Całym zespołem wybieramy jedno zadanie, które jest najłatwiejsze ze wszystkich innych. Dajemy mu wartość 1.
* <!-- .element: class="fragment fade-in" --> Używamy tylko wartości z ciągu Fibonacciego (1, 2, 3, 5, 8, 13, 21, ♾, ? - nie mam pojęcia, ☕️). Dzięki temu bardziej skupiamy się na rzędach wielkości niż samych jednostkach, bo pomiędzy 9 a 10 dużej różnicy nie ma.
* <!-- .element: class="fragment fade-in" --> Jednostką są Story Points (SP). Jest to zupełnie abstrakcyjna miara. Możecie o niej myśleć jak o dowolnej innej abstrakcyjnej. Np. to zadanie wyceniam na 5 kasztanów. Informacja zupełnie nieprzydatna, ale pozwala porównywać zadania. Skoro tamto jest warte 8 to jest bardziej wartościowe (trudniejsze).
* <!-- .element: class="fragment fade-in" --> Dla jednej osoby 1 SP może oznaczać 1 godzinę pracy a dla innej 1 dzień.

___

### Przebieg estymacji

* <!-- .element: class="fragment fade-in" --> Całym zespołem omawiamy sobie jedno wybrane zadanie, aby mieć pewność, że wszyscy rozumieją je tak samo.
* <!-- .element: class="fragment fade-in" --> Gdy wszyscy są gotowi jednocześnie wyciągają kartę ze swoją estymatą, aby nie sugerować się innymi
* <!-- .element: class="fragment fade-in" --> Jeśli rozbieżności są duże, to znaczy, że członkowie zespołu mają różne zrozumienie zadania i trzeba jeszcze o nim podyskutować. Warto zapytać osoby z najmniejszą i największą estymatą dlaczego tyle dają.
* <!-- .element: class="fragment fade-in" --> Jeśli rozbieżności są małe to można je uśrednić lub wspólnie zgodzić się na którąś wartość (zazwyczaj wyższą)

Poszukajcie narzędzi typu Scrum Poker online i użyjcie do estymowania zadań na Planningu.
<!-- .element: class="fragment fade-in" -->

___

## Odpowiedzialność zbiorowa

Ciężko winić kogoś, za to, że zachoruje. Ale można winić za to, że się do czegoś zobowiązał, a nie dał znać że to się nie uda. Dlatego ważne jest daily, aby mieć nawyk aktualizowania statusu co najmniej raz dziennie. Oczywiście można częściej.
<!-- .element: class="fragment fade-in" -->

Gdy tylko dowiecie się, że ktoś z załogi wam niedomaga, to powinniście od razu pomyśleć co z tym można zrobić. Jeśli były rozpoczęte prace to należy wkomitować / przekazać to co się do tej pory udało zrobić. To kolejny powód dla którego małe, a częste commity są dobrą praktyką. Każdy ma dostęp do bieżącej wersji kodu i łatwo wtedy przekazać pracę.
<!-- .element: class="fragment fade-in" -->

Dla nas, obserwatorów z zewnątrz nigdy nie możemy ocenić ile kto z zespołu zrobił. Dla nas po prostu zrobił to zespół. Jeżeli czujecie, że robicie za dużo / za mało i coś jest niesprawiedliwe, to możecie napisać nam o waszych problemach i w razie czego zmienić zespół.
<!-- .element: class="fragment fade-in" -->

___

## Dobre praktyki współpracy zespołowej

* <!-- .element: class="fragment fade-in" --> Pair programming
* <!-- .element: class="fragment fade-in" --> Mob programming
* <!-- .element: class="fragment fade-in" --> Peer code review
* <!-- .element: class="fragment fade-in" --> Jak najszybsze dostarczanie zadań. Lepiej dostarczyć 4 na 8 zadań pracując po 2 osoby nad każdym niż 0/8 mając jednocześnie wszystkie rozpoczęte.
* <!-- .element: class="fragment fade-in" --> Brak odgórnych przypisań osób do zadań. Osoba która właśnie ma czas bierze pierwsze z góry zadanie (lub jedno z pierwszych, jeśli nie są zablokowane)
* <!-- .element: class="fragment fade-in" --> 1 osoba może maksymalnie mieć przypisane tylko 1 zadanie w danej chwili. Dopiero po zakończeniu poprzedniego zadania można wziąć kolejne.

___

## [Agile manifesto](https://agilemanifesto.org)

> Odkrywamy nowe metody programowania dzięki praktyce w programowaniu i wspieraniu w nim innych. W wyniku naszej pracy, zaczęliśmy bardziej cenić:
>
> **Ludzi i interakcje** od procesów i narzędzi
>
> **Działające oprogramowanie** od szczegółowej dokumentacji
>
> **Współpracę z klientem** od negocjacji umów
>
> **Reagowanie na zmiany** od realizacji założonego planu.
>
> Oznacza to, że elementy wypisane po prawej są wartościowe, ale większą wartość mają dla nas te, które wypisano po lewej.

___

## Q&A
