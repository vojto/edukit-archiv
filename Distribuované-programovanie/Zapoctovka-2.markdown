zapoctovka c2

- **Je pre system ShareMe potrebny nastroj idlj? Ak ano, za akym ucelom?**

Existuje IDL subor pre certifikacnu sluzbu, ktory sa pomocou nastroja idlj skompiluje a vytvori sa mnozina stub tried. 

- **Patri metoda registerKey do rozhrania ICertificationAuthority? Ak ano, uvedte/charakterizujte jej prototyp.**

`public boolean registerKey (String owner, byte[] key, String password)`

Neviem co je *prototyp metody*, ale asi myslia toto.

- **Kolko objektov certifikacnej autority je spustenych, ak bezi 10 uzlov ShareMe?**

Teraz neviem co myslia. Kazdy uzol ma svoje objekty, ktore sa staraju o komunikaciu s certifikacnou autoritou, ak myslia toto tak 10.

Ak myslia certifikacnu autoritu samotnu, tak potom iba 1.

Iny nazor: Podla mna je spusteny iba jeden objekt certifikacnej autority CORBA ORB v celom systeme shareme, pretoze pri inicializacii objektu pre pracu s CORBA sa vola ORB.init(), pricom tato trieda je sigleton, cize existuje iba jedna instancia na presne stanovenom porte (10050) na stanovenom hostitelskom pocitaci (dslab.fei.tuke.sk)

- **Ako a za akym ucelom sa komunikuje s certifikacnou autoritou v triede SearchEngineImpl?**

> Následne v metóde search() je vykonaný obrátený proces: najskôr je overená signatúra prichádzajúcej žiadosti (opäť získajte verejný kľúč žiadateľa od CA, extrahujte signatúru zo žiadosti a verifikujte ju použitím pomocného objektu ISecurityHelper). Ak došlá žiadosť nie je podpísaná (napr. uzol ešte nepodporuje bezpečnostnú infraštruktúru), akceptujte ju, ale odpovedajte nepodpísanou odpoveďou (t.j. ako signatúru použite null). Ak je podpis žiadosti neplatný, vyvolajte výnimku ShareMeException. V ďalšom kroku sa vykoná samotné vyhľadanie a výsledný objekt typu IFileList je podpísaný (resp. nie, ak samotný dotaz nebol podpísaný!). Výsledná signatúra (alebo null ak bola žiadosť nepodpísaná) je použitá v konštruktore pri vytváraní objektu typu ISearchResponse, ktorý je vrátený klientovi.

Po slovensky: Niekto chce u mna vyhladavat. Ak ma jeho request signaturu, tak ju vezmem, spytam sa certifikacnej autority, ci sedi, ak nahodou nie, thrownem chybu. Ak je vsetko ok, tak zoznam vyhladanych suborom podpisem a ulozim do responseSignature. Toto poslem do triedy SearchResponse. Ak request neobsahuje signaturu, tak na to kaslem a nic nepodpisujem.

- **Strucne charakterizujte HTTP server implementovany v ulohe 4 co do komunikacie sposobu 
realizacie svojich uloh (spojovanost, stavovost, pocet klientov)**

- **Akym sposobom server rozpozna, ktory z ovladacov typu IHTTPServerEntry ma pouzit na zodpovedanie dotazu klienta?**

HTTP server si udrziava zoznam objektov entry v datovej structure hashtable. Najprv sa entry zaregistruje pomocou metody `register`. Potom sa rozoberie request a podla toho, ake klucove slovo je v URL sa najde entry.

- **Vymenujte metody protokolu HTTP, ktore musi podporovat ShareMe uzol.**

`GET`

- **Obsah objektu akeho typu sa vyuziva pre vytvorenie navratovej hodnoty v metode getDocument () triedy ShareMeEntry?**
?THREAD?
- **Je nasledujuci dotaz spravny vzhladom na protokol http a system ShareMe? **
`GET /docs/test    test HTTP/1.0`

nie-nespravny format dotazu-obsahuje 4 casti, vrati chybovy dokument

- **Kolko obsluznych objektov je zaregistrovanych v korektne spustenom uzle ShareMe?**

7: `ShutdownListener`, `IsAliveReceiver`, `HostListImpl`, `IsAliveSender`, `SearchEngine`, `SecurityHelper`, `HTTPServer`

- **Patri metoda getKey do rozhrania ICertificationAuthority? Ak ano, uvedte/charakterizujte jej prototyp.**
-ano,patri.       KeyType getKey(int string owner) raises (CorbaCAException)

- **Bolo by možné komunikovať s certifikačnou autoritou v inom jazyku ako je Java(odpoved zdovodnite)**

- **Ake udaje su obsiahnute v objekte typu IDocument(aspon 3)**
-zoznam vlastnikov, zoznam liniek, zoznam suborov(ale nie som si tym ista)-opravte ma,ak sa mylim..

Podla mna to ma byt takto - cas poslednej modifikacie (getLastModified()), typ obsahu (getContentType()), dlzka toho obsahu (getContentLength()), obsah stranky (getContent()), cashe (getCachingInfo())

- **Ake objekty a typy su v ShareMe?**