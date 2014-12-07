# Quine-McCluskeyho metoda

## Skupiny

* Funkcie budeme spajat do skupin, skupiny sa vytvoria urobenim parov zo vsetkych funkcii (v pripde troch): *f1xf2, f1xf3, f2xf3, f1xf2xf3*.
	* pozn: x znamena logicky sucin v mojom zapise
* Pre kazdu skupinu urobime skupinovu mapu

* Takto sme zredukovali pocet jedniciek
* Mozme zapisat f2xf3 a bude ovela jednoduchsia: !a !b !c !d + a b !c

* Teraz mame vyjadrene vsetky skupiny a ich minimalne formy.

## Skupinova funkcia

* Dalej ziskame velku skupinovu funkciu, ktoru ziskame *logickym suctom* funkcii f1…f3 (alebo kolko-kolvek ich mame.) 
	* Vysledkom bude asi funkcia, ktora ma same jednicky, iba semtam nulu. (kedze to OR-ujeme.)

## Hodnotiaca funkcia

* Suma 2^(k-1) * fi(a, b, c, d)
	* Cize vynasobime mocninu dvojky jednickou alebo nulkou
	* A potom ich vsektky spocitame
	* Toto robime pre kazdu bunku Karnaughovej mapy -- teda pre kazdu kombinaciu abcd

## Zapisanie vsetkeho do tabulky
