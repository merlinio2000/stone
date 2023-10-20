# Horn Klausel

Ein **Disjunktionsterm** -> disjunktion von atomaren Literalen $\Phi_i$ (oder negiert atomar)
$$
\Large \Phi_1 \lor \Phi_2 \lor \Phi_3 \lor ... \lor \Phi_n
$$

Eine **Horn-Klausel** ist eine solche Klausel mit HÖCHSTENS einem positiven (d.h. nicht negierten) Literal


### Arten von Hornklauseln

#### Regel (definierte Hornklausel)
- GENAU ein postivies Literal $\lnot a_1 \lor ... \lor \lnot a_n \lor y$
- Als implikation $a_1 \land ... \land a_n \implies y$
- "Wenn alle $a_i$ wahr sind dann auch $y$"
- Positives Literal $P$ genannt  Konklusion
- Negative literale $\lnot P_i$ genannt Prämissen

#### Fakt (Faktenklausel)
- Keine negativen Literale
- Als Implikation $1 \implies y$
- "$y$ ist wahr"

#### Anfrage (Zielklausel)
- kein positives Literal
- Als Implikation: $a_1 \land ... \land a_n \implies 0$
- "$a_i$ sind alle nicht wahr"

### Als Implikation

Horn-Klauseln lassen sich als Implikation darstellen:
$$
\large \lnot \Phi \lor \Psi = \Phi \implies \Psi
$$

"Wenn $\Phi$, dann $\Psi$"



### Inferenzregel für Horn-Klauseln

Ordered-Linear Resolution for Definite Claused (OLD)
![[OLD_inferenz.png]]
![[OLD_bsp_sokrates.png]]