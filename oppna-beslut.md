---
layout: default
title: Öppna arkitekturbeslut
nav_order: 4
---

# Öppna arkitekturbeslut
{: .no_toc }

Denna sida listar arkitekturbeslut som ännu **inte är fattade**. Formatet är inspirerat av Architecture Decision Records (ADR). Varje beslut har en ansvarig, en tidsgräns och ett spår av alternativ.

Fattade beslut arkiveras i `beslut/` och länkas i efterhand.

{: .warning }
**6 öppna beslut** kräver svar senast Q2 2026. Se tabellen nedan.

<details open markdown="block">
  <summary>Innehåll</summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---

## Sammanfattning

| ID | Titel | Berörd förmåga | Beslut senast | Ansvarig |
|---|---|---|---|---|
| [ADR-001](#adr-001) | Enhetligt ärendeschema | F2 | 2026-03-31 | Arkitekt A |
| [ADR-002](#adr-002) | Val av meddelandeformat | F1 | 2026-03-15 | Arkitekt B |
| [ADR-003](#adr-003) | Arkiveringsstrategi för ärenden | F2 | 2026-04-30 | Juridik + Arkitekt A |
| [ADR-004](#adr-004) | Stöd för realtidsströmmar | F1 | 2026-05-31 | Arkitekt B |
| [ADR-005](#adr-005) | Val av analysdatabas | F3 | 2026-06-30 | Arkitekt C |
| [ADR-006](#adr-006) | Pseudonymiseringsstrategi | F3 | 2026-06-30 | Dataskyddsombud + Arkitekt C |

---

## ADR-001

### Enhetligt ärendeschema

**Status:** Öppet
**Berörd förmåga:** [F2 – Ärendehantering](formågor/f2/)
**Beslut senast:** 2026-03-31
**Ansvarig:** Arkitekt A

#### Kontext

Plattformen integrerar mot tre befintliga ärendehanteringssystem med delvis överlappande men icke-kompatibla datamodeller. Utan ett gemensamt schema tvingas varje konsument hantera N olika format, vilket ökar komplexitet och fel.

#### Frågeställning

Vilket gemensamt ärendeschema ska plattformen använda som kanoniskt format för F2?

#### Alternativ

| Alt | Beskrivning | Fördelar | Nackdelar |
|---|---|---|---|
| A | Definiera eget minimalt schema | Full kontroll, enkelt | Underhållsbörda, ingen community |
| B | Adoptera [OASIS Case Management Model](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=cmmn) (CMMN) | Standard, verktygsstöd | Komplex, överkonstruerat för vårt behov |
| C | Basera på Digg:s Mina ärenden-modell | Nationellt harmoniserat | Begränsat till medborgarmötet |
| D | Hybrид: Digg som yttermodell, internt minimalt schema | Harmoni + enkelhet | Kräver mappningslager |

#### Rekommendation (preliminär)

Alternativ D — hybridmodell. Inväntar bekräftelse från Digg-samordning.

---

## ADR-002

### Val av meddelandeformat

**Status:** Öppet
**Berörd förmåga:** [F1 – Informationsutbyte](formågor/f1/)
**Beslut senast:** 2026-03-15
**Ansvarig:** Arkitekt B

#### Kontext

F1 behöver ett standardiserat format för strukturerade meddelanden som stödjer versionering, schemavalidering och framåt/bakåtkompabilitet.

#### Frågeställning

Vilket meddelandeformat ska vara primärt för maskin-till-maskin-kommunikation inom F1?

#### Alternativ

| Alt | Format | Fördelar | Nackdelar |
|---|---|---|---|
| A | JSON + JSON Schema | Välkänt, enkelt | Verbose, inget inbyggt schema-registry |
| B | Apache Avro | Kompakt, schema-registry | Kräver Confluent/schema-server |
| C | Protocol Buffers (protobuf) | Effektivt, starkt typat | Kräver kodgenerering, inlärningströskel |
| D | CloudEvents + JSON | Standardiserat event-format | Passar events men inte request/response |

#### Rekommendation (preliminär)

Alternativ A för request/response-mönster, alternativ D för händelsenotifieringar. Kräver bekräftelse att JSON Schema-versionshantering täcker behoven.

---

## ADR-003

### Arkiveringsstrategi för ärenden

**Status:** Öppet
**Berörd förmåga:** [F2 – Ärendehantering](formågor/f2/)
**Beslut senast:** 2026-04-30
**Ansvarig:** Juridik + Arkitekt A

#### Kontext

Avslutade ärenden måste arkiveras i enlighet med arkivlagen och myndighetens informationshanteringsplan. Det är oklart om arkivering ska ske centralt via plattformen eller delegeras till källsystemen.

#### Frågeställning

Var och hur arkiveras ärenden som handläggs via plattformen?

#### Alternativ

| Alt | Ansvar | Fördelar | Nackdelar |
|---|---|---|---|
| A | Centralt via plattformens arkivtjänst | Enhetlighet, ett gränssnitt | Kräver ny tjänst, kompetens |
| B | Delegerat till källsystem | Befintlig infrastruktur | Inkonsekvent, svår att granska |
| C | Hybridmodell: metadata centralt, handlingar i källsystem | Balans | Komplex sökmodell |

#### Beroenden och öppna frågor

- Pågående upphandling av e-arkiv kan påverka valet — beslut bör samordnas.
- Juridisk utredning om arkivansvar för plattformsägd data pågår (klar april 2026).

---

## ADR-004

### Stöd för realtidsströmmar

**Status:** Öppet
**Berörd förmåga:** [F1 – Informationsutbyte](formågor/f1/)
**Beslut senast:** 2026-05-31
**Ansvarig:** Arkitekt B

#### Kontext

Tre intressenter har uttryckt behov av händelseströmmar med latens under 100 ms — vilket är utanför nuvarande F1-kravs scope. Beslut behövs om detta ska ingå i F1 eller hanteras separat.

#### Frågeställning

Ska F1 utvidgas med stöd för realtidsströmmar, eller hanteras det som en separat förmåga?

#### Alternativ

| Alt | Ansats |
|---|---|
| A | Utvidga F1 med strömningsstöd (Kafka/Pulsar) |
| B | Definiera F4 – Realtidshändelser som separat förmåga |
| C | Avvakta och utvärdera behov om 12 månader |

#### Öppna frågor

- Vilka av de tre intressenterna har faktiska SLA-krav vs. önsketänkande?
- Driftsorganisationens kapacitet att förvalta en strömningsplattform är oklar.

---

## ADR-005

### Val av analysdatabas

**Status:** Öppet
**Berörd förmåga:** [F3 – Analys och uppföljning](formågor/f3/)
**Beslut senast:** 2026-06-30
**Ansvarig:** Arkitekt C

#### Kontext

F3 kräver ett analyslager som kan hantera tidsseriedata, aggregeringar och ad-hoc-queries över minst 24 månaders historik, med god prestanda för interaktiva dashboards.

#### Alternativ

| Alt | Teknik | Fördelar | Nackdelar |
|---|---|---|---|
| A | ClickHouse | Exceptionell OLAP-prestanda, kolumnär | Relativt ny i myndighetsmiljöer |
| B | PostgreSQL + TimescaleDB | Välkänt, PostgreSQL-kompabilitet | Sämre vid hög volym |
| C | Managed service (t.ex. BigQuery, Redshift) | Skalbarhet, drift ingår | Datahemvist, upphandlingskrav |
| D | Befintlig BI-plattform (om sådan finns) | Inget nytt system | Ofta ej optimerad för händelsedata |

---

## ADR-006

### Pseudonymiseringsstrategi

**Status:** Öppet
**Berörd förmåga:** [F3 – Analys och uppföljning](formågor/f3/)
**Beslut senast:** 2026-06-30
**Ansvarig:** Dataskyddsombud + Arkitekt C

#### Kontext

F3:s analyslager innehåller händelseloggar som kan innehålla indirekta personuppgifter (ärendenummer, IP-adresser, tidsmönster). GDPR kräver att analys sker på pseudonymiserade data.

#### Frågeställning

Vilken pseudonymiseringsteknik och vilket ansvarsmönster ska användas?

#### Alternativ

| Alt | Teknik | Fördelar | Nackdelar |
|---|---|---|---|
| A | Tokenisering vid inmatning (ETL-lager) | Enkelt, transparent | Nyckelhantering känslig |
| B | Differential privacy vid aggregering | Starkt integritetsskydd | Komplext, noggrannhetsförlust |
| C | K-anonymitet på exporterade rapporter | Väletablerat | Skyddar inte mot bakgrundskunskap |

#### Öppna frågor

- DSO-utlåtande om kravet på länkbarhet för felsökning inväntas.
- Vilken minimal pseudonymiseringsnivå accepteras för intern driftsövervakning?
