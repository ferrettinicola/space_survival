---
type: dashboard
tags: [index, space-race]
---

# 🚀 SPACE RACE — Project Hub

> [!quote] Concept
> Sparatutto arcade spaziale in HTML5 Canvas + JS vanilla. Il giocatore pilota una navicella in un mondo toroidale 20.000×20.000px, evita e distrugge meteoriti, combatte alieni e sopravvive il più a lungo possibile.

---

## 🗺️ Struttura del Gioco

| Mondo | Descrizione | Accesso |
|---|---|---|
| [[Mondo Principale]] | Mondo di partenza, toroidale 20k×20k | Spawn diretto |
| [[Secondo Mondo]] | Void Dimension, 45 secondi, 1.875× velocità | Entrare in un [[Elementi del Mondo#Buchi Neri\|Buco Nero]] |

---

## 📂 Note Principali

### 🌌 Mondo Principale
- [[Mondo Principale]] — Overview e fisica
- [[Elementi del Mondo]] — Pianeti, nebulose, galassie, buchi neri
- [[La Navicella]] — Le 4 navi, controlli, statistiche
- [[Meteoriti]] — Tipi, comportamento, danni
- [[Alieni]] — 4 tipi, AI, drop
- [[Power-Up]] — Star Power, Scudo, Fuoco Rapido, HP

### 🌑 Secondo Mondo
- [[Secondo Mondo]] — Overview, regole, fisica
- [[Nemici del Void]] — Meteoriti void + Torrette
- [[Transizioni]] — Entrata e uscita dal buco nero

---

## 📊 Stato Attuale

> [!success] Funzionante
> - Sistema di gioco completo
> - 2 mondi distinti
> - 4 navi con abilità speciali
> - Sistema power-up
> - Classifica con localStorage
> - i18n IT/EN

> [!warning] Da Migliorare
> - Nessun audio
> - Mobile da rifinire
> - Nessuna progressione a lungo termine
> - Bilanciamento da testare

> [!todo] Idee Future
> - [ ] Audio con Web Audio API
> - [ ] Sistema di upgrade tra partite
> - [ ] Boss fight dedicata
> - [ ] Sblocco progressivo navi
> - [ ] Achievement

---

## 🔧 Tecnologia

```
Linguaggio   → HTML5 + CSS3 + JavaScript vanilla
Rendering    → Canvas 2D API
File         → Singolo .html (~4700 righe)
Storage      → localStorage (classifica, skin, lingua, nome)
Lingue       → Italiano / Inglese (i18n completo)
```
