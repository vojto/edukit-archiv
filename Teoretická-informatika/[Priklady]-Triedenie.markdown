# Predikaty a operatory

- `d(Y1, K)` - Postupnost M je na konci
- `l > r | Y1` Prvok vlavo do indikatora je vacsi ako prvok vpravo
- `l < r | Y1` Prvok vlavo je mensi

![obrazok](http://hron.fei.tuke.sk/~rinik/data/Screen%20Shot%202013-01-10%20at%2010.49.28%20AM.png)

# Zostrojte algoritmus Dijkstra pre triedenie postupnosti pouzitim Minimalneho prvku zostupne.

Dominika Hurajtová triedenie pouzitim minimalneho prvku je select sort, to ze je zostupne znamena ze ide od najväcsieho po najmensi, vyberies sice minimalny prvok, ale vymenis ho z väcsim l (Y1) < l (Y2) transp(l(Y1), l(Y2))

Matúš Sulír Oproti vzostupnému stačí zmeniť znamienko? V tom selection_sort__zostupne.png (čo tu niekto uploadol, to s červenými písmenami) je to zbytočne zložité, nie?

![obrazok](http://dl.dropbox.com/u/4446823/selection%20sort.jpg)

Muf Muphistopheles ked vymenis znamienko bude to zostupne triedenie pouzitim maximalneho prvku.

Matúš Sulír A to už prečo?

Muf Muphistopheles aky prvok ukladas do usporiadaneho zoznamu? minimalny ci maximalny?

Dominika Hurajtová ale vyhladavas minimalny

Dominika Hurajtová neviem, je fakt mozne, ze sa mylim, ale nic ine som nenasla nikde, iba ze selection sort = triedenie minimalneho prvku

Pavol Daňo dominika ma pravdu.nemyli sa.

Matúš Sulír Ešte ma napadlo, že to mohol chcieť tak, že ak je triedenie vzostupné a vyberaný má byť maximálny prvok, tak tá utriedená postupnosť bude pribúdať sprava a nie zľava. Dáva to logiku. Tým pádom by bol ale pôvodný selection_sort.png riešením pre "vzostupne, minimálnym prvkom", čo sa v minuloročných zadaniach nenachádza.

Dominika Hurajtová no ano lebo je to zakladny algoritmus, ktory je zostaveny na vzostupne utriedovanie, cize mas pravdu je to vzostupne minimalnym prvkom

Jozef Ferko Mne to tiez vychadza iba na tu zmenu znamienka. Pozeral som rozne algoritmy a pseudokody, v ktorych bolo zmenene iba znamienko 

Pavol Daňo @edit: pouzitim minimalneho prvku zostupne treba menit viac veci nez len porovnanie, vraj Martin Kriska daval tu kdesi poupraveny obrazok co treba zmenit abo to bolo zostupne
