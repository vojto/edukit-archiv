# Minimalizacia

Chceme dostat co najjednoduchsi zapis. 

## Minimalna forma

Ako robime minimalnu: Hladam kontury tak, aby som spolu uzavrel 2^n jedniciek alebo neurcitych stavov.
* Mozu sa prekryvat
* Kontury by mali byt co najvacsia
* Maju pokryt vsetky jednicky

* Hladam take premenne, co su cele zakryte -- tie budu *priame*
* Tie premenne, ktorych indexy vobec nezasahuju do kontury su *negovane*. 

### Konjunktivna

* Hladam nuly a tie premenne, ktore maju hodnotu *nula* su *priame*, *jednicky* su *znegovane*. 

### Dizjunktivna

* Hladam jednotky a tie premenne, ktore maju hodnotu *jedna* su *priame*,  *nulky* su *znegovane*.