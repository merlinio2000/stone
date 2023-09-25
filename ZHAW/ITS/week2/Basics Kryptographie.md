

# Ziele

- Confidentiality: nur berechtigte können Nachricht lesen/entziffern
- Integrity: Nachricht wird empfangen wie sie versendet wurde
- Authenticity: Empfänger kann sicher sein dass Nachricht tatsächlich vom Sender stammt
- Non-Repudiation: Empfänger kann nach Erhalt nicht abstreiten dass sie die Nachricht empfangen wurde
- Freshness: Nachrichten können nicht abgefangen und später nochmals gesendet werden


# Kommunikationsmodell
#alice
- Alice: sendet Nachricht an Bob
- Bob: empfängt von Alice
- Eve: Attacker, kann mitlesen aber nicht verändern
- Mallory: 2. Attacker, kann mitlesen und verändern
- Trent: Drittperson der Alice & Bob vertrauen, unterstützt (e.g. CA)

# Verschlüsselungsmodell
- Plaintext p
- Schlüssel k
- Ciphertext c
-> Intercept durch Attacker veränderter
- Ciphertext c'
- Plaintext p'

Notation für Ver-/Entschlüsslung $c = E[k](p)$ / $p' = D[k](c')$



# Attacken 

**Attacker kann...**
- Ciphertext-only: von Ciphertext Rückschlüsse auf Plaintext oder Key ziehen
- Chosen-ciphertext: Ciphertexte generieren und vom System entschlüsseln lassen.
	- Attacker bekommt dadurch *entweder* Plaintext (und kann daraus auf Key zurückschlissen)
	- *ODER*
	- nur Teilinformationen wie Entschlüsselung OK/NOK 
- Known-plaintext: Rückschlüsse auf andere Plaintexte oder Key machen durch Kentniss von anderen Plain-Ciphertext Paaren
- Chosen-plaintext: Plaintexte wählen die dass System verschlüsselt. Mit dem resultierenden Ciphertext können Rückschlüsse auf andere Plaintexte oder sogar Key gezogen werden
- Brute-force: Alles ausprobieren bis Resultat sinnvoll erscheint

# Work Faktor

Abhängig von:
- Verschlüsselungsalgo
- Keylen
- Randomness des Key: Work Faktor ist maximal falls alle Keys gleich wahrscheinlich

Work Faktor Zeit wird an unrealistisch Schnellem System gemessen mit $10^9$ Chips die je in $10^{-12}s$ einen Key probieren können

|Work Factor|avg sec| avg year|
|---|---|---|
|$2^{64}$|1.8e-2|-|
|$2^{96}$|7.9e7|2.5|
|$2^{128}$|3.4e17|1.1e10|
|$2^{256}$|1.2e56|3.7e48|

Aus Tabelle wird ein work factor von $2^{128}$ als sicher betrachtet.
umrechnen in bits -> work factor $128$ bits ($2^n$ -> $n$ bits)

# Perfect Secrecy
#vernam #one-time-pad

Informationstheorietisch sicher: Algorithmus bei dem den ursprünglichen Plaintext nicht erkennt selbst nach ausprobieren aller schlüssel. (auch gennant **Perfect Secrecy**)
Aktuell nur ein solcher Algo: **One-Time-Pad (Vernam Cipher)**
![[Pasted image 20230925153827.png]]


# Kryptographisch sichere Algorithmen

Eigenschaften: 
- allg. bekannt
- keine Fehler bekannt
- Work Factor $> 128$ bits

