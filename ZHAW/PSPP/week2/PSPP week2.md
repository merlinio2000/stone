
# (reguläre) Grammatik
#regulär #grammatik

Test ob grammatik regulär ist durch einsetzen:
E = T { "+" T }.
T = F { "\*" F }.
F = id.
-> ist regulär weil z.B. T + T -> F \* F + F -> id \* id + id 
E = F { "\*" F }.
F = id | "(" E ")".
-> ist *NICHT* regulär weil z.B. F * F -> id | E * id | E -> id | F\*F * id | F
Auch bei wiederholtem Einsetzen lassen sich E/F nicht eliminieren aus dem Ausdruck (gefangen in Rekursion)

