# Tohtorocne (2013)

A)

1. DWH, Staging area
2. Temporal DBs
3. Implementacia JOIN, vymenovat a opisat algoritmy
4. Optimalizacia request, relacna algebra

# Ostatne

toto som nasiel na fore
Vseobecny kanonicky dotazovaci strom ma formu:
Projekcie - Selekcie - Kartezky sucin tabuliek (predstav si to zvysle) 

Princim je v tom vykonat na zaklade pravidiel:
1. Projekcia(relacie R) = Projekcia1(Projekcia2(relacie R)) = Projekcia2(projekcie1(relacie R))
2. Selekcia (s vhodnou podmienkov spojenia) ( Relacia R Kartazsky sucin Relacia S) = Relacia R Spojenie (podmienka spojenia) Relacia S
3. Seleckcia (podmienka selekcie pre relaciu R) (kartezsky sucin Relacie R a S) = (selekcia (podmienka selekcie pre relaciu R) Kartazsky sucin Relacia S

na zaklade tychto podmienok sa snazis vytvorit efektivny strom v ktorom by bolo vyhladavanie najefektivnejsie, kedze kartezsky sucin tabuliek je pametovo narocny.
1. Rozbijes vsetobecnu selekciu na selekcie v pripade (pravidlo 1)
2. Vykonava sa tak, ze selekcie nad jednotlivymi tabulka na zaklade 3. pravidla prevedies k tymto tabulka,
3. na zaklade pravidla 2. vykonas joiny po tom co umiestnis tie podmienky nad nich.

pocuj, a ked sa robi select za WHERE f.Mesto = ënuernbergí and f.Firma = d.Firma and d.Vyrobok = o.Vyrobok
sa to vykonava zlava alebo podla pravidiel ze projekcia selekcia atd...

modelovanie d·t
UmoûÚuj˙ v˝voj·rom vytv·raù a udrûiavaù d·tovÈ modely pre zdrojov˝ch systÈmov a d·t datab·z d·tovÈho skladu. V prÌpade potreby mÙûu byù d·tovÈ modely vytvorenÈ pre pracovnej oblasti.
Poskytovaù dopredu inûinierske schopnosti generovaù schÈmu datab·zy.
Poskytovaù reverznÈ inûinierstvo schopnostÌ na zÌskanie ˙dajov z modelu slovnÌka d·t existuj˙cich source datab·z.
Poskytovaù dimenzion·lnÌ modelovanie d·t n·vrh·ra pre vytvorenie STAR schÈmy

1. Struktura DWH a ETL

2. Temporalne DB

3. RA - operacia join a jej implementacie

4. priklad - zrobit z daneho selectu kanonicky strom, optimalizovany strom a popisat kroky optimalizacie



toto bola B skupina

A skupina mala textove databazy a operaciu select

C skupina mala objektove db a operaciu mnozin



otazky boli (C skupina):

1. Struktura DWH a ETL

2.  OODB

3. RA - mnozinove operacie + algoritmy

4. priklad - zrobit z daneho selectu kanonicky strom, optimalizovany strom a popisat kroky optimalizacie



B skupina:

1. Struktura DWH, ETL a jej suvis so staging area

2. Temporalne DB

3. RA - join + algoritmy

4. priklad - urobit z daneho selectu kanonicky strom, optimalizovany strom a popisat kroky optimalizacie



Ano, ti co boli na opravnom isli do osobitneho radu a mam pocit, ze mali skupinu D, v ktorej bolo:

1. Struktura DW(obrazok) + metadata

2. Sposoby indexovania

3. Main memory DB

4. Zo zadaneho selectu urobit kanonicky strom a jeho optimalizaciu





toto som nasiel v predminulom roku :

databazove technologie ktore sme na prednaskach nepreberali

temporalne databazy,

objektove,

textove,

ETL a jeho struktura,

RA a algoritmy,

kanonicky strom a jeho optim

1. OLAP - Technologie, Multidimensional analyzy
2. Vysvetlite princip dvojfazoveho triedenia triedenim a zlucovanim (2-parse sort-merge)
2. Bezpecnost Databazy
- pristupove pr·va v DBS
- viacurovnova bezpecnost v DB(multilevel seciurity, MLS), BELLILA Padula MODEL.
- Discretionary a mandatory access (DAC a MAC) - MLS model security technologie v DBMS ORACLE - virtualne private databazy MLS
3. Strom