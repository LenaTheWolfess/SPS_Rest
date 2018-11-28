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

