# Eesti vaatamisväärsuste avastamise veebirakendus – arendusplaan

> **Seis:** mustand. Töö on pooleli. Allolevas tabelis on näha, mis on valmis ja mis veel puudub.

## Projekti kirjeldus

See repositoorium sisaldab kooliprojekti, kus kavandan veebirakenduse, mille abil saab avastada Eesti vaatamisväärsusi. Kasutaja saab rakenduses:

- vaadata vaatamisväärsusi kaardil;
- otsida ja filtreerida neid näiteks maakonna või tüübi järgi;
- lugeda vaatamisväärsuse kirjeldust ja praktilist infot.

**Töö eesmärk** on koostada rakenduse arendusplaan. Valmis rakendust ma selle töö käigus ei programmeeri. Plaanis kirjeldan arendusprotsessi, metoodikat, töövahendeid, arhitektuuri ja versioonimist ning põhjendan tehtud valikuid.

## Materjalide asukoht

| Ülesande osa | Fail | Seis |
|---|---|---|
| 1. Arendusprotsess ja mudelite võrdlus | `docs/01-development-process.md` | valmis |
| 2. Arendusmetoodika, kasutajalood ja backlog | `docs/02-methodology-backlog.md` | valmis |
| 2. Tööde haldamise keskkond (GitHub Projects) | link lisatakse siia | tegemata |
| 3. CASE-vahendite võrdlus ja kasutamise näited | `docs/03-case-tools.md` | tegemata |
| 4. Tarkvaraarhitektuur | `docs/04-architecture.md` | tegemata |
| 4. Arhitektuuriskeem (muudetav lähtefail) | `diagrams/` | tegemata |
| 5. Versiooniplaan (SemVer) | `docs/05-versioning.md` | tegemata |

Failide nimed võivad töö käigus veidi muutuda. Tabelit uuendan iga etapi järel.

## Kaustade struktuur

```
README.md      – projekti kirjeldus ja juhised materjalide leidmiseks
CLAUDE.md      – püsijuhised AI-assistendile
docs/          – kavandamise dokumendid
diagrams/      – skeemide muudetavad lähtefailid ja nende pildid
```

## Kavandatud töövahendid

Need on esialgsed valikud. Põhjendused lisan vastavatesse dokumentidesse.

- **Git ja GitHub** – muudatuste salvestamiseks ja dokumentide hoidmiseks
- **GitHub Projects** – kasutajalugude ja tööde planeerimiseks
- **diagrams.net** – arhitektuuriskeemi koostamiseks
- **PlantUML** – UML-skeemide koostamiseks tekstina

## AI kasutamine

Selgituste ja skeemide koostamisel kasutasin abiks AI-assistenti Claude Code. Tehtud valikud ja lõpliku sisu vaatan üle ise.
