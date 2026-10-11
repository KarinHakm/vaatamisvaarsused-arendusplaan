# 2. Arendusmetoodika ja tööde nimekiri (backlog)

Eelmises dokumendis (`docs/01-development-process.md`) valisin iteratiivse ja inkrementaalse arendusmudeli. Selles dokumendis valin metoodika, mille järgi seda mudelit praktikas kasutada. Lisaks koostan kasutajalood, määran neile prioriteedid ja planeerin esimese sprindi.

## 2.1 Scrum ja Kanban

### Scrum

Scrum jagab töö kindla pikkusega sprintideks, mis kestavad kuni ühe kuu. [1] Igal sprindil on eesmärk ja selle lõpuks peab valmima töötav osa tootest (inkrement).

Scrumi meeskonnas on kolm vastutusala [1]:
- **tooteomanik (Product Owner)** järjestab tööde nimekirja ehk otsustab, mis on kõige väärtuslikum;
- **Scrum Master** aitab meeskonnal Scrumi järgida ja eemaldab takistusi;
- **arendajad (Developers)** teevad sprindi töö.

Scrumis on viis sündmust: sprint, sprindi planeerimine, igapäevane koosolek (Daily Scrum, 15 minutit), sprindi ülevaatus ja sprindi retrospektiiv. [1]

### Kanban

Kanban on viis, kuidas parandada töö liikumist (voogu) läbi protsessi. [2] Kanbani juhendis on kolm põhitegevust [2]:
- töövoo määramine ja nähtavaks tegemine, tavaliselt tahvlil veergudega;
- töös olevate ülesannete aktiivne juhtimine, sealhulgas **pooleliolevate tööde arvu piiramine** (WIP-piirang);
- töövoo pidev parandamine.

Kanbani juhend ei määra sprinte ega kindlaid rolle. Uut tööd alustatakse siis, kui pooleliolevate tööde piirang seda lubab. [2]

### Võrdlus

| Tunnus | Scrum | Kanban |
|---|---|---|
| Töö rütm | Kindla pikkusega sprindid | Pidev voog, sprinte pole |
| Planeerimine | Iga sprindi alguses valitakse tööd sprindi eesmärgi järgi | Tööd võetakse järjekorrast siis, kui eelmine on valmis |
| Rollid | Tooteomanik, Scrum Master, arendajad | Kindlaid rolle ei nõuta |
| Muudatused | Käimasoleva sprindi eesmärki ei ohustata, uued tööd lähevad järgmisesse sprinti | Järjekorda saab muuta igal ajal |
| Pooleliolevate tööde piiramine | Kaudselt, sest sprinti võetakse ainult nii palju tööd, kui jõutakse teha | Otseselt, iga veeru jaoks on WIP-piirang |
| Mõõdikud | Sprindi eesmärgi täitmine, valminud tööde maht sprindis | Pooleliolevate tööde arv, läbilaskevõime, töö vanus, tsükliaeg [2] |
| Kliendile tulemuse näitamine | Sprindi ülevaatusel iga sprindi lõpus | Siis, kui töö on valmis |
| Sobib hästi | Uue toote arendamiseks, kui on vaja regulaarset planeerimist ja tagasisidet | Hoolduseks ja tugitööks, kui tööd tulevad ettearvamatult |

### Miks valime Scrumi?

1. **Arendame uut toodet.** Kõigepealt on vaja teha põhifunktsioonid ja siis neid järk-järgult täiendada. Sprindid sobivad selleks hästi.
2. **Klient saab regulaarselt tagasisidet anda.** Sprindi ülevaatusel näeb klient iga kahe nädala tagant töötavat versiooni.
3. **Sprindi eesmärk hoiab tööd fookuses.** Iga sprint lahendab ühe selge probleemi, näiteks „kasutaja näeb vaatamisväärsusi kaardil”.
4. **Muutustega on lihtne toime tulla.** Kui nõuded muutuvad või tähtaeg lüheneb, muudab tooteomanik tööde nimekirja järjekorda ja järgmine sprint planeeritakse uute prioriteetide järgi.
5. **Sobib eelmises dokumendis valitud mudeliga.** Scrumi juhendi järgi kasutab Scrum iteratiivset ja inkrementaalset lähenemist. [1]

**Millal valiksin Kanbani?** Kanban sobiks pärast rakenduse avaldamist, kui põhitöö on hooldus: vigade parandamine ja vaatamisväärsuste andmete uuendamine. Siis tulevad tööd ettearvamatult ja neid ei ole mõtet kaheks nädalaks ette planeerida.

### Rollid meie projektis

Päris projektis oleks **tooteomanik** kliendi esindaja, näiteks turismiettevõttest või omavalitsusest. Lisaks oleks meeskonnas **Scrum Master** ja 2–3 **arendajat**.

Selles kooliprojektis teen planeerimise üksi, seega täidan ise kõiki rolle. Sprindi pikkus on 2 nädalat. See on meie projekti valik, mitte Scrumi nõue (vt `docs/01-development-process.md`).

## 2.2 Kasutajad

| Roll | Kirjeldus |
|---|---|
| **Külastaja** | Inimene, kes otsib vaatamisväärsusi ilma sisse logimata. Näiteks turist või kohalik elanik. |
| **Registreeritud kasutaja** | Külastaja, kes on loonud konto ja saab salvestada lemmikuid ning kirjutada arvustusi. |
| **Administraator** | Kliendi töötaja, kes lisab ja muudab vaatamisväärsuste andmeid. |

## 2.3 Kasutajalood

Kasutajalugu on kirjutatud kujul: **„[Rollina] tahan [vajadus], et [eesmärk].”** Vastuvõtukriteeriumide järgi saab kontrollida, kas lugu on valmis.

Suurus on antud **lugupunktides** (story points). Need on töömahu suhtelised hinnangud, mitte tunnid. Punktid ei ole Scrumi kohustuslik osa. Kasutame neid, et hinnata, kui palju tööd ühte sprinti mahub.

### US1 – Vaatamisväärsused kaardil
**Külastajana tahan näha Eesti vaatamisväärsusi kaardil, et leida huvitavaid kohti enda lähedalt või reisi sihtkohast.**
- Avalehel on Eesti kaart, kus vaatamisväärsused on tähistatud märkidega.
- Kaarti saab suurendada, vähendada ja liigutada.
- Märgile klõpsates näeb vaatamisväärsuse nime ja linki detailvaatele.
- Kaart töötab ka telefoni brauseris.

Prioriteet: **Must** · Suurus: **5**

### US2 – Vaatamisväärsuse detailvaade
**Külastajana tahan näha vaatamisväärsuse kirjeldust ja praktilist infot, et otsustada, kas sinna minna.**
- Detailvaates on nimi, pilt, kirjeldus, aadress, lahtiolekuajad ja piletiinfo (kui see on olemas).
- Detailvaates on väike kaart vaatamisväärsuse asukohaga.
- Detailvaatel on oma aadress (URL), mida saab teistega jagada.

Prioriteet: **Must** · Suurus: **3**

### US3 – Otsing nime järgi
**Külastajana tahan otsida vaatamisväärsust nime järgi, et leida kiiresti konkreetne koht.**
- Otsingukasti saab sisestada nime või selle osa, näiteks „loss”.
- Otsing ei sõltu suurtest ja väikestest tähtedest.
- Kui midagi ei leitud, kuvatakse selle kohta teade.

Prioriteet: **Must** · Suurus: **3**

### US4 – Filtreerimine maakonna ja tüübi järgi
**Külastajana tahan filtreerida vaatamisväärsusi maakonna ja tüübi järgi, et näha ainult mind huvitavaid kohti.**
- Saab valida maakonna, näiteks Harjumaa või Saaremaa.
- Saab valida tüübi, näiteks loss või mõis, muuseum, loodus, kirik.
- Filtreid saab kombineerida ja tulemused uuenevad nii kaardil kui ka nimekirjas.

Prioriteet: **Must** · Suurus: **5**

### US5 – Vaatamisväärsuste haldamine
**Administraatorina tahan lisada, muuta ja kustutada vaatamisväärsusi, et andmed oleksid ajakohased.**
- Haldusvaatesse pääseb ainult sisse loginud administraator.
- Vaatamisväärsusele saab lisada nime, kirjelduse, asukoha, maakonna, tüübi, pildi ja praktilise info.
- Kohustuslike väljade puudumisel kuvatakse veateade.
- Muudatus on kasutajatele kohe nähtav.

Prioriteet: **Must** · Suurus: **8**

### US6 – Kasutajakonto
**Külastajana tahan luua konto ja sisse logida, et kasutada isiklikke funktsioone.**
- Konto saab luua e-posti ja parooliga.
- Parool salvestatakse turvaliselt räsitud kujul.
- Kasutaja saab sisse ja välja logida.

Prioriteet: **Should** · Suurus: **5**

### US7 – Lemmikud
**Registreeritud kasutajana tahan salvestada vaatamisväärsusi lemmikutesse, et koostada endale nimekiri kohtadest, mida külastada.**
- Detailvaates on nupp „Lisa lemmikutesse” ja „Eemalda lemmikutest”.
- Kasutaja näeb oma lemmikute nimekirja ja saab neid vaadata kaardil.

Prioriteet: **Should** · Suurus: **3**

### US8 – Arvustused ja hinded
**Registreeritud kasutajana tahan anda vaatamisväärsusele hinde ja kirjutada arvustuse, et jagada oma kogemust teistega.**
- Hinne on 1–5 tärni ja arvustuse tekst on valikuline.
- Detailvaates on näha keskmine hinne ja arvustused.
- Administraator saab sobimatu arvustuse eemaldada.

Prioriteet: **Could** · Suurus: **5**

### US9 – Lähedal asuvad vaatamisväärsused
**Külastajana tahan näha minu asukohale lähimaid vaatamisväärsusi, et leida reisil kiiresti midagi lähedalt.**
- Rakendus küsib asukoha kasutamiseks luba.
- Kuvatakse lähimad vaatamisväärsused koos kaugusega.
- Kui luba ei anta, töötab rakendus edasi ilma selle funktsioonita.

Prioriteet: **Could** · Suurus: **3**

### US10 – Marsruudi planeerimine
**Registreeritud kasutajana tahan koostada mitme vaatamisväärsuse külastamiseks marsruudi, et planeerida päevareisi.**

Prioriteet: **Won't (seekord)** · Suurust ei hinnatud

### US11 – Mobiilirakendus
**Külastajana tahan kasutada rakendust eraldi mobiilirakendusena, et seda oleks telefonis mugavam kasutada.**

Prioriteet: **Won't (seekord)** · Suurust ei hinnatud

### US12 – Ingliskeelne liides
**Välisturistina tahan kasutada rakendust inglise keeles, et saaksin infost aru.**

Prioriteet: **Won't (seekord)** · Suurust ei hinnatud

### Tehniline töö T1 – Arenduskeskkond ja algandmed
See ei ole kasutajalugu, vaid tehniline töö, ilma milleta ei saa US1 ja US2 tööd alustada.
- Projekti kood, andmebaas ja testkeskkond on üles seatud.
- Andmebaasis on vähemalt 20 Eesti vaatamisväärsuse algandmed. Need sisestatakse käsitsi, sest haldusvaade (US5) tuleb alles 2. sprindis.

Suurus: **5**

## 2.4 Prioriteedid

Prioriteetide määramiseks kasutan **MoSCoW-meetodit** [3]:
- **Must** – minimaalne kasutatav hulk nõudeid, mille projekt kindlasti valmis teeb;
- **Should** – oluline, kuid mitte hädavajalik;
- **Could** – soovitav, kuid vähem oluline;
- **Won't (seekord)** – kokku lepitud, et seda selles ajavahemikus ei tehta.

| ID | Kasutajalugu | Prioriteet | Suurus | Sprint | Põhjendus |
|---|---|---|---|---|---|
| T1 | Arenduskeskkond ja algandmed | – | 5 | 1 | Ilma selleta ei saa teisi töid alustada. |
| US1 | Vaatamisväärsused kaardil | Must | 5 | 1 | Rakenduse põhiidee. Ilma selleta pole toodet. |
| US2 | Detailvaade | Must | 3 | 1 | Kaardist üksi ei piisa, kasutaja vajab infot koha kohta. |
| US3 | Otsing nime järgi | Must | 3 | 2 | Kui vaatamisväärsusi on palju, on konkreetset kohta kaardilt raske leida. |
| US4 | Filtreerimine | Must | 5 | 2 | Aitab kasutajal leida just teda huvitavaid kohti. |
| US5 | Andmete haldamine | Must | 8 | 2 | Ilma selleta ei saa andmeid ajakohasena hoida. Esimeses sprindis sisestatakse andmed käsitsi. |
| US6 | Kasutajakonto | Should | 5 | 3 | Vajalik lemmikute ja arvustuste jaoks, kuid põhifunktsioonid töötavad ka ilma kontota. |
| US7 | Lemmikud | Should | 3 | 3 | Suurendab kasutaja huvi rakendusse tagasi tulla, kuid ei ole hädavajalik. |
| US8 | Arvustused ja hinded | Could | 5 | 4 | Kasulik, kuid vajab sisu modereerimist ja on alguses väikese kasutajate arvu juures vähem väärtuslik. |
| US9 | Lähedal asuvad vaatamisväärsused | Could | 3 | 4 | Mugav reisil, kuid sama infot saab ka kaardilt. |
| US10 | Marsruudi planeerimine | Won't | – | – | Suur töö, mis vajab välist marsruuditeenust. Kaalume hiljem kasutajate tagasiside põhjal. |
| US11 | Mobiilirakendus | Won't | – | – | Veebirakendus on kavandatud töötama ka telefonis. Eraldi rakendus oleks esimeses versioonis liiga suur töö. |
| US12 | Ingliskeelne liides | Won't | – | – | Kõik vaatamisväärsuste tekstid tuleks tõlkida. Esimene versioon on eesti keeles. |

**Töömahu jaotus.** Must-kasutajalood on kokku 24 punkti, Should-lood 8 punkti ja Could-lood 8 punkti, seega kokku 40 punkti (ilma Won't-lugude ja tehnilise tööta). Must-lugude osa on 60%, Should-lugude osa 20% ja Could-lugude osa 20%. See vastab MoSCoW soovitusele, et Must-tööd ei võtaks tavaliselt rohkem kui 60% töömahust. [3] Nii jääb varu: kui aega jääb puudu, saab Could-lood välja jätta, ilma et põhifunktsioonid kannataksid.

Tehnilisel tööl T1 ei ole MoSCoW prioriteeti, sest see ei ole kasutajalugu. Sisuliselt on see siiski hädavajalik. Kui arvestada ka T1 (5 punkti) Must-töö hulka, on Must-töö 29 punkti 45-st ehk umbes 64%. See on veidi üle soovituse, seega on plaanis vähem varu. Could-lood (8 punkti) ei muuda Must-töö osakaalu, kuid annavad paindlikkust: kui tegelik töö osutub arvatust suuremaks, saab need välja jätta ja vabanenud aja kasutada Must-tööde lõpetamiseks.

Prioriteedid ei ole lõplikud. Tooteomanik vaatab need üle iga sprindi lõpus ja uue info põhjal võib järjekord muutuda.

## 2.5 Seos nelja iteratsiooniga

Eelmises dokumendis kirjeldatud neli iteratsiooni on Scrumis neli sprinti.

| Sprint | Eesmärk (`docs/01-development-process.md`) | Tööd | Punktid |
|---|---|---|---|
| 1 | Vaatamisväärsused kaardil ja nende detailvaade | T1, US1, US2 | 13 |
| 2 | Otsing ja filtrid, administraator saab andmeid lisada ja muuta | US3, US4, US5 | 16 |
| 3 | Kasutajakonto ja lemmikud | US6, US7 | 8 |
| 4 | Arvustused, parandused tagasiside põhjal, ettevalmistus väljalaskeks | US8, US9, eelmiste sprintide tagasisidest tekkinud parandused | 8 + parandused |

Sprintide maht on erinev, sest punktid on esialgsed hinnangud. Meeskonna tegelik töökiirus selgub alles pärast esimest sprinti. Kui 2. sprint osutub liiga suureks, liigub osa tööst järgmisesse sprinti. Selle otsuse teeb tooteomanik prioriteetide järgi.

Võrreldes eelmise dokumendiga lisandus 4. sprinti US9 (lähedal asuvad vaatamisväärsused). See on Could-lugu ja tehakse ainult siis, kui aega jääb.

> **Kooskõlastamist vajav muudatus:** failis `docs/01-development-process.md` ei ole 4. iteratsiooni kirjelduses US9 veel mainitud. See tuleb hiljem lisada, kui mõlemad dokumendid koos üle vaatame.

## 2.6 Esimese sprindi plaan

**Sprindi eesmärk:** kasutaja näeb Eesti vaatamisväärsusi kaardil ja saab avada nende kirjelduse.

**Kestus:** 2 nädalat (10 tööpäeva)

**Sprinti valitud tööd:** T1, US1, US2 (kokku 13 punkti)

13 lugupunkti on esialgne hinnang. Kui palju tööd sprindis tegelikult valmib, sõltub meeskonna töökiirusest, mis selgub alles esimese sprindi järel. Samuti sõltub see tehniliste valikute keerukusest, näiteks kaarditeegi ja andmebaasi seadistamisest. Kui sprindi ajal selgub, et kõike ei jõua, täpsustatakse töö sisu koos tooteomanikuga, kuid sprindi eesmärki ei muudeta. [1]

### Ülesanded

| Töö | Ülesanne |
|---|---|
| T1 | Projekti koodihoidla ja töövoo seadistamine |
| T1 | Andmebaasi tabeli loomine vaatamisväärsuste jaoks (nimi, kirjeldus, asukoht, maakond, tüüp, pilt, praktiline info) |
| T1 | 20 vaatamisväärsuse algandmete kogumine ja sisestamine |
| T1 | Testkeskkonna seadistamine, kuhu saab rakenduse üles panna |
| US1 | Serveri liides (API), mis tagastab kõigi vaatamisväärsuste nimed ja asukohad |
| US1 | Kaardivaade (OpenStreetMap kaardialus) koos vaatamisväärsuste märkidega |
| US1 | Märgile klõpsates avaneva infokasti tegemine |
| US1 | Kaardivaate kontroll telefoni ekraanil |
| US2 | Serveri liides (API), mis tagastab ühe vaatamisväärsuse kõik andmed |
| US2 | Detailvaate leht koos väikese asukohakaardiga |
| US1, US2 | Testid ja vastuvõtukriteeriumide kontroll |

Täpsemad tehnoloogiavalikud kirjeldan arhitektuuri dokumendis (`docs/04-architecture.md`).

### Sprindi ajakava

| Päev | Tegevus |
|---|---|
| 1 | **Sprindi planeerimine:** miks see sprint on väärtuslik, mida jõuame teha ja kuidas töö tehakse [1] |
| 1–10 | **Igapäevane koosolek** (15 min): mida tegin, mida teen järgmiseks, mis takistab |
| 1–3 | T1: arenduskeskkond, andmebaas ja algandmed |
| 3–7 | US1: kaardivaade |
| 6–9 | US2: detailvaade |
| 9 | Testimine, vigade parandamine, rakenduse paigaldamine testkeskkonda |
| 10 | **Sprindi ülevaatus:** töötava rakenduse näitamine kliendile ja tagasiside kogumine |
| 10 | **Sprindi retrospektiiv:** mis läks hästi, mida järgmises sprindis paremini teha |

### Oodatav tulemus

- Testkeskkonnas töötab rakenduse esimene versioon **0.1.0** (versioonimine on kirjeldatud failis `docs/05-versioning.md`).
- Kasutaja näeb kaardil vähemalt 20 vaatamisväärsust ja saab avada nende detailvaate.
- Klient on esimest versiooni näinud ja tema tagasiside on lisatud tööde nimekirja.

### Valmis olemise määratlus (Definition of Done)

**Päris arendusmeeskonnas**, kes rakendust ehitab, loetakse töö valmis, kui:
- kõik vastuvõtukriteeriumid on täidetud;
- kood on salvestatud Git-i ja teine arendaja on selle üle vaadanud (koodiülevaatus ehk code review), sest nii leitakse vigu, mida autor ise ei märka;
- funktsioon on testitud nii arvuti kui ka telefoni brauseris;
- funktsioon töötab testkeskkonnas.

**Selles kooliprojektis** koostan üksi arendusplaani ega ehita valmis veebirakendust. Ma ei ole koodi kirjutanud, rakendust testkeskkonnas käivitanud ega koodiülevaatust läbinud. Ülaltoodud määratlus on osa plaanist ja kirjeldab, mida meeskond kasutaks. Oma töös saan kontrollnimekirja abil kontrollida plaani dokumente:
- kas igal sprinti planeeritud kasutajalool on roll, vajadus, eesmärk ja kontrollitavad vastuvõtukriteeriumid;
- kas dokumendid on omavahel kooskõlas;
- kas õpetaja nõuded on täidetud.

Selline enesekontroll ei asenda teise inimese ülevaatust, sest oma vigu on raskem märgata.

## 2.7 Tööde planeerimine ja jälgimine

Hakkan tööde nimekirja haldama **GitHub Projectsis**, kui tahvel on loodud. Link tahvlile lisatakse siia ja README-sse.

**Tahvli veerud:**

| Veerg | Tähendus |
|---|---|
| Backlog | Kõik tööd, mis pole veel sprinti valitud |
| Sprint Backlog | Käimasoleva sprindi tööd, mida pole veel alustatud |
| Töös | Tööd, mida praegu tehakse |
| Ülevaatusel | Valmis tööd, mida kontrollitakse vastuvõtukriteeriumide ja valmis olemise määratluse järgi |
| Valmis | Tööd, mis vastavad valmis olemise määratlusele |

Iga kasutajalugu lisatakse GitHubi eraldi issue'na. Sellel on väljad **prioriteet** (Must, Should, Could, Won't), **suurus** (punktid) ja **sprint**.

**Kuidas planeerimine ja jälgimine käib:**

1. **Tööde nimekirja täpsustamine.** Pidev tegevus, kus suuri lugusid jagatakse väiksemateks ning lisatakse kirjeldusi, järjekorda ja suurusi. [1] Uued nõuded lisatakse kasutajalugudena veergu Backlog.
2. **Sprindi planeerimine.** Sprindi alguses valitakse kõige kõrgema prioriteediga tööd sprindi eesmärgi järgi ja liigutatakse need veergu Sprint Backlog.
3. **Igapäevane jälgimine.** Tahvlilt on näha, mis on töös ja mis on valmis. Igapäevasel koosolekul räägitakse takistustest.
4. **Sprindi ajal.** Sprindi eesmärki ohustavaid muudatusi ei tehta, kuid töö sisu võib tooteomanikuga täpsustada. [1]
5. **Sprindi lõpus.** Ülevaatusel näidatakse valminud tööd ja retrospektiivil arutatakse töökorralduse parandamist. Lõpetamata tööd lähevad tagasi veergu Backlog ja tooteomanik määrab nende prioriteedi uuesti.

## Allikad

1. Schwaber, K., Sutherland, J. (2020). *The Scrum Guide.* <https://scrumguides.org/scrum-guide.html>
2. Coleman, J., Vacanti, D. jt (2025). *The Kanban Guide* (versioon mai 2025). <https://kanbanguides.org/english/>
3. Agile Business Consortium. *What is MoSCoW Prioritization?* <https://www.agilebusiness.org/dsdm-project-framework/moscow-prioritisation.html>
