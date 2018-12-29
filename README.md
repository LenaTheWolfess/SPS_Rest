# SPS_Rest

Rest (Representational State Transfer) je architektonický štýl vývoja webovej služby.
Je populárny pre jednoduchosť a preto, že je postavený nad existujúcimi systémami a možnosťami Http.

Výhody
```
interakcie sú založené na konštrukciách, ktoré sú vám známe ak ste oboznámený s Http
napríklad Rest používa návratové kódy z Http (404 - požadovaný objekt nebol nájdený, 200 - všetko je v poriadku )
pre zabezpečenú komunikáciu stačí využiť SSL a TLS
jazykovo nezávislý štýl architektúry
```
Nevýhody
```
používanie Http prináša limitácie (http neukladá stavy medzi správami - rest aplikácie sú bezstavové)
server neinformuje klientov o zmene (klient sa musí stále opýtať, či sa niečo zmenilo)
```
Operácie
```
GET - základná operácia pre získanie dát ( text / json / xml )
PUT - väčšinou sa používa pre update dát
DELETE - mazanie dát
POST - pridávanie dát ( a zložitejšie operácie )
```
Rest server sa dá vytvoriť napríklad pomocou
```
Spring Boot
čistý Spring
Restlet
```

Restlet framework je na stránke https://restlet.com/open-source/downloads/current/ ( zo spodnej časti si zoberieme pom-ko do mavenu )

Použijeme javu

Resource je súčasťou architektúry v Reste.
Na serveri sa definujú triedy rozširujúce ServerResource a pomocou anotácií @Get, @Post, @Put definujeme operácie pre daný resource.

Každý resource je spojený s inou url adresou. Pre server s viac ako jedným resourcom sa používa Component.
```
Component component ´new Component();
```
Potom sa nastaví protokol a port
```
component.getServers().add(Protocol.HTTP, 8182);
```
Treba spárovať url s resoursmi
```
component.getDefaultHost().attach("/nazov1", PrvyResource.class);
component.getDefaultHost().attach("/nazov2", DruhyResource.class);
component.getDefaultHost().attach("/nazov3/{parameter}", PodrobnyResource.class);
```
A stačí spustiť server
```
component.start();
```

V resource vieme ziskať parametre z url pomocou
```
getRequestAttributes().get("parameter")
```

Na strane klienta, možeme posielať požiadavky cez napríklad Postmana https://www.getpostman.com/
alebo si napísať klientovskú aplikáciu v jave.

Na strane klienta sa len potrebujeme pripojiť na správnu url adresu. Na to slúži ClientResource.
```
ClientResource clientResource = new ClientResource("htttp://adresaServera:Port/zvyšokPodľaResourcuKtorýChceme");
```
A ďalej pristupujeme cez získaný resource.
```
TriedaObjektu objekt = clientResource.get(TriedaObjektu.class);
clientResource.post(objektKtoryChcemePridať);
```

Na strane servera v príslušnom resource môžeme definovať
```
@Get("json")
public TriedaObjektu nejakyNazov() {
    return objekt;
}
@Post
public void nejakyInyNazov(novyObjekt) {
   // napriklad uloz novy objekt do uloziska
}
```

# Úloha 1
Stiahnite si zip empty a pripravte ako maven projekt.
Server sa spúšťa cez App.java, Console client cez Client.java, aplikácia pre klienta cez NewJDialog.java.
Trieda ProductList len obaľuje ArrayList - nič do nej netreba implementovať.

Vytvorte resource na strane servera pre predpripravený produkt, tak aby po poslaní požiadavky GET vrátil zoznam produktov.
Get sa dá otestovať cez url v prehliadači http://localhost:8182/products alebo pomocou postmana. 

# Úloha 2
Doplňte funkcionalitu pre pridanie nového produktu z klienta POST.
V Client.java sa pripojte na potrebný resource a otestujte POST a GET.

# Úloha 3
Doplňte resource pre samostatný produkt, tak aby sa pri požiadavke http://localhost:8182/product/1 vrátil len produkt s id 1 a otestujte v Client.java.
A podobne doplňte resource pre review, tak aby pri požiadavke http://localhost:8182/product/1/reviews sa vrátil len zoznam príslušných hodnotení a otestujte v Client.java.

# Úloha 4
Dopľnte NewJDialo.java tak, aby sa v ľavom liste zobrazil zoznam produktov, pričom po označení sa vypíše ich názov a cena v príslušných labeloch, a zobrazí sa zoznam hodnotení daného produktu.

# Úloha 5
Umožnite cez NewJDialog.java pridávať hodnotenia k označenému produktu.

Celkové možné riešenie sa nachádza v full.zip.
