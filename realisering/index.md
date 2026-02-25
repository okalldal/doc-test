---
layout: default
title: Realisering
nav_order: 5
has_children: true
---

# Realisering – nuläge och gap
{: .no_toc }

Denna del av dokumentationen beskriver i vilken utsträckning nuvarande systemlandskap **faktiskt realiserar** de identifierade förmågorna. Varje förmåga utvärderas mot dess kvalitetskrav och ges en mognadsgrad.

---

## Nulägesbild per förmåga

| Förmåga | Nuläge (mognadsgrad) | Mål | Gap |
|---|---|---|---|
| [F1 – Informationsutbyte](f1/) | 2 – Definierad | 4 | Stort |
| [F2 – Ärendehantering](f2/) | 3 – Standardiserad | 4 | Medel |
| F3 – Analys och uppföljning | 1 – Initial | 3 | Stort |

### Förklaring av gap-klassificering

| Gap | Innebär |
|---|---|
| Litet | ≤ 1 mognadsgrads skillnad; åtgärder inom befintliga resurser |
| Medel | 1–2 nivåers skillnad; kräver dedikerat projekt |
| Stort | ≥ 2 nivåers skillnad; kräver ny kapabilitet eller upphandling |

---

## Systemlandskap (förenklad)

```
┌─────────────────────────────────────────────────────────────────┐
│                     Nuvarande systemlandskap                    │
│                                                                 │
│  ┌──────────────┐   ┌──────────────┐   ┌──────────────────┐    │
│  │  Legacy ESB  │   │  Ärendesys A │   │   Ärendesys B    │    │
│  │  (IBM MQ)    │   │  (DiA v2.3)  │   │   (Platina 6)    │    │
│  └──────┬───────┘   └──────┬───────┘   └────────┬─────────┘    │
│         │                 │                    │               │
│         └─────────────────┼────────────────────┘               │
│                           ▼                                    │
│                  ┌────────────────┐                            │
│                  │   Integrationsb│  ← planerat, ej driftsatt  │
│                  │   -plattform   │                            │
│                  └────────────────┘                            │
│                                                                 │
│  BI-verktyg: Excel + Power BI (ad hoc, ej ansluten till DSP)   │
└─────────────────────────────────────────────────────────────────┘
```

---

## Prioriteringsmatris

Gapen rangordnas efter **riskvikt × nyttopotential**:

| Prioritet | Åtgärd | Berörd förmåga | Typ |
|---|---|---|---|
| 1 | Ersätt Legacy ESB med händelsedriven buss | F1 | Ny infrastruktur |
| 2 | Inför gemensamt ärendeschema (ADR-001) | F2 | Standardisering |
| 3 | Anslut Ärendesys B till integrationsplattform | F2 | Integration |
| 4 | Etablera analyslager (ADR-005) | F3 | Ny kapabilitet |
| 5 | Inför schemavalidering på alla F1-meddelanden | F1 | Kvalitetshöjning |
