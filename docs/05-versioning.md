# 5. Versioonihaldus ja versiooniplaan

See dokument kirjeldab, kuidas Eesti vaatamisväärsuste veebirakenduse versioone nummerdataks ja välja antaks. **Kõik siin nimetatud versioonid on kavandatavad.** Rakendust ei ole ehitatud, seega pole ühtegi versiooni välja antud ega Git tag'i ega GitHub Release'i loodud.

## 5.1 Semantiline versioonimine (SemVer)

Kasutame semantilise versioonimise reegleid (Semantic Versioning 2.0.0). Versiooninumber on kujul **MAJOR.MINOR.PATCH**, näiteks `1.4.2`. [1]

| Osa | Millal suureneb | Lihtne seletus |
|---|---|---|
| **MAJOR** | Kui API-s tehakse muudatus, mis ei ole tagasiühilduv [1] | Vanad kliendid (nt mobiilirakenduse vana versioon) ei pruugi enam töötada |
| **MINOR** | Kui lisatakse uus funktsioon tagasiühilduval viisil [1] | Lisandub midagi uut, aga kõik vana töötab edasi |
| **PATCH** | Kui parandatakse viga tagasiühilduval viisil [1] | Midagi uut ei lisandu, ainult viga parandatakse |

**Lisareeglid** [1]:
- Kui MINOR suureneb, muutub PATCH nulliks: `1.4.2` → `1.5.0`.
- Kui MAJOR suureneb, muutuvad MINOR ja PATCH nulliks: `1.5.0` → `2.0.0`.
- Versioonid kujul `0.y.z` on algse arenduse jaoks. Selles faasis võib kõik muutuda.
- Versioon `1.0.0` määrab avaliku API.
- Väljaantud versiooni sisu ei tohi enam muuta. Parandus antakse välja uue versioonina.
- Eelversiooni tähistab sidekriipsu järel olev osa, näiteks `1.0.0-rc.1` (release candidate ehk väljalaskekandidaat). Eelversioon on järjekorras madalam kui sellele vastav tavaversioon: `1.0.0-rc.1` < `1.0.0`.

### Näide: kui praegune versioon on 2.4.1

| Muudatus | Järgmine versioon |
|---|---|
| Veaparandus | `2.4.2` |
| Uus tagasiühilduv funktsioon | `2.5.0` |
| Avalikku API-d lõhkuv muudatus | `3.0.0` |

## 5.2 Mis on meie rakenduse „avalik API”?

SemVer räägib API muudatustest. Meie rakenduses on avalik API **REST API** (nt `GET /api/attractions?county=Saaremaa`, vt `docs/04-architecture.md`), mida kasutab veebiliides ja võimalik tulevane mobiilirakendus.

Seepärast hindame iga muudatuse puhul, kas **olemasolev API klient jääb tööle**:
- kui jääb ja lisandub midagi uut, on tegemist MINOR-muudatusega;
- kui jääb ja ainult viga parandati, on tegemist PATCH-muudatusega;
- kui ei jää, on tegemist MAJOR-muudatusega.

## 5.3 Kavandatav versiooniplaan

Versiooniplaan järgib sprintide plaani failis `docs/02-methodology-backlog.md` (punkt 2.5) ja iteratsioonide plaani failis `docs/01-development-process.md` (punkt 1.3).

| Sprint | Kavandatav versioon | Mis lisandub | Miks just see number |
|---|---|---|---|
| 1 | **0.1.0** | T1, US1 (kaart), US2 (detailvaade) | Esimene töötav versioon. Algne arendus, seega `0.y.z` |
| 2 | **0.2.0** | US3 (otsing), US4 (filtrid), US5 (andmete haldamine) | Uued funktsioonid, seega suureneb MINOR |
| 3 | **0.3.0** | US6 (kasutajakonto), US7 (lemmikud) | Uued funktsioonid, seega suureneb MINOR |
| 4 | **1.0.0-rc.1**, seejärel **1.0.0** | US8 (arvustused), US9 (lähedal asuvad vaatamisväärsused, kui aega jääb), parandused tagasiside põhjal | Avalik väljalase. Versioon `1.0.0` määrab avaliku API |

Sprintide vahel võib tulla ka PATCH-versioone. Näiteks kui pärast 2. sprindi ülevaatust leitakse filtris viga, antakse parandus välja versioonina `0.2.1`.

**Kui plaan muutub:** kui näiteks tähtaeg lüheneb, võib versioon `1.0.0` sisaldada ainult Must-prioriteediga kasutajalugusid (T1, US1–US5, vt `docs/02-methodology-backlog.md`, punkt 2.4). Ülejäänud funktsioonid lisanduksid hiljem MINOR-versioonidena.

## 5.4 Näited pärast versiooni 1.0.0

| Muudatus | Liik | Versioon pärast 1.0.0 |
|---|---|---|
| Otsing ei leia vaatamisväärsust, kui nimi on kirjutatud suure algustähega (US3 vastuvõtukriteeriumi järgi ei tohi otsing tähtede suurusest sõltuda) | PATCH | `1.0.1` |
| Kaardimärk kuvatakse vales kohas | PATCH | `1.0.1` |
| Lisatakse US9 „Lähedal asuvad vaatamisväärsused”, kui see 4. sprindis ei valminud | MINOR | `1.1.0` |
| Lisatakse ingliskeelne liides (US12) | MINOR | `1.1.0` |
| API vastuses nimetatakse väli `county` ümber väljaks `region`, mistõttu vanad kliendid ei leia enam maakonda | MAJOR | `2.0.0` |
| API-st eemaldatakse aadress, mida mobiilirakenduse vanad versioonid kasutavad | MAJOR | `2.0.0` |

Kui MAJOR-muudatust ei saa vältida, on soovitatav API-d versioonida, näiteks `/api/v1/...` ja `/api/v2/...` (vt `docs/04-architecture.md`, punkt 4.10). Siis saavad vanad kliendid mõnda aega veel vana API-t kasutada.

## 5.5 Git tag'id

Git tag on nimi, mis märgib ajaloos kindla commit'i, tavaliselt väljalaske. [2] Git tag'e on kahte liiki [2]:
- **lihtne tag** (lightweight) on ainult viide commit'ile;
- **annoteeritud tag** (annotated) sisaldab ka märkija nime, e-posti, kuupäeva ja sõnumit.

Kasutame **annoteeritud tag'e**, sest need sisaldavad rohkem infot. Git-i dokumentatsioon soovitab üldjuhul just neid. [2]

Tag'i nimi algab tähega `v`, näiteks `v0.1.0`. SemVer-i järgi ei ole `v0.1.0` ise semantiline versioon, vaid tag'i nimi. Semantiline versioon on `0.1.0`. `v` lisamine on levinud viis näidata, et tegemist on versiooninumbriga. [1]

Kavandatav näide 1. sprindi lõpust:

    git tag -a v0.1.0 -m "Versioon 0.1.0: vaatamisväärsused kaardil ja detailvaade"
    git push origin v0.1.0

Tag tuleb eraldi GitHubi saata, sest tavaline `git push` tag'e vaikimisi ei saada. [2]

## 5.6 GitHub Release'id

GitHub Release on Git tag'il põhinev väljalase, millele saab lisada väljalaske kirjelduse (release notes) ja failid. [3]

Kavandatav töökäik:
1. Alusta GitHubis uue väljalaske loomist ja vali selle tag, näiteks `v0.1.0`. [4]
2. Kirjuta väljalaske kirjeldus: mis lisandus, mis parandati ja millised kasutajalood valmisid. Kirjelduse saab ka automaatselt koostada nupuga **Generate release notes**. [4]
3. Väljalaskekandidaat (`v1.0.0-rc.1`) märgitakse valikuga **This is a pre-release**. [4]

## 5.7 Väljalaske käik sprindi lõpus

1. Kontrolli, et sprindi tööd vastavad valmis olemise määratlusele (vt `docs/02-methodology-backlog.md`, punkt 2.6).
2. Otsusta versiooninumber punktide 5.1 ja 5.2 reeglite järgi.
3. Koosta muudatuste loetelu.
4. Loo annoteeritud Git tag ja saada see GitHubi (punkt 5.5).
5. Loo tag'i põhjal GitHub Release (punkt 5.6).
6. Paigalda versioon testkeskkonda ja pärast kontrolli avalikku keskkonda.

Väljaantud versiooni enam ei muudeta. Kui selles leitakse viga, antakse parandus välja uue PATCH-versioonina. [1]

## 5.8 Git-i harud

- **`main`** on haru, kus on alati töötav kood. Väljalaske tag'id luuakse `main` harus olevale commit'ile.
- Iga kasutajaloo jaoks tehakse **eraldi haru**, näiteks `feature/us4-filter`. Nii ei sega pooleli olev töö teisi ja `main` jääb töökorda.
- Kui töö on valmis ja üle vaadatud, liidetakse haru `main` harusse.

See kooliprojekt sisaldab ainult arendusplaani dokumente, mitte rakenduse koodi. Seetõttu teen siin kõik muudatused otse `main` harusse ja selles repositooriumis tag'e ei kasuta.

## Allikad

1. Preston-Werner, T. *Semantic Versioning 2.0.0.* <https://semver.org/>
2. Chacon, S., Straub, B. *Pro Git*, ptk 2.6 „Git Basics – Tagging”. <https://git-scm.com/book/en/v2/Git-Basics-Tagging>
3. GitHub Docs. *About releases.* <https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases>
4. GitHub Docs. *Managing releases in a repository.* <https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository>
