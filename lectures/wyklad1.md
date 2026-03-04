---
title: "Fundamenty i Logika Programowania"
---

### Polecana literatura

1. Grębosz J.: Symfonia C++ Standard. Edition 2000, 2009.
2. Prata S.: Szkoła programowania. Język C. Helion.
3. Harris S., Ross J.: Algorytmy od podstaw. Helion.
4. Wróblewski P.: Algorytmy, struktury danych i techniki programowania. Helion.
5. Programowanie w C. Wikibooks. http://upload.wikimedia.org/wikibooks/pl/6/6a/C.pdf
6. Pyszczuk A.: Programowanie w języku C. http://www.arturpyszczuk.pl/files/c/pwc.pdf

---

## Algorytm: Przepis na rozwiązanie problemu

Algorytm to precyzyjna instrukcja krok po kroku, jak wykonać konkretne zadanie. 
To abstrakcyjny pomysł, który istnieje zanim jeszcze dotkniemy klawiatury.

### Kluczowe cechy algorytmu:

- **Skończoność:** Musi mieć wyraźny początek i koniec.
- **Jasność:** Każdy krok musi być jednoznaczny dla wykonawcy.
- **Efektywność:** Powinien rozwiązywać problem w optymalny sposób.

### Sposoby zapisu algorytmu:

1. **Opis słowny** (naturalny język).
2. **Pseudokod** (uproszczony zapis przypominający kod).
3. **Schemat blokowy** (wizualna prezentacja logiki).

> Zbiór dobrze zdefiniowanych kroków prowadzących do wykonania pewniego zadania 
>
> Matematycznie - skończony ciąg jasno zdefiniowanych czynności, konieczny do wykonania określonych zadań. 

> Algorytm przeprowadza **stan początkowy** do określonego **stanu końcowego**. 

Badaniem algorytmów zajmuje się algorytmika. 

## Program: Algorytm wcielony w życie

Program to algorytm zapisany w **języku programowania**. 
Język ten stanowi pomost między ludzkim myśleniem a binarną logiką procesora.

### Poziomy abstrakcji języków:

- **Niskopoziomowe (np. Assembler):** Bliskie sprzętowi, trudne dla człowieka, dają pełną kontrolę.
- **Wysokopoziomowe (np. C++, Python, Java):** Bardziej zrozumiałe dla ludzi, ukrywają techniczne detale sprzętu.

```C++
#include <stdio.h> 
main ()
{
    int a = 4;
    int b = 2;
    if (a>=b)
    printf("a większe lub równe");
    else 
        print("a mniejsze lub równe");
    return 0;
}
```
Więcej o aktualnie używanych językach znajdziesz [tutaj](http://www.tiobe.com/index.php/content/paperinfo/tpci/index.html)

Algorytm wygodnie jest wyrażać za pomocą schematu blokowego.
Pokazuje czynności, działania, instrukcej i wzajemne relacje. 

<img src="../img/rys0.png" class="center" >

<img src="../img/rys1.png" class="center">


### Jak kod staje się działaniem?

- **Kod źródłowy:** Plik tekstowy napisany przez programistę.
- **Kompilator (C++):** Tłumaczy cały kod na raz do pliku wykonywalnego (szybkość).
- **Interpreter (Python):** Czyta i wykonuje kod linijka po linijce (elastyczność).


##  Paradygmaty: Jak myślimy o programie?

To, jak podchodzimy do pisania programu, zależy od wybranego paradygmatu:

- **Programowanie proceduralne:** Skupiamy się na funkcjach i czynnościach ("zrób to, potem tamto").
- **Programowanie obiektowe (OOP):** Skupiamy się na "bytach" (obiektach), które mają swoje dane i potrafią wykonywać operacje. **To będzie główny temat naszego kursu.**

Oprócz klasycznego podziału na procedury i obiekty, wyróżniamy podejścia, które całkowicie zmieniają sposób pracy z danymi:

- **Programowanie funkcyjne**

Zamiast wydawać komputerowi instrukcje krok po kroku ("zmień tę zmienną"), traktujemy program jak rozwiązywanie funkcji matematycznych.

Kluczowe cechy:

1. Immutability (Niezmienność): Dane raz stworzone nie mogą być zmienione. Zamiast zmieniać listę, tworzymy nową, zmodyfikowaną.
2. Pure Functions (Czyste funkcje): Funkcja dla tych samych danych zawsze zwraca ten sam wynik i nie zmienia nic "na zewnątrz" (brak efektów ubocznych).
3. First-class functions: Funkcje można przekazywać jako argumenty do innych funkcji (tak jak liczby).

Przykłady: Haskell, Lisp, Elixir (oraz nowoczesne dodatki w C++, Java czy JavaScript).

## Programowanie różniczkowalne (Differentiable Programming) & Autograd

To nowoczesny paradygmat, który stał się fundamentem współczesnej Sztucznej Inteligencji (Deep Learning).

Czym jest Autograd? To mechanizm automatycznego różniczkowania (Automatic Differentiation). Pozwala on programowi na automatyczne obliczanie pochodnych funkcji, które sami napisaliśmy.
Dzięki temu algorytm może sam "nauczyć się", jak poprawić swoje parametry, aby zminimalizować błąd (np. w sieciach neuronowych).

**Logika**: Program nie tylko wykonuje operacje, ale potrafi śledzić, jak każda operacja wpłynęła na wynik końcowy, co pozwala na "cofnięcie się" i optymalizację (tzw. backpropagation).

**Przykłady**: Biblioteki takie jak PyTorch, Pennylane, TensorFlow, JAX.

### Programowanie deklaratywne (Declarative)

Opisujesz co chcesz uzyskać, a nie jak ma to zrobić komputer.

Programowanie Logiczne: Definiujesz fakty i relacje, a komputer wyciąga wnioski (np. Prolog).
```prolog
% FAKTY (Facts)
% rodzic(Kto, Kogo).
rodzic(jan, anna).
rodzic(jan, marek).
rodzic(anna, piotr).
rodzic(marek, kasia).

% REGUŁY (Rules)
% X jest dziadkiem Y, JEŻELI X jest rodzicem Z, ORAZ Z jest rodzicem Y.
dziadek(X, Y) :-
    rodzic(X, Z),
    rodzic(Z, Y).

% X i Y są rodzeństwem, JEŻELI mają tego samego rodzica Z,
% ORAZ X i Y to nie ta sama osoba.
rodzenstwo(X, Y) :-
    rodzic(Z, X),
    rodzic(Z, Y),
    X \= Y.
```

Zapytania (SQL): Nie piszesz pętli przeszukującej bazę danych, tylko prosisz: "Daj mi wszystkich użytkowników z Warszawy".

```sql
SELECT * FROM users WHERE city="Warszawa"
```

## Anatomia działającego programu

Gdy uruchamiasz program, system operacyjny tworzy **proces**. 
To "żyjąca" instancja Twojego kodu w pamięci RAM.

| Obszar | Co zawiera? | Rola w programie |
| :--- | :--- | :--- |
| **Segment Kodu** | Instrukcje procesora | "Co mam zrobić?" (np. dodaj, skocz, porównaj) |
| **Segment Danych** | Zmienne, stałe, teksty | "Na czym mam to zrobić?" (np. liczby, imiona, adresy) |

**Mechanizm działania:**

Procesor pobiera instrukcję z segmentu kodu, pobiera potrzebne dane z segmentu danych, wykonuje operację i zapisuje wynik. Jeśli proces przebiega zgodnie z algorytmem, program kończy się sukcesem. Błąd w logice lub naruszenie dostępu do pamięci skutkuje błędem (bugiem).


**Program komputerowy** to sekwencja symboli opisująca obliczenia zgodnie z pewnymi regułami zwanymi językiem programowania. 

Program jest zazwyczaj wykonywany przez komputer, czasami bezpośrednio – jeśli wyrażony jest w języku zrozumiałym dla danej maszyny lub pośrednio – gdy jest kompilowany lub interpretowany przez inny program.

Formalne wyrażenie metody obliczeniowej w postaci języka zrozumiałego dla człowieka nazywane jest **kodem źródłowym**, podczas gdy program wyrażony w postaci zrozumiałej dla
maszyny (to jest za pomocą ciągu zer i jedynek) nazywany jest **kodem maszynowym** bądź
postacią binarną (wykonywalną).

**Kompilator** tłumaczy kod źródłowy zapisany w danym języku programowania na kod maszynowy, dzięki czemu możliwe staje się jego późniejsze uruchomienie. 

**Interpreter** natomiast odczytuje kod źródłowy na bieżąco, analizuje go i wykonuje kolejne porcje przetłumaczonego kodu. 
Programy przeznaczone do interpretacji często nazywane są **skryptami**.


Programy komputerowe można zaklasyfikować według ich zastosowań: aplikacje użytkowe, systemy operacyjne, gry wideo, kompilatory i inne.

W najprostszym modelu **wykonanie programu** polega na umieszczeniu go w pamięci operacyjnej komputera i wskazaniu procesorowi adresu pierwszej instrukcji.
Po tych czynnościach procesor będzie wykonywał kolejne instrukcje programu, aż do jego zakończenia. 

Program może zakończyć się w dwojaki sposób: poprawnie lub błędnie.

Program komputerowy będący w trakcie wykonania nazywany jest **procesem** lub **zadaniem**.

Program można podzielić na dwie części (obszary):

- część kodu (składającą się z instrukcji sterujących działaniem procesora),
- część danych (składającą się z danych wykorzystywanych i opracowywanych przez
program, np. adresów pamięci, stałych liczbowych, komunikatów tekstowych).

Programowanie jest procesem tworzenia programów. Jest to cykliczny proces polegający na:

- edycji kodu źródłowego (implementacja),
- uruchamianiu programu (kompilacja),
- analizie działania,
- powrocie do edycji kodu źródłowego w celu poprawienia błędów lub dalszego posze-
rania funkcjonalności.

Przed przystąpieniem do programowania należy określić cel programu i zaprojektować program (tu przydają się schematy blokowe). 
Kod źródłowy zapisuje się w pliku tekstowym (w języku C plik taki ma rozszerzenie *.c lub *.cpp)