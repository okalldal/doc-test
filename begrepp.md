---
layout: default
title: Begrepp
nav_order: 2
---

# Begrepp och begreppsmodell
{: .no_toc }

Denna sida definierar de kärnbegrepp som används genomgående i arkitekturdokumentationen. Begreppen är hämtade från domänanalysen och harmoniserade mot [DIGG:s begreppsram](https://www.digg.se) och EU:s [European Interoperability Framework (EIF)](https://ec.europa.eu/isa2/eif_en).

<details open markdown="block">
  <summary>Innehåll</summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---

## Begreppsmodell (översikt)

```
┌─────────────────────────────────────────────────────┐
│                    Plattform (DSP)                  │
│                                                     │
│   ┌──────────┐   realiserar   ┌──────────────────┐  │
│   │ Förmåga  │ ──────────────▶│    Tjänst/API    │  │
│   └──────────┘                └──────────────────┘  │
│        │ beskrivs av                  │ exponerar   │
│        ▼                             ▼             │
│   ┌──────────┐               ┌──────────────────┐  │
│   │Information│               │  Informations-   │  │
│   │  sobject  │               │    modell        │  │
│   └──────────┘               └──────────────────┘  │
└─────────────────────────────────────────────────────┘
```

---

## Kärnbegrepp

### Förmåga

> En förmåga är vad plattformen *kan göra* — oberoende av hur det är implementerat.

En förmåga beskrivs i termer av **syfte**, **intressenter**, **informationsobjekt** och **kvalitetskrav**. Förmågor är stabila över tid; teknisk realisering kan förändras utan att förmågan ändras.

Se [Förmågor](formågor/) för fullständig förteckning.

**Synonym:** kapabilitet
**Engelsk term:** capability

---

### Tjänst

> En tjänst är en teknisk implementation av (delar av) en förmåga.

En tjänst har ett definierat gränssnitt (API), versionshantering och en angiven SLA. En förmåga kan realiseras av en eller flera tjänster; en tjänst kan bidra till flera förmågor.

**Exempel:** REST-API för ärendestatus, GraphQL-endpoint för informationssökning.

---

### Informationsobjekt

> Ett informationsobjekt är en namngiven datamängd med definierad semantik och livscykel.

Informationsobjekt är de "byggklossar" som utbyts mellan system och aktörer. De definieras i **informationsmodellen** och mappas mot nationella och europeiska standarder där sådana finns.

**Exempel:** Ärende, Beslut, Person, Organisation, Händelse.

---

### Aktör

> En aktör är en människa, organisation eller system som interagerar med plattformen.

| Aktörstyp | Exempel |
|---|---|
| Intern användare | Handläggare, systemförvaltare |
| Extern medborgare | Privatperson som söker tjänst |
| Externt system | Partnerorganisations API |
| Bakgrundstjänst | Schemalagd integration |

---

### Integration

> En integration är en teknisk koppling mellan två eller flera system.

Integrationer klassificeras efter kopplingsgrad:

| Typ | Beskrivning | Kopplingsgrad |
|---|---|---|
| Filöverföring | Batch, t.ex. SFTP | Lös |
| Meddelandebaserad | Asynkron kö/ämne | Medel |
| API-anrop | Synkront REST/SOAP | Tät |
| Delad databas | Gemensam lagring | Mycket tät (undviks) |

---

### Informationsmodell

> Informationsmodellen specificerar struktur, semantik och relationer för plattformens informationsobjekt.

Modellen underhålls som ett UML-klassdiagram (PlantUML) och publiceras som maskinläsbart JSON-LD-schema. Ändringar hanteras via [öppna arkitekturbeslut](oppna-beslut/).

---

### SLA (servicenivåavtal)

> Ett SLA definierar de mätbara krav som en tjänst ska uppfylla.

Standardnivåer:

| Nivå | Tillgänglighet | Svarstid (p95) | Supporttid |
|---|---|---|---|
| Kritisk | 99,9 % | < 500 ms | 24/7 |
| Standard | 99,5 % | < 2 s | Kontorstid |
| Intern | 99,0 % | < 5 s | Bästa-möjliga |

---

### Arkitekturbeslut (ADR)

> Ett arkitekturbeslut dokumenterar ett val med tillhörande kontext, alternativ och konsekvenser.

Öppna (ej fattade) beslut listas på sidan [Öppna arkitekturbeslut](oppna-beslut/). Fattade beslut arkiveras i `beslut/` med status *accepterat* eller *avvisat*.

---

### Teknisk skuld

> Teknisk skuld är avvikelsen mellan nuläge och den arkitektur som krävs för att långsiktigt realisera förmågorna.

Skulden inventeras per förmåga under [Realisering](realisering/) och värderas i en riskviktad prioriteringsmatris.

---

## Ordlista (A–Ö)

| Begrepp | Definition | Se även |
|---|---|---|
| ADR | Architecture Decision Record | [Öppna beslut](oppna-beslut/) |
| API | Application Programming Interface | Tjänst |
| DSP | Digital Samordningsplattform — plattformens kortnamn | — |
| EIF | European Interoperability Framework | — |
| Förmåga | Se ovan | [Förmågor](formågor/) |
| Gap | Skillnad mellan förmågekrav och nuläge | [Realisering](realisering/) |
| Händelse | Inträffad förändring med arkiverings­värde | Informationsobjekt |
| Integration | Se ovan | — |
| Livscykel | Stadier ett informationsobjekt genomgår | Informationsobjekt |
| Mognadsgrad | Skala 1–5 för i vilken grad en förmåga är realiserad | [Realisering](realisering/) |
| SLA | Se ovan | — |
| Tjänst | Se ovan | — |
