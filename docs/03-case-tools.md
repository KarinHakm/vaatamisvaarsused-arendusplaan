# 3. CASE-vahendid

## 3.1 Mis on CASE-vahend?

CASE (Computer-Aided Software Engineering) tähendab arvutiga toetatud tarkvaraarendust. CASE-vahend on programm, mis aitab mõnda tarkvaraarenduse tegevust teha kiiremini, korrektsemalt või nähtavamalt. Näiteks aitab see süsteemi modelleerida, töid planeerida või muudatusi hallata.

Selles projektis kasutan CASE-vahendeid peamiselt **disainietapis** (arhitektuuri ja andmevoo modelleerimine) ning **planeerimisel ja dokumenteerimisel**.

## 3.2 Projektis kasutatud vahendid

| Vahend | Liik | Milleks kasutan | Tulemus projektis | Seis |
|---|---|---|---|---|
| **diagrams.net** | Modelleerimine ja disain | Arhitektuuriskeem | Lähtefail `diagrams/architecture.drawio` ja sellest eksporditud pilt `diagrams/architecture.png` | kasutatud |
| **PlantUML** | Modelleerimine (UML) | Andmevoo järjestusskeem | Lähtefail `diagrams/filter-flow.puml` ja sellest genereeritud pilt `diagrams/filter-flow.png` | kasutatud |
| **Git ja GitHub** | Versioonihaldus | Dokumentide ja skeemide muudatuste salvestamine | Repositoorium ja commit'ide ajalugu | kasutatud |
| **GitHub Projects** | Planeerimine | Kasutajalood ja sprindid tahvlil | – | **planeeritud, veel tegemata** |

**Õpetaja nõude täitmine:** nõue on kasutada vähemalt kahte tarkvaraarendust toetavat vahendit, millest vähemalt üks on modelleerimise või disaini vahend. Selle nõude täidavad **diagrams.net ja PlantUML**, sest mõlemad on modelleerimise vahendid ja mõlemaga on projektis skeem tehtud. Git ja GitHub on lisaks kasutusel versioonihalduseks. **GitHub Projects on praegu veel tegemata.** Arvestan seda nõude täitmisel alles siis, kui tahvel on loodud.

## 3.3 Milliseid arendustegevusi need vahendid toetavad

Tabel käsitleb laiemalt projektitöö tegevusi, mitte ainult arendusprotsessi etappe. Arendusprotsessi etapid on kirjeldatud failis `docs/01-development-process.md`.

| Tegevus | Vahend | Kuidas aitab |
|---|---|---|
| Nõuete analüüs ja planeerimine | GitHub Projects (planeeritud) | Kasutajalood, prioriteedid ja sprindid on ühes kohas ja nähtavad |
| Disain ja arhitektuur | diagrams.net | Näitab komponente ja nende seoseid ühel pildil |
| Disain ja arhitektuur | PlantUML | Näitab, kuidas päring liigub kihtide kaudu andmebaasini ja tagasi |
| Dokumenteerimine | diagrams.net, PlantUML | Skeemid on dokumentide sees piltidena ja lähtefailid on muudetavad |
| Muudatuste haldus | Git ja GitHub | Iga muudatus on salvestatud, seda saab võrrelda ja vajadusel tagasi võtta |
| Suhtlus kliendi ja meeskonnaga | diagrams.net | Pildilt on lahendust lihtsam selgitada kui tekstist |

## 3.4 diagrams.net meie projektis

**Mis see on:** toote ametlik nimi on **draw.io**. See on skeemide joonistamise rakendus, mille veebiversioon asub aadressil app.diagrams.net. [6] Selles dokumendis kasutan nime diagrams.net, sest nii on see nimetatud ka õpetaja ülesandes. Rakendust saab kasutada brauseris või töölauarakendusena ja selle lähtekood on avatud (Apache 2.0 litsents). [1] Skeem salvestatakse `.drawio` faili, mis on pakkimata XML-fail. [2]

**Näide:** arhitektuuriskeem `diagrams/architecture.drawio` (vt `docs/04-architecture.md`, punkt 4.3). Skeemil on kasutaja brauser, Spring Booti server koos kihtidega, PostgreSQL ja väline kaarditeenus.

**Kasutuskogemus:**
- Skeemi esimene versioon koostati AI-assistendi abiga XML-failina ja avati brauseris aadressil app.diagrams.net.
- Esimesel eksportimisel selgusid kujundusvead, mida failist lugedes ei näinud: üks silt puudutas kasti serva, teine ulatus silindri peale ja SQL-nool oli kõver. Vead parandati komponentide asukohti muutes ja pilt eksporditi uuesti.
- PNG tuli eksportida käsitsi. Brauser salvestas faili allalaadimiste kausta ja teisel korral nimega `architecture (1).png`, mistõttu tuli fail käsitsi õigesse kausta kopeerida.
- Eksportimisel sai valida „Include a copy of my diagram”. Siis on PNG-pildi sees ka muudetav skeem. [2]
- Võrdlesin skeemi faili enne ja pärast teist paigutuse parandust Git-i võrdluskäsuga (`git diff --no-index`). Muutunud oli 13 rida: komponentide asukohad ja suurused (näiteks `x="680"` muutus `x="740"`), noolte ühenduspunktid, joonistuslehe laius ja üks legendi tekst. Võrdlusest on raske aru saada, mis skeemil tegelikult muutus, sest muudatused on kirjas numbrite ja XML-atribuutidena.
- GitHub ei kuva `.drawio` lähtefaili tavalise pildina. Et skeem oleks dokumendis näha, tuleb sellest PNG-pilt eraldi eksportida ja repositooriumi lisada. Meie projektis on selleks `diagrams/architecture.png`.

## 3.5 PlantUML meie projektis

**Mis see on:** PlantUML on avatud lähtekoodiga tööriist, mis loob UML-skeeme tekstilisest kirjeldusest. [3] See vajab tööks Javat. Graphviz programmi on vaja ainult mõne skeemitüübi jaoks. [4]

**Näide:** maakonna filtri järjestusskeem `diagrams/filter-flow.puml` (vt `docs/04-architecture.md`, punkt 4.5). Lõik lähtekoodist (read 5–13):

    actor "Külastaja" as user
    participant "Veebiliides\n(HTML, CSS, JS, Leaflet)" as ui
    participant "API kiht\nAttractionController" as api
    participant "Äriloogika kiht\nAttractionService" as service
    participant "Andmekiht\nAttractionRepository" as repo
    database "PostgreSQL" as db

    user -> ui : valib maakonna "Saaremaa"
    ui -> api : GET /api/attractions?county=Saaremaa

**Kasutuskogemus:**
- Skeemi süntaksi sai kontrollida käsurealt (`java -jar ~/tools/plantuml.jar -checkonly diagrams/filter-flow.puml`) ja pildi genereerida ühe käsuga.
- Paigutuse teeb PlantUML ise, seega ei tekkinud kattuvaid silte ega kõveraid nooli. Samas ei saa ise täpselt määrata, kuhu miski skeemil läheb.
- Järjestusskeemi jaoks Graphvizi vaja ei läinud: seda polnud arvutisse paigaldatud ja pilt tekkis ikkagi.
- Kui lisasime rea `hide footbox` (peidab skeemi alt korduvad osaliste nimed), oli Git-is näha ainult üks lisatud rida. Muudatus oli kohe arusaadav.
- Esialgu polnud PlantUML-i arvutis. Skeemi tegemisel kasutati ajutiselt allalaaditud `.jar` faili. Hiljem paigaldati PlantUML (versioon 1.2026.8) püsivalt faili `~/tools/plantuml.jar`. See laaditi alla ametlikult GitHubi väljalasete lehelt ja selle SHA-256 kontrollsumma kontrolliti üle.
- GitHub ei kuva `.puml` lähtefaili tavalise pildina. GitHub kuvab Markdownis otse ainult nelja vormingut: mermaid, geoJSON, topoJSON ja ASCII STL. [5] Et skeem oleks dokumendis näha, tuleb PNG-pilt eraldi genereerida ja repositooriumi lisada. Meie projektis on selleks `diagrams/filter-flow.png`.

## 3.6 Võrdlustabel

| Tunnus | diagrams.net | PlantUML |
|---|---|---|
| Lähenemine | Joonistamine hiirega | Skeem kirjutatakse tekstina |
| Õppimine | Lihtne, saab kohe alustada | Tuleb õppida süntaksit |
| Paigutus | Kasutaja paneb kõik ise paika: täielik kontroll, aga rohkem käsitööd | Automaatne: kiire ja korrektne, aga vähem kontrolli |
| Sobib eriti hästi | Arhitektuuriskeemid, vabakujulised skeemid | UML-skeemid, eriti järjestusskeemid |
| Lähtefail | `.drawio` (XML) | `.puml` (lihttekst) |
| Muudatused Git-is | Raske lugeda (XML, koordinaadid) | Lihtne lugeda (iga rida on sisuline) |
| Pildi tegemine | Käsitsi eksport rakendusest | Üks käsk käsurealt |
| Mida on vaja | Brauser või töölauarakendus | Java, mõne skeemitüübi jaoks Graphviz [4] |
| GitHubis kuvamine | `.drawio` faili ei kuvata pildina. PNG tuleb eraldi eksportida ja lisada | `.puml` faili ei kuvata pildina [5]. PNG tuleb eraldi genereerida ja lisada |
| Kaitsmisel muutmine | Kiire, näha kohe ekraanil | Vaja teada süntaksit ja pilt uuesti genereerida |
| Litsents | Avatud lähtekood, Apache 2.0 [1] | Avatud lähtekood [3] |

## 3.7 Eelised ja puudused

### diagrams.net

**Eelised:**
- lihtne alustada, süntaksit pole vaja õppida;
- vaba paigutus: saab rühmitada komponente aladesse (brauser, server) ja kasutada värve;
- skeemi muutmine on näha kohe;
- sobib kliendile ja õpetajale lahenduse näitamiseks.

**Puudused:**
- paigutus on käsitöö: silte ja nooli tuli eraldi sättida;
- muudatusi on Git-is raske jälgida;
- pilt tuleb pärast iga muudatust käsitsi uuesti eksportida.

### PlantUML

**Eelised:**
- skeem on tekst: muudatused on Git-is selgelt näha;
- automaatne paigutus;
- järgib UML-i, sobib järjestusskeemideks;
- pildi saab teha ühe käsuga.

**Puudused:**
- tuleb õppida süntaksit;
- paigutust ei saa täpselt juhtida;
- vajab Javat;
- tulemust näeb alles pärast pildi genereerimist.

## 3.8 Miks kasutasime kumbagi

- **Arhitektuuriskeemi** jaoks valisin **diagrams.net-i**, sest arhitektuuriskeemil on oluline paigutus: mis asub brauseris, mis serveris ja mis on väline teenus. Seda on lihtsam joonistada kui tekstina kirjeldada. Lisaks on seda kaitsmisel kiire muuta.
- **Andmevoo** jaoks valisin **PlantUML-i**, sest järjestusskeem on standardne UML-skeem, mille paigutus on alati sama (osalised üleval, sõnumid ülalt alla). Tekstina on seda kiire kirjutada ja muuta.

## 3.9 Kuidas skeemi kaitsmisel muuta

**diagrams.net** – kaitsmisharjutus: mobiilirakenduse lisamine skeemile.

> See on harjutus skeemi muutmiseks. Mobiilirakendus on praegu prioriteediga Won't (US11, vt `docs/02-methodology-backlog.md`) ja selle võimalik lisamine on kirjeldatud failis `docs/04-architecture.md`, punkt 4.10.

1. Ava app.diagrams.net ja ava seal fail `diagrams/architecture.drawio` (näiteks menüüst **File → Open from → Device**).
2. Lohista vasakult paneelilt uus kast ja kirjuta sinna „Mobiilirakendus”. Paiguta kast **väljapoole „Kasutaja brauser” ala**, sest mobiilirakendus ei tööta brauseris.
3. Tõmba noolt kastist turvamoodulini ja kirjuta sildiks „HTTPS, REST API, JSON”.
4. Salvesta muudatus ja ekspordi PNG (**File → Export as → PNG**). Pärast salvestamist kontrolli, et muudatus jõudis faili `diagrams/architecture.drawio`, sest brauseris võib salvestamine luua hoopis allalaaditud koopia.

Menüü **File → Export as → PNG** on selles projektis kasutatud. Faili avamise ja salvestamise menüütoiminguid pole selles projektis läbi proovitud ja need võivad rakenduse versiooniti erineda.

**PlantUML** – kaitsmisharjutus: vahemälu lisamine skeemile.

> See on harjutus skeemi muutmiseks. Vahemälu on kirjeldatud ainult võimaliku tulevase lahendusena 100 korda suurema kasutajate arvu jaoks (vt `docs/04-architecture.md`, punkt 4.8). Praeguses plaanis ega olemasolevas skeemis seda ei ole.

1. Ava `diagrams/filter-flow.puml` tekstiredaktoris.
2. Lisa osaline, näiteks `participant "Vahemälu" as cache`.
3. Lisa sõnumid, näiteks `service -> cache : otsib vahemälust`.
4. Genereeri kõigepealt **proovipilt ajutisse kausta**, et olemasolev pilt säiliks. Käivita projekti juurkaustas:
   `java -jar ~/tools/plantuml.jar -tpng -o /tmp/plantuml-preview diagrams/filter-flow.puml`
   Proovipilt tekib faili `/tmp/plantuml-preview/filter-flow.png`.
5. Kui proovipilt on õige, genereeri lõplik pilt projekti juurkaustas:
   `java -jar ~/tools/plantuml.jar -tpng diagrams/filter-flow.puml`

**Hoiatus:** 5. sammu käsk kirjutab olemasoleva faili `diagrams/filter-flow.png` üle ilma küsimata. Kasuta `-o` järel alati **absoluutset teed** (nt `/tmp/...`). Suhteline tee arvestatakse `.puml` faili kausta suhtes ja tekitaks uue kausta `diagrams/` sisse.

Kaitsmisharjutuse ajal võib 5. sammu vahele jätta. Nii saab harjutada ilma repositooriumis olevat pilti muutmata.

## Allikad

1. jgraph. *drawio* (GitHubi repositoorium). <https://github.com/jgraph/drawio>
2. draw.io. *Save file formats.* <https://www.drawio.com/doc/faq/save-file-formats>
3. PlantUML. Ametlik veebileht. <https://plantuml.com/>
4. PlantUML. *Getting started.* <https://plantuml.com/starting>
5. GitHub Docs. *Creating diagrams.* <https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-diagrams>
6. draw.io. Ametlik veebileht. <https://www.drawio.com/>
