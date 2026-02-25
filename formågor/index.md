---
layout: default
title: Förmågor
nav_order: 3
has_children: true
---

# Förmågor
{: .no_toc }

Förmågor beskriver *vad* plattformen ska kunna göra, oberoende av teknisk implementation. Varje förmåga har ett tydligt syfte, definierade intressenter och mätbara kvalitetskrav.

---

## Förmågeöversikt

| ID | Förmåga | Prioritet | Mognadsgrad (mål) | Status |
|---|---|---|---|---|
| F1 | [Informationsutbyte](f1/) | Hög | 4 / 5 | Pågår |
| F2 | [Ärendehantering](f2/) | Hög | 4 / 5 | Pågår |
| F3 | [Analys och uppföljning](f3/) | Medel | 3 / 5 | Planerad |

### Mognadsgrader

| Nivå | Innebär |
|---|---|
| 1 – Initial | Ad hoc, inga definierade processer |
| 2 – Definierad | Process finns men tillämpas inkonsekvent |
| 3 – Standardiserad | Konsekvent tillämpning, viss mätning |
| 4 – Hanterad | Mätning och styrning på plats |
| 5 – Optimerad | Kontinuerlig förbättring, fullt automatiserad |

---

## Hur förmågor relaterar till plattformen

En förmåga realiseras av en eller flera **tjänster** och konsumeras av en eller flera **aktörer**. Relationen dokumenteras i respektive förmågebeskrivning och spåras in i [Realisering](../realisering/).

```
Aktör ──använder──▶ Förmåga ──realiseras av──▶ Tjänst/System
                       │
                       └──beskrivs med──▶ Informationsobjekt
```
