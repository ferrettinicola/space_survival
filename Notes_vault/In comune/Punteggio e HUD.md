---
type: reference
tags: [punteggio, hud, interfaccia, sistema]
---

# 📊 Punteggio e HUD

← [[🏠 HOME]]

---

## Sistema di Punteggio

| Evento | Punti |
|---|---|
| Ogni secondo sopravvissuto | +1 |
| Ogni secondo nel Void (1,875×) | +1,875 |
| Meteorite normale colpito | +3 |
| Meteorite rosso | +5 |
| Meteorite cristallo (+ ogni frammento) | +7 |
| Meteorite nel Secondo Mondo | +10 |
| Alieno Scout / Caotico / Bombardiere | +20 |
| Dreadnought | +50 |
| Torretta nel Secondo Mondo | +15 |

---

## HUD Durante il Gioco

### Pannello Centrale (in alto)
- **VITA**: barra 100px + testo numerico
  - Verde se HP > 10
  - Arancio se HP 5–10
  - Rossa lampeggiante se HP ≤ 5
- **BOOST**: barra gialla (viola nel Void)
- **FUOCO**: barra cyan → rossa sotto 25%

### Alto Destra
- Punteggio attuale (oro, grande)
- Record personale sotto

### Basso Destra
- Timer partita (discreto, faded)

### Sidebar Destra
- Power-up attivi con: icona + barra timer + secondi rimanenti
- Scompare se nessun boost è attivo

### HUD Void
- **◈ VOID DIMENSION ◈** in cima
- Barra viola con countdown in secondi
- Barre boost e munizioni diventano viola

### Flash Rosso
- Lo schermo si tinge di rosso ad ogni danno ricevuto

---

## Classifica

- Salvata in `localStorage('vr_scores')` come array `[{name, score, time}]`
- **Deduplicazione per nome** (case-insensitive): mantiene solo il punteggio più alto per ogni giocatore
- Max **20 entry**, ordinate per score decrescente
- Visibile nella schermata Game Over e nel modal dedicato

---

## Schermate

| Schermata | Descrizione |
|---|---|
| **Start** | Animata con stelle parallax + oggetti che derivano |
| **Modal Navi** | Griglia 2×2 con pannello dettaglio e barre stats |
| **Modal Istruzioni** | 3 tab: Controlli / Punteggio / Universo |
| **Modal Classifica** | Top 20 con nome, score, tempo |
| **Game Over** | Stats + input nome + classifica + bottoni |

---

## i18n

- Tutte le stringhe disponibili in **Italiano** e **Inglese**
- Tasto 🌐 EN/IT visibile nei menu, nascosto durante il gameplay
- Preferenza salvata in `localStorage('vr_lang')`
