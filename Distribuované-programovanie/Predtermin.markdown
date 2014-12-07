# Ktore okruhy nie su spomenute v ziadnych otazkach

* Multicast
* Gossip protokoly
* QoS
* JNDI, Jini

To samozrejme neznamena, ze nebudu, ale je to dost pravdepodobne.

# Otazky z fora 09/10

Transparentnost subeznosti

Co znamena prenositelnost v DS

Centralizovany algoritmus pre cas

Definicia distribuovaneho systemu

Nieco s usporiadanym multicastom

Pomocou operácii socket, bind, listen, accept, connect, send, receive a close schematicky zobrazte aplikáciu typu klient-server používajúcu na komunikáciu posielanie správ podľa Berkeley socketov.

Nakreslit docasnu synchronnu komunikaciu s potvrdenim dorucenia na strane prijimatela

Ktore problemy DS sa riesili na prednaske

Ktoré z nasledujúcich okruhov v rámci distribuovaných systémov sme preberali počas prednášok?

      a. odolnost voci chybam
      b. súbežnosť (concurenncy)
      c. synchronizacia   
      d. bezpecnost

Ktoré z nasledujúcich komponentov infraštruktúry pre zabezpečenie RPC pouziva informaciu
identifikujucu vzdialenu metodu ci nejak tak...

      a. program klienta               d. dispatcher
      b. stub procedúra klienta      e. stub procedúra servera
      c. komunikačný modul          f. procedúra služby

Aká je úloha DCE démona pri naviazaní klienta na server v systémoch DCE RPC?

Ake objekty sa odovzdavaju formou odkazov pri RMI

Pre mutlipocitacovu HW platformu sa najlepsie hodi forma komunikacie:
a. Message passing interface MPI
b. BSD sokety
c. door IPC

Aku funkciu ma notify v systemoch s perzistentnymi spravami ci co

Stručne charakterizujte architektúru objektového servera typu „thread-per-request“

Uveďte a charakterizujte odlozeny synchrónny spôsob volania objektov v systéme CORBA (sémantika, popis)? 

Charakterizujte model callback pre asynchrónne volanie v sytéme CORBA? 

Doplňte potrebný kód aby mohlo byť rozhranie R1 rozhraním distribuovaného objektu:

      public interface R1 {
                public int urobNieco();
        }

Aké vyhľadávanie umožňuje adresárová služba na rozdiel od klasickej mennej služby?

Ktoré udalosti dáva do súvisu relácia stalo-sa-pred, ktorá sa využíva pri synchronizácii logických hodín?

# Dalsie otazky z fora: SKÚŠKA - RIADNY TERMÍN by Korgen

1. (3 body) Uveďte definíciu distribuovaného systému.
2. (2 body) Ktoré z nasledujúcich okruhov v rámci distribuovaných systémov sme preberali počas prednášok?
a. komunikácia
b. súbežnosť (concurenncy)
c. identifikácia/pomenovanie (naming)
d. bezpečnosť
3. (3 body) Vymenujte aspoň tri typy informácií, ktoré je žiaduce ukrývať pre zvýšenie transparentnosti v distribuovaných systémoch:
4. (3 body) Uveďte tri príklady obmedzenia škálovateľnosti vzhľadom na rozsah zaťaženia.
5. (2 body) Ktoré z nasledujúcich komponentov infraštruktúry pre zabezpečenie RPC sa podieľajú na kódovaní prenášaných údajov?
a. program klienta               d. dispatcher
b. stub procedúra klienta      e. stub procedúra servera
c. komunikačný modul          f. procedúra služby
6. (3 body) Aká je úloha DCE démona pri naviazaní klienta na server v systémoch DCE RPC?
7. (? body) Aká je sémantika odovzdávania vzdialených objektov ako parametrov pri RMI?
8. (? body) Znázornite časový diagram interakcie komunikačných partnerov pri perzistentnej synchrónnej komunikácii.
9. (? body) Pre aký typ hardvérovej platformy distribuovaného systému sa hodí komunikácia prostredníctvom socketov?
*NEVIETE NIEKTO?*
10. (? body) Vymenujte operácie základného rozhrania fronty v message-queuing systémoch?
11. (? body) Pomocou operácii socket, bind, listen, accept, connect, send, receive a close schematicky zobrazte aplikáciu typu klient-server používajúcu na komunikáciu posielanie správ podľa Berkeley socketov.
12. (4 body) Stručne charakterizujte architektúru objektového servera typu „thread-per-object“? 
13. (3 body) Uveďte a charakterizujte synchrónny spôsob volania objektov v systéme CORBA (sémantika, popis)? 
14. (3 body) Charakterizujte model callback pre asynchrónne volanie v sytéme CORBA? 
15. (3 body) Uveďte definíciu mena?
16. (4 body) Doplňte potrebný kód aby mohlo byť rozhranie R1 rozhraním distribuovaného objektu: 
public interface R1 {
          public int urobNieco();
  }
17. (2 body) Služba internetu DNS využíva:
a. iteratívne rozlišovanie
b. rekurzívne rozlišovanie
c. kombináciu iteratívneho a rekurzívneho rozlišovania
18. (2 body) Aké vyhľadávanie umožňuje adresárová služba na rozdiel od klasickej mennej služby?
19. (2 body) Výhodou lokalizačnej služby je, že si aplikácie nemusia uchovávať:
a. ľudsky čitateľné mená entít
b. identifikátory
c. adresy entít
20. (4 body) Ktoré udalosti dáva do súvisu relácia stalo-sa-pred, ktorá sa využíva pri synchronizácii logických hodín?
21. (4 body) Pri nasledujúcich operáciách vzhľadom na klienta, môžeme hovoriť o konzistencii v rámci modelu:
a. monotónne čítanie
b. monotónny zápis
c. čítanie svojich zápisov
d. zápisy nasledujúce čítania
L1:  WS(x1)      R(x1)            
L2:           WS(x1:x2)       R(x1:x2)