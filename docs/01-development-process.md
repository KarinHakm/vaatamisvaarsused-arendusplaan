# 1. Tarkvara arendusprotsess

Selles dokumendis kirjeldan, kuidas Eesti vaatamisväärsuste avastamise veebirakendus jõuaks ideest kasutajateni ja kuidas seda hiljem hooldataks. Lisaks võrdlen kahte arendusprotsessi mudelit, põhjendan oma valikut ja selgitan, mida teha, kui klient muudab arenduse ajal nõudeid.

## 1.1 Arendusprotsessi etapid

| Etapp | Eesmärk | Mida see meie projektis tähendab |
|---|---|---|
| **1. Idee ja eesmärk** | Selgitada välja, millist probleemi rakendus lahendab ja kellele see on mõeldud. | Turistidel ja kohalikel on raske leida ühest kohast infot Eesti vaatamisväärsuste kohta. Rakendus koondab info kaardile. Sihtrühmad on turistid, kohalikud ja vaatamisväärsuste andmeid haldav administraator. |
| **2. Nõuete kogumine ja analüüs** | Kirja panna, mida rakendus peab tegema (funktsionaalsed nõuded) ja millised omadused peavad sellel olema (mittefunktsionaalsed nõuded). | Nõuded kirjutan kasutajalugudena, näiteks „Turistina tahan näha vaatamisväärsusi kaardil, et leida midagi enda lähedalt.” Mittefunktsionaalsed nõuded on näiteks see, et rakendus töötab ka telefoni brauseris ja leht avaneb kiiresti. |
| **3. Disain ja arhitektuur** | Otsustada, kuidas süsteem on üles ehitatud: komponendid, andmebaas, kasutajaliides ja tehnoloogiad. | Koostan arhitektuuriskeemi ja UML-skeemid (vt `docs/04-architecture.md`). |
| **4. Arendus (programmeerimine)** | Kirjutada programmikood disaini järgi. | Arendus toimub väikeste osadena. Igas iteratsioonis valmib mõni töötav funktsioon. |
| **5. Testimine** | Kontrollida, kas rakendus töötab õigesti ja vastab nõuetele. | Iga funktsiooni testitakse samas iteratsioonis, kus see valmib. Kasutajalool on vastuvõtukriteeriumid, mille järgi saab kontrollida, kas töö on valmis. |
| **6. Kasutuselevõtt (juurutamine)** | Viia rakendus serverisse, kus kasutajad saavad seda kasutada. | Rakendus avaldatakse veebis. Iga väljalase saab versiooninumbri (vt `docs/05-versioning.md`). |
| **7. Hooldus ja edasiarendus** | Parandada vigu, uuendada andmeid ja lisada uusi funktsioone. | Kasutajate tagasiside põhjal tekivad uued kasutajalood. Vaatamisväärsuste andmeid tuleb pidevalt uuendada. |

Etappide järjekord on loogiline, kuid **etappide läbimise viis sõltub arendusmudelist**. Koskmudelis läbitakse iga etapp kogu projekti jaoks üks kord. Iteratiivses arenduses korduvad etapid 2–7 iga väikese osa jaoks.

## 1.2 Arendusmudelite võrdlus

### Koskmudel (waterfall)

Koskmudelis läbitakse etapid kindlas järjekorras ja järgmise etapiga alustatakse alles siis, kui eelmine on valmis. Kõik nõuded pannakse kirja projekti alguses ja kasutaja näeb valmis rakendust alles projekti lõpus. Klassikalises koskmudelis on testimine eraldi etapp pärast arendust, kus kogu süsteemi kontrollitakse tervikuna. See ei tähenda, et enne seda midagi ei kontrollita: arendajad saavad oma koodi ka arenduse ajal kontrollida ning mõnes koskmudeli variandis kavandatakse testid juba nõuete ja disaini etapis. Põhiline erinevus on see, et terviklik süsteem jõuab testimisse ja kasutajani hilja.

Mudelit seostatakse sageli W. W. Royce'i 1970. aasta artikliga. Huvitav on see, et Royce ise kirjutas lihtsa järjestikuse mudeli kohta: *„I believe in this concept, but the implementation described above is risky and invites failure.”* [1, lk 329] Tema selgituse järgi on arenduse lõpus toimuv testimisetapp esimene hetk, kus süsteemi tegelik käitumine selgub. Kui siis ilmneb suur probleem, võib olla vaja disaini põhjalikult muuta. Samas artiklis pakkus Royce välja ka täiendusi, mis seda riski vähendavad. [1]

### Iteratiivne ja inkrementaalne arendus

Iteratiivses arenduses tehakse tööd lühikeste tsüklitena (iteratsioonidena). Igas tsüklis kavandatakse, arendatakse ja testitakse väike osa rakendusest. Inkrementaalne tähendab, et rakendus kasvab samm-sammult: iga iteratsiooni lõpus on olemas töötav ja eelmisest veidi suurem versioon. Selle põhimõtte järgi töötavad ka agiilsed metoodikad, näiteks Scrum. [2] [3]

### Võrdlustabel

| Tunnus | Koskmudel | Iteratiivne arendus |
|---|---|---|
| Nõuded | Lepitakse kokku projekti alguses ja need peaksid püsima samana | Täpsustuvad töö käigus |
| Töö järjekord | Etapid järjest, igaüks üks kord | Etapid korduvad igas iteratsioonis |
| Esimene töötav versioon | Projekti lõpus | Juba esimese iteratsiooni järel |
| Kliendi tagasiside | Peamiselt alguses ja lõpus | Iga iteratsiooni lõpus |
| Testimine | Kogu süsteemi testimine on eraldi etapp pärast arendust | Iga valminud osa testitakse samas iteratsioonis |
| Nõuete muutmine | Kallis, sest tuleb minna tagasi varasematesse etappidesse | Odavam, sest muudatus lisatakse järgmistesse iteratsioonidesse |
| Planeerimine | Põhjalik plaan alguses, tähtajad ja eelarve on paremini ette teada | Lähiaega planeeritakse täpselt, kaugemat tulevikku umbkaudselt |
| Dokumentatsioon | Mahukas, iga etapi tulemus dokumenteeritakse | Väiksem, tähtsaim on töötav tarkvara |
| Sobib, kui | Nõuded on selged ja stabiilsed (nt seadusest tulenevad süsteemid, riistvaraga seotud tarkvara) | Nõuded on ebaselged või muutuvad ning kasutaja tagasiside on oluline |

**Koskmudeli eelised:** see on lihtne mõista ja juhtida, etapid ja tulemused on selgelt piiritletud ning dokumentatsioon on põhjalik.
**Koskmudeli puudused:** vead ja valesti mõistetud nõuded tulevad välja hilja, muudatused on kallid ja klient näeb tulemust alles lõpus.

**Iteratiivse arenduse eelised:** töötav versioon on varakult olemas, tagasisidet saab tihti, riskid vähenevad ja muudatustele on lihtne reageerida.
**Iteratiivse arenduse puudused:** projekti lõplikku kestust ja mahtu on raskem ette öelda, klient peab olema pidevalt kaasatud ja arhitektuur võib kannatada, kui seda ei planeerita.

## 1.3 Meie projekti jaoks valitud mudel

Valin **iteratiivse ja inkrementaalse arendusmudeli** ning selle praktiliseks korraldamiseks metoodika **Scrum** (põhjendus on failis `docs/02-methodology-backlog.md`).

**Põhjendused:**

1. **Nõuded ei ole alguses täpselt teada.** Pole kindel, milliseid funktsioone turistid kõige rohkem kasutavad, kas kaarti, otsingut, lemmikuid või marsruute. Iteratiivne arendus võimaldab kõigepealt teha lihtsa versiooni ja koguda tagasisidet.
2. **Põhifunktsioonid valmivad varakult.** Esimeses iteratsioonis saab valmis teha kõige olulisema osa: vaatamisväärsused kaardil ja nende detailvaade. Hiljem tulevad otsing, kasutajakonto ja lemmikud.
3. **Projekt on väike.** Meeskond on väike ja klient on kättesaadav, nii et tagasisidet saab tihti küsida.
4. **Muudatused on tõenäolised.** Klient võib soovida näiteks mobiilirakendust või uusi andmeid. Iteratiivses mudelis lisatakse need järgmistesse iteratsioonidesse ilma kogu plaani ümber tegemata.
5. **Riskid vähenevad.** Kui mõni tehniline lahendus, näiteks kaarditeenus, ei tööta ootuspäraselt, selgub see esimestes iteratsioonides, mitte projekti lõpus.

**Miks mitte koskmudel?** Koskmudel sobiks, kui kõik nõuded oleksid algusest peale selged ja muutumatud. Meie projektis see nii ei ole. Kui teeksime kõik nõuded ette valmis ja klient näeks rakendust alles lõpus, oleks suur oht, et rakendus ei vasta kasutajate tegelikele vajadustele.

### Esialgne iteratsioonide plaan

Scrumis nimetatakse iteratsiooni sprindiks. Meie projektis kestab üks sprint 2 nädalat. See on projekti enda valik, mitte Scrumi kohustuslik kestus: Scrumi juhendi järgi on sprint kindla pikkusega ja kestab kuni ühe kuu. [3] Kaks nädalat on piisavalt lühike aeg, et saada tihti tagasisidet, ja piisavalt pikk, et valmiks mõni töötav funktsioon. Plaan on esialgne ja täpsustub backlog'i koostamisel.

| Iteratsioon | Põhieesmärk |
|---|---|
| 1 | Vaatamisväärsused kaardil ja nende detailvaade (esimene töötav versioon) |
| 2 | Otsing ja filtrid, administraatori võimalus andmeid lisada, muuta ja kustutada |
| 3 | Kasutajakonto ja lemmikud |
| 4 | Arvustused, lähedal asuvad vaatamisväärsused (kui aega jääb), parandused tagasiside põhjal, ettevalmistus avalikuks väljalaskeks |

## 1.4 Kui klient muudab arenduse keskel nõudeid

Iteratiivses arenduses on nõuete muutumine tavaline osa tööst, mitte erandlik probleem. Agiilse tarkvaraarenduse manifest ütleb: *„reageerimist muutunud oludele rohkem, kui algse plaani järgimist”*. [2]

Uue või muutunud nõude korral teeksin nii:

1. **Kuulan kliendi ära ja panen nõude kirja** uue kasutajaloona backlog'i (GitHub Projectsis).
2. **Selgitan välja põhjuse ja väärtuse.** Miks seda vaja on ja kui oluline see võrreldes teiste töödega on?
3. **Hindan mõju.** Kui palju tööd see nõuab? Kas see mõjutab arhitektuuri, andmebaasi või juba tehtud funktsioone? Kas tähtaeg või muud tööd nihkuvad?
4. **Määran koos kliendiga prioriteedi.** Klient (Scrumis tooteomanik) otsustab, kas uus nõue on olulisem kui mõni olemasolev töö. Kui aeg on piiratud, tuleb midagi muud edasi lükata.
5. **Käimasolevat iteratsiooni üldjuhul ei muudeta.** Uus nõue võetakse tööle järgmises iteratsioonis. Erand on kriitiline viga või muudatus, ilma milleta iteratsiooni eesmärgil pole mõtet. Siis arutatakse plaan koos ümber.
6. **Uuendan dokumente.** Vajadusel muudan kasutajalugusid, arhitektuuriskeemi ja versiooniplaani, et need oleksid omavahel kooskõlas. Muudatused salvestan Git-i.
7. **Näitan tulemust iteratsiooni lõpus** ja küsin kliendilt tagasisidet.

**Näide.** Arenduse keskel soovib klient, et lisaks veebirakendusele tehtaks ka mobiilirakendus. Kirjutan selle kohta uued kasutajalood ja hindan mõju arhitektuurile. Kui serveri liides (API) on veebiliidesest eraldi, saab mobiilirakendus põhimõtteliselt kasutada sama serverit ja andmebaasi. See eeldab siiski, et olemasolev API sobib mobiilikliendile. Lisatööd võib vaja minna näiteks siis, kui mobiilirakendus vajab teistsugust sisselogimist, väiksemaid andmemahtusid aeglase ühenduse jaoks, tõuketeavitusi või võrguühenduseta kasutamist. Klient otsustab, kas mobiilirakendus tuleb enne mõnda teist funktsiooni või pärast esimest väljalaset. Käimasoleva iteratsiooni töö lõpetatakse plaani järgi.

**Koskmudelis oleks sama olukord keerulisem.** Nõuded on juba lukus, nii et muudatus tuleb vormistada ametliku muudatustaotlusena. Selle järel tuleb sageli minna tagasi analüüsi- ja disainietappi, mis tähendab lisakulu ja tähtaja nihkumist.

## Allikad

1. Royce, W. W. (1970). *Managing the Development of Large Software Systems.* Proceedings, IEEE WESCON, August 1970, lk 1–9. Koopia: <https://faculty.washington.edu/hazeline/misc/reserve/royce_waterfall.pdf> (koopia lehekülgedel on numbrid 328–338 ja tsitaadi leheküljenumber on antud koopia numeratsiooni järgi)
2. Beck, K. jt (2001). *Agiilse tarkvaraarenduse manifest* (eestikeelne tõlge). <https://agilemanifesto.org/iso/et/manifesto.html>
3. Schwaber, K., Sutherland, J. (2020). *The Scrum Guide.* <https://scrumguides.org/scrum-guide.html>
