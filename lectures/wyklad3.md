Wykład 1: 

---
title: "Reprezentacja informacji i wstęp do architektury komputerów"
---

## Bit

1. Dlaczego komputer rozumie tylko zera i jedynki?

Zanim napiszemy pierwszą linijkę kodu w C/C++, musimy zrozumieć, na czym ten kod będzie działał. Komputer to urządzenie elektroniczne, a jego "mózg" (procesor) składa się z miliardów mikroskopijnych przełączników – **tranzystorów**.

Tranzystor działa jak włącznik światła, ma tylko dwa stany fizyczne:

1. Brak napięcia (wyłączony) – co w logice zapisujemy jako 0.
2. Jest napięcie (włączony) – co w logice zapisujemy jako 1.

Pojedyncze zero lub jedynka to **Bit** (ang. _binary digit_). 
To najmniejsza możliwa porcja informacji.

Ponieważ jeden bit to za mało, by przekazać sensowną informację, komputery grupują je w paczki. Standardową paczką jest **Bajt** (_Byte_), który składa się z 8 bitów.

Jeden bajt pozwala na zapisanie $2^8=256$ unikalnych kombinacji.

## Systemy liczbowe w informatyce

My, ludzie, używamy systemu dziesiętnego (DEC), bo mamy 10 palców. 
Komputery używają systemu dwójkowego (BIN).

### System Binarny (Dwójkowy)

Każda pozycja w liczbie binarnej to kolejna potęga liczby 2 (zaczynając od prawej strony, od $2^0$).

Przykład: Jak komputer widzi liczbę 13?

W systemie binarnym to 1101. Dlaczego?
$$
1⋅2^3 + 1⋅2^2 + 0⋅2^1 +1⋅2^0 = 8+4+0+1 = 13
$$

### System Heksadecymalny (Szesnastkowy - HEX)

Zapisywanie długich ciągów zer i jedynek jest dla programisty niewygodne i łatwo o błąd. 
Dlatego inżynierowie wymyślili system szesnastkowy.

Dlaczego akurat 16? Ponieważ $16=2^4$

Oznacza to, że dokładnie 4 bity (pół bajta) można zastąpić jednym znakiem w systemie HEX. 
To idealny kompromis między maszyną a człowiekiem.

Do zapisu używamy cyfr `0-9` oraz liter `A-F` (gdzie A=10, B=11, ..., F=15).

#### Przykład:

Binarnie: `1010 1111` (8 bitów)

Dzielimy na pół: `1010` (dziesiętne 10, czyli A) oraz `1111` (dziesiętne 15, czyli F).

Zapis HEX: `AF` lub `0xAF` (w C/C++ przedrostek 0x oznacza system szesnastkowy).

## Jak komputer zapisuje tekst? (Kod ASCII)
   
Komputer nie "widzi" liter. Zna tylko liczby. Aby wyświetlić tekst, inżynierowie stworzyli tabelę kodową – swego rodzaju słownik. 
Najbardziej podstawowym standardem jest ASCII (_American Standard Code for Information Interchange_).

Każdemu znakowi przypisano konkretną wartość liczbową. Na przykład:

Litera 'A' to dziesiętnie 65 (binarnie 01000001).

Litera 'B' to 66.

Litera 'a' to 97.

Spacja to 32.

Wskazówka inżynierska: W języku C litera to pod spodem po prostu liczba (typ char to w rzeczywistości mała liczba całkowita). 
Możemy więc wykonać operację matematyczną: 'A' + 1 i otrzymamy 'B'!

## Problem liczb ujemnych: Jak zapisać minus?

Zapisywanie liczb dodatnich jest proste. Ale co z ujemnymi? 

Komputer nie ma fizycznego znaku "minus" (−) w pamięci RAM. Ma tylko zera i jedynki.

### Krok 1: Kod Znak-Moduł (ZM)

Pierwszy, najprostszy pomysł inżynierów. Zarezerwujmy najstarszy bit (ten najbardziej po lewej, tzw. MSB - _Most Significant Bit_) jako znak.

`0 = plus`

`1 = minus`

Przykład dla 8 bitów:
```
0000 0101 = +5

1000 0101 = −5
```

Problem z ZM: Mamy dwie reprezentacje zera: 0000 0000 (+0) oraz 1000 0000 (-0). 

Dla procesora to koszmar logiczny.

Musiałby sprawdzać każdy znak osobno przed wykonaniem dodawania, co wymaga skomplikowanych i wolnych układów scalonych.

### Krok 2: Kod U1 (Uzupełnień do jedności)

Aby uzyskać liczbę ujemną, negujemy wszystkie bity liczby dodatniej (zamieniamy 1→0, 0→1). 

Ten system był lepszy matematycznie, ale nadal miał problem "podwójnego zera" i wymagał korekt przy dodawaniu.

### Krok 3: Kod U2 (Uzupełnień do dwóch)

To system, którego używają dzisiaj absolutnie wszystkie procesory (i z którego będziecie korzystać w C/C++).

Aby uzyskać ujemną reprezentację liczby w U2:

- Weź liczbę dodatnią.
- Zaneguj wszystkie bity (jak w U1).
- Dodaj 1 do wyniku.

_Przykład_ dla +5 (na 8 bitach):
```
0000 0101 (+5)

1111 1010 (negacja)

1111 1011 (dodanie 1) → To jest -5 w U2!
```
Zapis matematyczny
:
W kodzie U2, najstarszy bit ma po prostu wagę ujemną. Całą resztę liczymy normalnie. Formalnie wartość liczby X na n bitach to:
$$
X_{(U2)} = -x_{n-1} \dot 2^{n-1} + \sum_{i=0}^{n-2} x_i \dot 2^i
$$

Dlaczego U2 wygrało i zdominowało świat technologii?

Geniusz U2 polega na tym, że dla procesora nie ma różnicy między dodawaniem a odejmowaniem. Procesor używa tego samego, prostego układu scalonego (sumatora) niezależnie od tego, czy liczby są dodatnie, czy ujemne. Kwestia znaku rozwiązuje się "sama" w bitach.

## Zjawisko Przepełnienia (Overflow)

 Jeśli mamy zmienną 8-bitową ze znakiem, największa liczba, jaką zapiszemy, to `+127` `(0111 1111)`.
> Co się stanie, jeśli dodamy do niej 1?
> 
Otrzymamy `1000 0000`. 

Najstarszy bit stał się jedynką. Procesor uzna to za liczbę ujemną (dokładnie `−128`).

Program nie wyrzuci błędu kompilacji! Po prostu nagle z wartości dodatniej zrobi się ujemna, co w wojskowych lub lotniczych systemach sterowania jest błędem krytycznym. 
To zjawisko nazywamy **przepełnieniem całkowitoliczbowym** (Integer Overflow) i jako programiści musicie zawsze dobierać odpowiednio duże typy zmiennych do Waszych problemów.