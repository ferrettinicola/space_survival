---
type: world
tags: [mondo-principale, fisica, world]
---

# 🌌 Mondo Principale

> [!info] Overview
> Il mondo di default dove il giocatore spawna all'inizio di ogni partita. Struttura toroidale: uscendo da un bordo si rientra dal lato opposto.

← [[🏠 HOME]]

---

## Dimensioni e Fisica

| Parametro | Valore |
|---|---|
| Dimensioni | **20.000 × 20.000 px** |
| Struttura | Toroidale (wrapping su tutti i bordi) |
| Spawn giocatore | Centro esatto `(10.000, 10.000)` |
| Camera | Lerp diretto 12×dt — nessuna dead zone |

> [!note] Fisica Toroidale
> Uscendo dal bordo destro si rientra dal bordo sinistro, e così per tutti e 4 i lati. Il mondo non ha "fine" — si può esplorare all'infinito.

---

## Contenuto del Mondo

Il mondo viene **generato proceduralmente** ad ogni partita con distribuzione a griglia (una cella per oggetto + jitter casuale). Ogni tipo ha una distanza minima tra istanze.

→ Vedi [[Elementi del Mondo]] per tutti i dettagli su ogni oggetto.

| Tipo | Quantità | Dist. minima |
|---|---|---|
| Pianeti | 100 | 900px |
| Nebulose | 16 | 2.800px |
| Nuvole di polvere | 20 | 1.800px |
| Galassie | 18 | 2.200px |
| Cluster stellari | 12 | 2.400px |
| Supernove | 10 | 2.800px |
| Pulsar | 10 | 2.800px |
| Cinture di asteroidi | 10 | 2.500px |
| Buchi neri | 14 | 2.000px |
| Costellazioni | 6 | 2.000px |

---

## Nemici Presenti

- [[Meteoriti]] — Spawn continuo, 3 tipi principali
- [[Alieni]] — Spawn ogni 10s, max 8 contemporanei, 4 tipi

---

## Loop di Gioco

```
Spawn → Esplora → Evita/Distruggi meteoriti
      → Combatti alieni → Raccogli power-up
      → Entra nel [[Secondo Mondo]] (opzionale)
      → Sopravvivi il più a lungo possibile
```

---

## Punteggio nel Mondo Principale

| Evento | Punti |
|---|---|
| Ogni secondo sopravvissuto | +1 |
| Meteorite normale | +3 |
| Meteorite rosso | +5 |
| Meteorite cristallo (+ frammenti) | +7 ciascuno |
| Alieno Scout / Caotico / Bombardiere | +20 |
| Dreadnought | +50 |

→ Vedi [[Punteggio e HUD]] per il sistema completo.
