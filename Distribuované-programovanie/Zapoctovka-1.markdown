* Aky druh komunikacie pouziva ShutdownListener + triedy ktore pouziva?
  * UDP komunikacia - vyuziva sa pomocny program StopShareMe.
  Server neustale sleduje vyhradeny UDP port pre spravy na ukoncenie aplikacie.
  Prijmu a znicia sa vsetky pakety, az kym sa neprijme korektny ukoncovaci paket, skladajuci sa z retazca:
  IConstants.EXIT_FLAG, znak medzera a heslo pre ukoncenie zhodujuce sa z heslom v konfig. subore.
  * Triedy: DatagramSocket, DatagramPacket, prijme sa retazec String

* Casovanie v GarbageCollectore
  * Po aktualizovani tabulky sa caka zvoleny casovy interval. Spravy "IAmAlive" maju obmedzenu platnost,
  preto ak uplynie niekolko intervalov po sebe a zaznam nie je obnoveny, musi byt z tabulky odstraneny.
  Odstranovanie sa realizuje po porovnani aktualneho casu s casom zaznamu tabulky - ak je rozdiel vacsi ako
  konstanta IConstants.LIFETIME_OF_HOSTINFOS, zaznam sa povazuje za expirovany a moze byt odstraneny z tabulky.

* Ci v IsAliveReceiver je na sockete timeout a dovod
  * Ano, nastavuje sa na hodnotu IConstants.IS_ALIVE_RECEIVER_TIMEOUT prostrednictvom metody setSoTimeout.
  * <strike>Dovod je, ze akonahle niektory uzol prestane vysielat spravy typu "IAmAlive", ostatne uzly v skupine ho po uplynuti
  prislusneho casoveho intervalu (timeout) vyradia zo zoznamu aktivnych uzlov.</strike>

Je tam cosi taketo:

    while(this.isRunning) {
    	try {
    		this.receiveIsAlivePacket();
    	} catch (SocketTimeoutException e) {
    		continue;
    	}
    }

Je tam 3-sekundovy timeout preto, aby dost casto kontrolovalo, ci sme nevypli receiver. Kebyze je 10 sekundovy timeout, tak sa to bude kontrolovat kazdych 10 sekund a ukoncenie programu by trvalo velmi dlho.

* Aky druh udajov prijima IsAliveReceiver
  * Prijimaju sa pakety obsahujuce serializovane objekty typu IHostInfoMessage. Pomocou ByteArrayInputStream sa
  nacitaju udaje z packetu a pomocou ObjectInputStream sa ziska samotny objekt.

* Konfiguracny subor jednotlivych uzlov + ako sa s tymi udajmmi naraba
  * Subor property je hlavnym konfiguracnym suborom systemu ShareMe. Nachadza sa v adresari 'resources'. Tento subor
  je pouzity ako konfiguracny subor kazdeho uzla pri jeho spusteni. Jeho pouzitim sa vyhneme uvadzaniu niektorych
  udajov priamo v zdrojovom kode systemu.
  * S udajmi sa naraba prostrednictvom premennej typu Properties a rozhrania IConstants.

* Ako sa ukoncuje vlakno shutdownlistener
  * Vlakno sa ukonci, ked sa posle ukoncovaci packet a pokial je zadane spravne ukoncovacie heslo daneho uzla.
  Spravny tvar ukoncovacie paketu: retazec IConstants.EXIT_FLAG, znak medzera a heslo zhodujuce sa s heslom v konfig. subore.

* Ake vlakna bezia v ulohe 1 vratane podulohy 1.5 - vymenovat iba 
  * Vlakno triedy ShutdownListener, IsAliveReceiver a vlakno GarbageCollectora (vnutornej triedy triedy HostListImpl)

* Synchronizacia isalive a garbagecollector
  * Musi sa zebezpecit pristup k tabulke v jednom casovom okamihu len pre jedno vlakno, aby metody put, get, contains a remove
  triedy HostListImpl neboli v konflikte s garbage collectorom, ktory odstranuje zaznamy z tabulky. Ako synchronizujuci
  objekt sa pouziva samotna hash-tabulka.

* Ake triedy su v implementacii shareme po 1.5 a nieco ako funguje shareme
  * Triedy: ShareMeImpl, ShutdownListener, IsAliveReceiver, HostListImpl (s vnutornou triedou GarbageCollector).

* Ake triedy pouziva isalivereceiver a aky druh komunikacie
  * Je to komunikacia prostrednictvom skupinovej komunikacie(multicast). Vyuzivaju sa triedy MulticastSocket, DatagramPacket, 
  prijate packety obsahuju objekty typu IHostInfoMessage

* Ci je timeout v shutdownlistenery a vysvetlit
  * V ShutdownListeneri nie je timeout, po spusteni je program zablokovany a caka na korektne ukoncovacie pakety, resp. sa
  da program ukoncit CTRL+C.

* Ako funguje casovanie v isalivesender
  * Casovanie je realizovane pomocou triedy TimerTask
  * V ShareMeImpl sa vytvori objekt triedy IsAliveSender a casovaca Timer, pomocou metody casovaca scheduleAtFixedRate() sa
  nastavi interval casovaca na hodnotu IConstants.IS_ALIVE_INTERVAL.

* Akeho typu je dotaz pre vyhladavanie
  * Typu ISearchRequest

14.Ktora trieda spusta vyhladavanie a na akych objektoch prebieha vyhladavanie
- Spusta ho trieda ShareMeImpl a jej metoda search(). Ziskava sa objekt typu ISearchResponse, z ktoreho sa extrahuje IFileList
  a ten sa nasledne prida do ISearchResult. Navratova hodnota je objekt ISearchResult obsahujuci vsetky objekty IFileList.

15.Ako sa spusta uloha 2 a ako sa ukoncuje
- Spusta sa prikazom, ktory si mozeme zobrazit prikazom ant run2_1 resp. ant run2_2. Ukoncenie - CTRL+c.

16.Akeho typu je trieda SearchEngine?
- kokotina, neni ziadneho typu

17.Co treba na kompilaciu a spustenie ulohy 2?
- Pouzitim RMI kompilatora sa vytvori stub triedy SearchEngineImpl.
- Kompiluje sa prikazmi ant lab2_1 a ant lab2_2.

18.Ako je strukturovana odpoved pri vyhladavani?
- Pomocou pola objektov typu IFile sa vytvori objekt typu IFileList, ten sa vyuziva pri vytvoreni navratovej hodnoty typu 
  ISearchResponse (pouzitim implementacnej triedy SearchResponseImpl, ktora sluzi na posielanie odpovede).

--------------------------------------------------------------------------------------------------------------------------
Dalsie otazky:

19.Ako prebieha vyhladavanie suborov
- Vyuziva sa komunikacia medzi distribuovanymi objektami v Jave - RMI(Remote Method Invocation). Spravy "IAmAlive" z ulohy 1
  obsahuju informacie aj o tom, ako a kde kontaktovat objekt uzla pomocou RMI. Vyhladanie suboru potom bude predstavovat postupne
  spracovanie zoznamu aktivnych uzlov a zasielanie vyhladavacieho dotazu kazdemu z nich. Na konci budeme mat zoznam uzlov, ktore
  mozu poskytnut hladany sobor.

20.Aky je tvar RMI URL adresy, ako ju ziskame
- rmi://{RMIRegistryHost}:{RMIRegistryPort}/{ServiceName}
- Iterativne sa prechadza zoznamom dostupnych uzlov a zo sprav IHostInfoMessage extrahujeme informacie o nazve RMI pocitaca
  (RMI registry host), RMI porte (RMI registry port) a nazve RMI sluzby (RMI service name). Potom mozeme vytvorit RMI URL adresu.

21.Ake ma parametre konstruktor triedy SearchEngineImpl, ake metody ma tato trieda
- ma 3 parametre: retazec fileBase(zodpoveda spristupnenemu adresaru sluzby ShareMe), retazec downloadURLPrefix (zodpoveda
  URL prefixu lokalneho uzla), a objekt typu IsecurityHelper
- metoda search() , vracia ISearchResponse

-------------------------------------------------------------------------

Minuly rok boli:

1. Share Me - konštruktor

2. či je použity Timer v IsAliveReceiver

3. ak typ udajov sa použiva v Receiver

4. Sender - triedy a komunikacia

5. komunikacia a triedy ShutdownLisener

6. či je potrebna registracia ak chcem vyhladavať

7. aka tieda je použivanan na vyhladavanie

8. akeho typu je Search EnginerImpl

9. tierdy a metody použite pri vyhladavani

10. akých hostou použivas pri vyhladavani alebo take niečo


----------------------------------------------------------------------

1. Co sa ako prve spusti v shareme (aka vlastnost)
2. Komunikacia shutdown listener + triedy 
3. Komunikacia IsAliveSender + triedy
4. Aky typ triedy sa pouziva na vyhladavanie 
5. Ktora trieda vola metodu hladania 
6. Ako je realizovane vykonavanie opakovanych cinnosti v garbage collector
7. Pouziva sa timeout v triede IsAliveReceiver? Dovod
8. Akeho typu su udaje co prijima IsAliveReceiver
9. Ktore uzly sa prehladavaju
10. Ci musi byt zaregistrovany rmi ak chces vyhladavat a dovod
