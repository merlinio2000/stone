
basierend auf [[Logik#Horn Klausel]]

# Syntax
- $\land$ wird ,
- $\lor$ wird ;
- $\leftarrow$ wird :-
- Klauseln enden mit .

#### Regeln
[[Logik#Regel (definierte Hornklausel)]]

```
H :- B_1, B_2, ..., B_m

Bsp:
oma(X, Y) :- mutter(X, Z), mutter(Z, Y).
```


#### Fakten
[[Logik#Fakt (Faktenklausel)]]

```
D :-

Bsp:
oma(emma, klaus) :-.   # oft ohne :-
```

#### Anfragen
[[Logik#Anfrage (Zielklausel)]]

```
:- A

Bsp:
:- oma(X, klaus)
```


## Konventionen

#### Namensgebung 

Variablen:
Mit grossbuchstaben bezeichnet oder beginnen mit `_`
Bsp: `X` oder `_X`

Konstanten, Funktionen & Prädikatsnamen:
Beginnen mit kleinbuchstaben:
Bsp: `vater_von(hans, V)`

Funktionen verwenden meist Variabeln für Ein/Ausgabeparamter
Bsp: `sin(X, Y)` entspricht `Y := sin(X)`



### Rekursion

Vorsicht bei Linksrekursion!!
![[prolog_rekursion.png]]


### (Un-)Gleichheit

Es soll ein bestimmter wert genommen (unifiziert) werden

Bsp: Vererbung an Nachfolger "Tina"
`erbe(X, Y) :- vorfahre(Y,X), X = tina.`
Bsp: enterbung von "Tina"
`erbe(X, Y) :- vorfahre(Y,X), X \= tina.`

**Beliebige** Unifikation mit spezieller Variable `_`
Bsp: X kennt alle deren Vater bekannt ist
`kennt_vater(X) :- vater(_, X).`
Der `_` kann interpretiert weden alls beliebiges Element in der Faktenbasis


### Eindeutigkeit
![[prolog_eindeutigkeit.png]]


### Negation

Mit Hornklauseln kann man **KEINE** Negation (not) Ausdrücken.
Prolog erlaubt dies Aber mit einer geigneten Interpretation des NOT operator

Eine davon ist
#### Negation-as-Failure (NAF)
Gängigste NOT interpretation

Umgs: "not(G) folgt aus der Wissensbasis, wenn der Beweis von G in endlicher Zeit scheitert" -> "G ist nicht beweisbar" -> "da G nicht aus WB folgt muss G falsch sein"

Bsp:
![[prolog_NAF.png]]



## Listen

`X = [carl, gustav, bertha]`

Verkettete Listen der Form `[Head | Tail]` (`|` Restlistenoperator)

Beispiele:
```
p([X, Y, Z]).
	X = carl
	Y = gustav
	Z = bertha
p([X | Y]).
	X = carl
	Y = [gustav, bertha]
p([X, Y | Z]).
	X = carl
	Y = gustav
	Z = [bertha]
```



#### Operationen auf Listen

- `sumlist(L, S)` um die Liste L zu summieren
- `member(X, L)` um zu überprüfen ob $X \in L$
- `append(L1, L2, L1_L2)` konkateniert L1 und L2 zusammen
- `setof(Template, Goal, Set)` Erzeugen eines Sets mit allen möglichen Unifikationen
	- Bsp: `setof(X, mutter(tina, X), S) -> S = [anna, nimo, pete]`



### Fail

`fail` Löst manuell Backtracking aus (alle weiteren Variablenbindungen ausprobieren), siehe .e.g [[#CUT für Negation]], [[#IO]]


## CUT

spezielles Literal `!` welches immer erfüllt ist
Kann benutzt werden um den Suchbaum zu "Beschneiden", behält momentane Variablenbedingungen (Unifikationen) bei

Beispiel: Definition von `member` aus [[#Operationen auf Listen]] die bei erster übereinstimmung Rekusion abbricht.
```
member(X, [X|_]) :- !.
member(X, [_|Y]) :- member(X, Y), !.
```


#### CUT für Negation

![[cut_negation.png]]




## Dynamische Fakten/Regeln

Mit bsp: `assert(vater(ulf, tina)).` können dynamisch zur laufzeit neue Fakten und Regeln zur Faktenbasis hinzugefügt werden (greift nicht wenn File via `consult` geladen wird)
Umgekehrt löscht `retract` solche Regeln




### IO

- `write(X)` Ausgabe
- `nl` Newline
- `read(X)` Eingabe (muss mit `.` abgeschlossen werden)

Bsp: Alle Kinder ausgeben

```
all_kinder(X) :- elternteil(X, Y), write(Y), nl, fail.
```

Fail sorgt hier dafür dass alle Variablenbindungen ausprobiert werden


## Beispiele

![[prolog_bsp.png]]


Fakultät:
![[prolog_bsp_factorial.png]]