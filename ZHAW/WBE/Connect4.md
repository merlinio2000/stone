
Team: Merlin Maggi
Link: [https://github.zhaw.ch/pages/maggimer/WBE_labs/](https://github.zhaw.ch/pages/maggimer/WBE_labs/)

### Features 

- Reset - das Spiel zurücksetzen
- Load/Store - des momentanen Spielstands (LocalStorage)
- Undo - beliebig oft, bis zum Spielbeginn
- Erkennen des Gewinners
- Animation welche die einzelnen Stücke in Position bringt
- Responsive Design

### Implementation

Das UI ist responsive gehalten (Mobile Kompatibilität nicht enthalten), das Grundsätzliche Layout besteht aus mehreren `flex` Containern.
Das Brett selbst ist mit einem fix definierten `grid` Layout gelöst

Aus Interesse an der Zukunft verwendet der gesamte Code das `ESModules`  System,
ebenso sind fast überall `TypeScript` Typ-Definitionen in Form von `JSDoc`-Kommentaren
vorhanden.

Weil ich schon länger neugierig betreffend WebComponents war, habe ich diese
Gelegenheit genutzt und wo sinnvol (hier die einzelnen Felder des Bretts) einzelne
Komponenten gezielt mittels WebComponents eingekapselt und logisch wie auch visuell vom rest isoliert.

Aus Interesse an der `Web Animations API` wurde ebenfalls eine programmatische
Animation umgesetzt, welche bei einem Klick auf das Brett das Stück in den Korrekten Slot
"fallen lässt"

Da mir Frameworks wie Angular und Vue bereits länger geläufig sind wollte ich ebenfalls
einen "direkteren" ansatz Ausprobieren. Die meisten DOM-Operationen werden manuell
oder mittels vorgegebener `elt` Funktion gemacht.
Dies mit dem Ziel DOM-Modifikationen auf ein minimum zu bringen und auch nur gezielte Updates vorzunehmen, ohne den Overhead eines VirtualDOM (React etc.)

Generell wurde bei der Implementierung auf Speicherverbrauch und Effizienz Rücksicht genommen. Ebenso wurde geachtet, dass die Anzahl Reihen & Spalten des Spielbretts generisch gelöst wurden. Zusammen mit der höchst effizienten Gewinn-überprüfung (linearer Aufwand), skaliert das Spiel problemlos auf ein 1000 x 1000 Spielbrett mit minimen Anpassungen

