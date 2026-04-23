# Poncho Quest — La Torre di Simo

Mini-gioco platform verticale con Simo che scala una torre di palazzo notturno.

## Come configurare il gioco

### 1. Aggiungi le tue 20 foto

Metti le foto nella cartella `photos/` con questi nomi esatti:

```
photos/
├── photo_1.jpg
├── photo_2.jpg
├── photo_3.jpg
├── ...
└── photo_20.jpg
```

Sono accettati anche `.jpeg` e `.png`. Se una foto manca, comparirà un placeholder colorato al suo posto.

Le foto verranno mostrate **in ordine**: `photo_1` è la più in basso (la prima che si raccoglie salendo), `photo_20` è la più in alto.

### 2. Aggiungi il video finale

Metti il video nella cartella principale (accanto a `index.html`) con il nome esatto:

```
final_video.mp4
```

Formato consigliato: **MP4 H.264** per massima compatibilità (specie su iPhone/Safari).

### 3. Avvia il gioco

⚠️ **IMPORTANTE:** non aprire `index.html` con doppio click — i browser bloccano il caricamento di immagini/video da `file://`. Devi servirlo da un mini-server locale.

**Opzione A — Server locale rapido (richiede Python installato):**

Apri il terminale nella cartella `poncho_quest_tower/` e lancia:

```bash
python3 -m http.server 8000
```

Poi vai a `http://localhost:8000` dal browser (o dal cellulare connesso alla stessa rete WiFi: usa l'IP del PC, es. `http://192.168.1.50:8000`).

**Opzione B — Pubblicalo online (consigliato per giocare da smartphone):**

Trascina la cartella `poncho_quest_tower/` su uno di questi servizi gratuiti:
- [Netlify Drop](https://app.netlify.com/drop) — drag & drop, link pubblico in 5 secondi
- [Vercel](https://vercel.com)
- [GitHub Pages](https://pages.github.com)

Poi apri il link sul cellulare.

## Controlli

**Da computer:**
- `←` `→` o `A` `D` per muoversi
- `SPAZIO` o `↑` o `W` per saltare
- `SPAZIO` per chiudere la foto e riprendere il gioco
- `SPAZIO` per avviare il video finale dopo la vittoria

**Da smartphone:**
- Pulsanti touch a schermo (frecce in basso a sinistra, salto in basso a destra)
- Tap qualsiasi parte dello schermo per chiudere la foto
- Tap sul pulsante "GUARDA IL VIDEO" alla fine

## Meccaniche di gioco

- **Obiettivo:** scalare la torre evitando di uscire dal bordo inferiore dello schermo (la torre "scende" sempre, accelerando col tempo).
- **Durata:** 2 minuti. Se sopravvivi e raggiungi la cima, vince Simo e parte il video.
- **Foto da raccogliere:** 20, distribuite uniformemente lungo la torre. Quando le tocchi, il gioco va in pausa e ti mostra la foto a schermo intero.
- **Power-up funghetto 🍄** (psichedelico, dura ~6s): cambia i colori dello schermo e aggiunge luci colorate fluttuanti che riducono un po' la visibilità. Effetto solo visivo.
- **Power-up birra analcolica 🍺** (dura ~8s): rallenta del 60% la velocità di discesa della torre. Power-up "buono".
- **Velocità camera:** parte lenta (0.35 px/frame), arriva a 1.8 px/frame negli ultimi secondi. Curva smooth.

## Struttura file

```
poncho_quest_tower/
├── index.html               ← il gioco
├── README.md                ← questo file
├── simo_idle.png            ← sprite ritagliati (già pronti)
├── simo_run_1.png
├── simo_run_2.png
├── simo_run_3.png
├── simo_jump.png
├── simo_fall.png
├── simo_hurt_1.png
├── simo_hurt_2.png
├── photos/
│   └── (metti qui photo_1.jpg ... photo_20.jpg)
└── final_video.mp4          ← (metti qui il video finale)
```

## Risoluzione problemi

- **Vedo solo il placeholder colorato al posto delle foto** → le foto non sono nella cartella `photos/` o hanno un nome diverso da `photo_1.jpg`, `photo_2.jpg`, ecc.
- **Il video non parte** → verifica che `final_video.mp4` sia presente accanto a `index.html` e che sia in formato MP4 H.264. Su iOS, il primo play richiede un'interazione utente (il pulsante "GUARDA IL VIDEO" la fornisce).
- **Su mobile vedo solo i controlli touch a schermo** → corretto, vengono mostrati automaticamente quando il dispositivo è touch.
- **Il personaggio salta troppo o troppo poco** → puoi regolare `CONFIG.jumpVelocity` (default `-10.2`) e `CONFIG.gravity` (default `0.42`) all'inizio del file `index.html`.
- **La torre scende troppo veloce / troppo lenta** → modifica `CONFIG.cameraSpeedStart` e `CONFIG.cameraSpeedEnd`.

## Note tecniche

- Risoluzione virtuale: 360×640 (portrait)
- Sprite scalati a ~70px di altezza in gioco
- Tutta la logica in un singolo file HTML, nessuna dipendenza esterna oltre ai Google Fonts (Press Start 2P + VT323)
- Audio sintetico con Web Audio API (no file audio esterni necessari)
