# SPACE RACE — Documento di Contesto Completo

## Panoramica

**SPACE RACE** è uno sparatutto arcade spaziale in HTML5 Canvas + JavaScript vanilla (nessuna libreria esterna). Il giocatore pilota una navicella in un mondo toroidale 20.000×20.000 pixel, evita e distrugge meteoriti, combatte navi aliene e sopravvive il più a lungo possibile. Contiene due mondi distinti: il Mondo Principale e il Secondo Mondo (accessibile entrando in un buco nero).

---

## Tecnologia

- **Linguaggio**: HTML5 + CSS3 + JavaScript vanilla
- **Rendering**: Canvas 2D API (nessun WebGL)
- **File**: singolo file `.html` (~4700 righe)
- **Storage**: `localStorage` per classifica, skin selezionata, lingua, nome giocatore
- **Lingue supportate**: Italiano e Inglese (i18n completo)

---

## Il Mondo

### Dimensioni e Fisica
- Mondo toroidale **20.000×20.000 px**: uscendo da un bordo si rientra dal lato opposto
- Spawn giocatore al centro esatto (`10000, 10000`)
- Camera segue il giocatore con lerp diretto (nessuna dead zone, movimento fluido)

### Oggetti di Sfondo (generati ogni partita, distribuzione a griglia)

| Tipo | Quantità | Distanza minima | Caratteristica |
|---|---|---|---|
| **Pianeti** | 100 | 900px | Raggio 55–165px, anelli (30%), lune (0–2) |
| **Nebulose** | 16 | 2800px | Grandi nuvole colorate (r 1600–3600px), molto tenui |
| **Nuvole di polvere** | 20 | 1800px | Grandi patch atmosferiche semitrasparenti |
| **Galassie** | 18 | 2200px | Ellissi di stelle colorate |
| **Cluster stellari** | 12 | 2400px | Campi di 65–135 stelle |
| **Supernove** | 10 | 2800px | Sfere pulsanti con raggi filamentosi, 7 colori |
| **Pulsar** | 10 | 2800px | Stelle con raggi rotanti, effetto orbita sui meteoriti |
| **Cinture di asteroidi** | 10 | 2500px | Ellissi di punti rocciosi decorativi |
| **Buchi neri** | 14 | 2000px | Portali al Secondo Mondo (vedi sezione dedicata) |
| **Costellazioni** | 6 | 2000px | Asterismi basati su coordinate RA/Dec reali |

#### Costellazioni (coordinate astronomiche reali)
Le 6 costellazioni hanno pattern basati su dati RA/Dec reali: **Grande Carro**, **Orione**, **Cassiopea**, **Leone**, **Scorpione**, **Cigno**. Posizione casuale ogni partita, angolo di rotazione casuale, linee in blu tenue, stelle con glow e flare a croce sulle principali.

#### Fisica Orbitale
Pulsar e Supernove esercitano due forze sui meteoriti vicini (raggio 260–320px):
- **Forza centripeta**: spinge verso l'orbita ideale (55% del raggio), crea orbite stabili
- **Forza tangenziale**: spinta perpendicolare che fa ruotare i meteoriti attorno all'oggetto (CW per pulsar, CCW per supernove)

---

## La Navicella

### Punti Vita
- HP iniziali: **20/20**
- HUD: barra verde (>10HP) → arancio (5-10HP) → rossa lampeggiante (≤5HP) + testo numerico

### Controlli
| Input | Azione |
|---|---|
| ↑↓←→ / WASD | Movimento |
| SPAZIO | Boost (barra gialla si svuota, ricarica automatica) |
| Click / F | Sparo verso il cursore del mouse |

### Boost
- Consumo: 1.8× drain rate, ricarica automatica (~3.5s ricarica completa)
- Moltiplicatore velocità durante boost: **2.8×**
- **Illimitato nel Secondo Mondo** (barra diventa viola)

### Munizioni (barra cyan)
- Ogni sparo consuma ~5.5% del serbatoio
- Ricarica automatica rilasciando il tasto (~5.5s ricarica completa)
- A 0% non si può sparare; barra diventa rossa sotto il 25%
- **Illimitate nel Secondo Mondo**
- **Illimitate durante Star Power**

### Danni ricevuti
| Fonte | Danno HP |
|---|---|
| Meteorite grande (size ≥22) | **20 HP** (morte istantanea) |
| Meteorite piccolo (size <22, frammento) | **5 HP** |
| Meteorite rosso (fast) | **20 HP** |
| Meteorite cristallo (special) | **20 HP** |
| Contatto alieno | **5 HP** |
| Laser alieno | **5 HP** |
| Laser torretta (Secondo Mondo) | **2 HP** |
| Buco nero (orizzonte degli eventi) | Teletrasporto nel Secondo Mondo |

**Iframe**: 0.9 secondi di invincibilità dopo ogni danno ricevuto.

---

## Le 4 Navi

| Nave | Velocità | Vel. Max | Cooldown | Vel. Proiettile | Dimensione Colpi |
|---|---|---|---|---|---|
| **VIPER** (cyan) | 345 | 442 | 0.18s | 910 px/s | Medi |
| **SCORPION** (arancio) | 403 | 520 | 0.26s | 728 px/s | Grandi |
| **PHANTOM** (viola) | 254 | 351 | 0.09s | 1248 px/s | Piccoli |
| **TITAN** (oro) | 215 | 310 | 0.38s | 820 px/s | Enormi (piercing 2) |

### Abilità Speciali (attivate raccogliendo la stellina dell'abilità, 12 secondi)

| Nave | Abilità | Effetto |
|---|---|---|
| **VIPER** | DOPPIO RAGGIO | Ogni sparo genera 2 proiettili gemelli a ±0.18 rad di offset |
| **SCORPION** | RAFFICA PESANTE | Burst potenziato (in sviluppo) |
| **PHANTOM** | INVISIBILITÀ | Invincibilità completa per 12 secondi |
| **TITAN** | SUPERNOVA | Ogni 2.5s distrugge tutto nel raggio 400px con onda d'urto dorata |

---

## I Meteoriti

### Tipi (Mondo Principale)

| Tipo | Colore | Velocità | Danno | Punti |
|---|---|---|---|---|
| **Normale** | Marrone/ocra 3D | Base (~60–138 px/s) | 20 HP se grande, 5 HP se piccolo | +3 |
| **Rosso** (fast) | Rosso con glow | 2.5× velocità normale | 20 HP | +5 |
| **Cristallo** (special) | Azzurro ghiaccio | Normale | 20 HP | +7 (+7 per frammento) |

**Cristallo**: colpendo si frammenta in **3 frammenti** più veloci (110–200px/s), ciascuno anch'esso `special` (7pt). Flash cyan+bianco al momento dello shatter.

**Meteor del Bombardiere**: lancia meteoriti con scia di scintille arancioni (`isBomb`).

### Frammenti (generati da splitMeteor/beamSplit)
- Size < 22px
- Danno: **5 HP** (non più innocui)
- Non classificati come `fast` o `special`

---

## I Meteoriti del Secondo Mondo

4 tipi visualmente distinti, tutti `isVoidMeteor = true`:

| Tipo | Colore | Glow | Velocità | Frequenza |
|---|---|---|---|---|
| 0 — Standard | Ossidiana viola-nera | Viola | Base | 45% |
| 1 — Plasma | Viola brillante + nucleo luminoso | Fucsia intenso | Base | 23% |
| 2 — Ghost | Quasi trasparente, scuro | Viola tenue | Base | 17% |
| 3 — Shard | Rosso-nero | Rosso fuoco | 1.7× velocità | 15% |

Tutti danno **10 punti** se distrutti (vs 3/5/7 nel mondo principale).

---

## Gli Alieni

Spawn ogni 10 secondi (dopo 8s di gioco), max 8 contemporanei. 50% spawna vicino alla camera, 50% in posizione casuale nel mondo. Dopo 60s: 35% probabilità di doppio spawn.

### 4 Tipi

| Tipo | Colore | HP | Comportamento | Frequenza | Drop |
|---|---|---|---|---|---|
| **Scout** | Verde | 3 | Orbita ellittica, 1 colpo mirato ogni 3.5–7.5s | 46% | ❤️ +10 HP |
| **Caotico** | Rosso/punte | 3 | Orbita ellittica, 3–5 colpi random ogni 0.8–2.3s | 26% | ⚡ Rapid Fire 30s |
| **Bombardiere** | Viola esagonale | 3 | Orbita ellittica, lancia meteore-bomba ogni 4–7s | 18% | 🛡 Scudo 30s |
| **Dreadnought** | Oro/armatura | 5 | Orbita lenta, tripla salva ogni 4–7s, HP barre nascoste | 10% | ⭐ Star Power 45s + 🔥 Abilità Nave 12s |

**Orbita**: tutti gli alieni seguono un'ellisse con centro che deriva lentamente verso il giocatore. Velocità orbitale con burst imprevedibili (sin-based). I colpi laser sono diversi per colore per ogni tipo.

**Danno contatto**: 5 HP. **Danno laser**: 5 HP. **Punti**: 20pt (Scout/Caotico/Bomb), 50pt (Dreadnought).

---

## Power-Up (Drop dagli Alieni)

| Icona | Drop da | Durata | Effetto |
|---|---|---|---|
| ❤️ Croce verde | Scout | Istantaneo | +10 HP |
| ⚡ Fulmine arancio | Caotico | 30 secondi | Fuoco rapido: 5× cadenza + munizioni infinite + velocità +60% |
| 🛡 Esagono viola | Bombardiere | 30 secondi | Scudo: invincibilità completa, aura viola visibile |
| ⭐ Stella dorata | Dreadnought | 45 secondi | **Star Power**: vedi sezione dedicata |
| 🔥 Stellina accent | Dreadnought | 12 secondi | Abilità nave specifica |

I power-up fluttuano nel punto di morte dell'alieno e scompaiono dopo 25 secondi. Una barra laterale destra mostra tutti i boost attivi con timer e barra di avanzamento.

### Star Power (45 secondi) — il più potente
- **Velocità**: +120% (superMult 2.2×)
- **Invincibilità** completa (iframe rinnovato ogni frame)
- **Munizioni infinite**
- **Scudo 220px**: distrugge automaticamente qualsiasi meteorite nel raggio
- **Missili guidati**: fuoco automatico verso i 2 meteoriti più vicini entro 500px, 3× cadenza, piercing ×3
- **Visuale**: raggi dorati rotanti, sparkle orbitanti, anello scudo semitrasparente, barra timer sopra la nave (diventa rossa lampeggiante negli ultimi 10s)

---

## Il Buco Nero

### Aspetto Visivo (8 layer)
1. Campo gravitazionale vasto (22× raggio, glow viola)
2. **Jet relativistici** (due fasci perpendicolari al disco)
3. **Disco di accrescimento** (4 anelli: marrone → arancio → giallo → bianco-giallo)
4. Wisps interni contro-rotanti
5. **Fotosfera** (anello di lensing gravitazionale)
6. Orizzonte degli eventi (nero assoluto)
7. **Rim di blueshift** (sottile alone bianco-azzurro)
8. 8 particelle di materia in caduta lungo il disco

### Gravità
- Raggio di influenza: **24× raggio** del buco nero (~1320–2640px)
- Forza: curva cubica: `12 + 900 × t³` (quasi impercettibile lontano, forte vicino)
- I meteoriti vengono attratti proporzionalmente (inversamente proporzionale alla loro dimensione)
- Distanza minima tra buchi neri: **2000px**

---

## Il Secondo Mondo (Void Dimension)

### Accesso
Avvicinarsi all'orizzonte degli eventi di un buco nero.

### Transizione di Entrata (2.8 secondi, 3 fasi)
1. **Fase 1**: 14 anelli concentrici spiralano verso il centro, 24 raggi rotanti comprimono, buco nero nero cresce
2. **Fase 2**: Flash bianco-viola accecante
3. **Fase 3**: Dissolvenza nel Secondo Mondo

### Il Mondo Void
- **Sfondo**: nero assoluto (`#020004`) con nebulose viola scuro, nuvole atmosferiche
- **Stelle** a 3 layer con parallasse 3.5× amplificata (scorrono velocemente)
- **Oggetti di mondo**: nebulose morte, orbi pulsanti viola, cluster ombra, rift/crepe luminose, 4 supernove colorate

### Fisica e Regole
- Tempo **1.875×** più veloce (timer, score, fisica)
- **Boost illimitato** (barra diventa viola)
- **Munizioni illimitate**
- Nessun boost di velocità aggiuntivo
- Il timer generale continua normalmente

### Nemici nel Void
**Meteoriti** (4 tipi diversi dal mondo principale, vedi sopra) + **6 torrette**:
- Esagonali arancioni, 3 HP, girano verso il giocatore
- Sparano ogni 2.5–4.5s, danno **2 HP**
- Se distrutte: **+5 HP** al giocatore + **+15 punti** + esplosione arancione

### Durata e Uscita
- Sopravvivi **45 secondi**: barra viola con countdown in secondi visibile in cima allo schermo
- Dopo 45s: **transizione di uscita** animata (2.6 secondi, inversa all'entrata) → espulsione automatica nel mondo principale

### Transizione di Uscita (2.6 secondi, 3 fasi)
1. **Fase 1**: Raggi spiralano verso l'interno, vignetta dal bordo, anelli collassano
2. **Fase 2**: Flash bianco-viola che sfuma
3. **Fase 3**: Overlay nero che si dissolve, anello viola in espansione "nascita"

---

## Punteggio

| Evento | Punti |
|---|---|
| Ogni secondo sopravvissuto | +1 |
| Meteorite normale colpito | +3 |
| Meteorite rosso | +5 |
| Meteorite cristallo (+ ogni frammento) | +7 |
| Meteorite nel Secondo Mondo | +10 |
| Alieno (Scout/Caotico/Bombardiere) | +20 |
| Dreadnought | +50 |
| Torretta nel Secondo Mondo | +15 |

---

## HUD e Interfaccia

### Durante il Gioco
- **Centro in alto**: pannello con VITA (barra 100px + testo numerico), BOOST (barra gialla), FUOCO (barra cyan→rossa)
- **Alto destra**: Punteggio attuale (oro, grande) + Record sotto
- **Basso destra**: Timer partita (discreto, faded)
- **Destra sidebar**: Power-up attivi con icona + barra timer + secondi rimanenti (sparisce se nessun boost attivo)
- **Durante Void**: scritta "◈ VOID DIMENSION ◈" + barra viola + countdown in secondi al centro in alto
- **Flash rosso**: schermo tinge di rosso ad ogni danno ricevuto

### Schermate
- **Schermata principale**: animata con stelle parallax + pianeti/oggetti che derivano, meteore decorative lente
- **Modal Navi**: griglia 2×2, click → pannello dettaglio con barre stats + descrizione abilità
- **Modal Istruzioni**: 3 tab — Controlli / Punteggio / Universo (enciclopedia elementi di gioco)
- **Modal Classifica**: top 20, deduplicata per nome (case-insensitive, mantiene miglior score)
- **Game Over**: statistiche + inserimento nome + classifica aggiornata + bottoni Riprova/Menu

---

## Classifica

- Salvata in `localStorage('vr_scores')` come array `[{name, score, time}]`
- **Deduplicazione**: stesso nome (case-insensitive) → mantiene solo il punteggio più alto
- Max 20 entry, ordinate per score decrescente

---

## Sistema i18n

Tutte le stringhe UI disponibili in **Italiano** e **Inglese**. Il tasto 🌐 EN/IT è visibile nelle schermate di menu e scompare durante il gameplay. La preferenza è salvata in `localStorage('vr_lang')`.

---

## Architettura Tecnica Rilevante

- **Loop**: `requestAnimationFrame` con `dt` cappato a 50ms
- **Camera**: lerp diretto (12× dt), nessuna dead zone
- **Particelle**: sistema unificato `particles[]` + `thrustParticles[]` + `voidParticles[]`
- **Bullets**: array `bullets[]` (mondo) + `voidBullets[]` (void) + `alienBullets[]`
- **Funzioni chiave**: `initWorld()`, `updatePlayer()`, `tryShoot()`, `updateVoid()`, `enterVoid()`, `exitVoid()`, `updateSuperMode()`, `updateShipAbility()`, `damagePlayer()`, `spawnDeathExplosion()`
- **State machine**: `state = 'start' | 'playing' | 'dead'` + `inVoid: boolean`
