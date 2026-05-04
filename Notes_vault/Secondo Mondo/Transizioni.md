---
type: reference
tags: [transizioni, void, animazioni, secondo-mondo]
---

# 🌀 Transizioni

> [!info]
> Le animazioni di entrata e uscita dal [[Secondo Mondo]]. Entrambe bloccano il gameplay durante l'animazione — il giocatore non può essere danneggiato.

← [[Secondo Mondo]]

---

## Transizione di Entrata

**Durata totale**: 2,8 secondi — 3 fasi sequenziali.

Trigger: la navicella tocca l'orizzonte degli eventi di un [[Elementi del Mondo#Buchi Neri|Buco Nero]].

### Fase 1 (0% → ~50%)
- 14 **anelli concentrici** spiralano verso il centro
- 24 **raggi rotanti** si comprimono verso il centro
- Il buco nero cresce fino a riempire lo schermo

### Fase 2 (~50% → ~70%)
- **Flash bianco-viola accecante**
- Transizione istantanea di luminosità

### Fase 3 (~70% → 100%)
- **Dissolvenza** dal bianco verso il Secondo Mondo
- Lo sfondo void si materializza gradualmente

---

## Transizione di Uscita

**Durata totale**: 2,6 secondi — 3 fasi sequenziali (inversa all'entrata).

Trigger: automatica dopo **45 secondi** nel Secondo Mondo.

> [!success] Invincibilità
> Durante l'intera transizione di uscita il giocatore è invincibile. Meteoriti, torrette e laser non causano danni.

### Fase 1 (0% → 35%)
- **Raggi spiralano verso l'interno** (inverso all'entrata)
- **Vignetta scura** che cresce dai bordi verso il centro
- **Anelli collassano** dall'esterno verso l'interno
- Effetto di "compressione" dello spazio

### Fase 2 (35% → 60%)
- **Flash bianco-viola** che sfuma (inverso: brillante → spento)
- Luminosità decresce da 1 a 0

### Fase 3 (60% → 100%)
- **Overlay nero** che si dissolve progressivamente
- **Anello viola in espansione** — effetto "nascita" nel mondo principale
- Il mondo principale appare gradualmente dietro

### Al Completamento
```
exitVoid() chiamata → inVoid = false
Player respawnato vicino al centro del Mondo Principale
Player.x = 10.000 ± 200px casuale
Player.vx = Player.vy = 0
Camera aggiornata immediatamente
Void arrays svuotati (meteoriti, proiettili, particelle, torrette)
```

---

## Stato Durante le Transizioni

| Elemento | Entrata | Uscita |
|---|---|---|
| Gameplay | ❌ Bloccato | ❌ Bloccato |
| Danni al giocatore | ❌ Impossibile | ❌ Impossibile |
| Timer generale | ✅ Continua | ✅ Continua |
| Void timer | ✅ Continua | ❌ Bloccato |
| Score | ❌ Bloccato | ❌ Bloccato |

---

## Note per Sviluppi Futuri

> [!todo] Idee
> - [ ] Audio sincronizzato con le fasi (swoosh, flash, boom)
> - [ ] Feedback aptico su mobile durante i flash
> - [ ] Transizione diversa se si entra nel void con Star Power attivo
> - [ ] Piccola cutscene testuale durante la fase 2 ("SEI NEL VOID")
