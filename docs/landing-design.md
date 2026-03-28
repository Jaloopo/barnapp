# Design: Kunskapskarta — Landningssida

**Fil:** `docs/index.html` (ersätt befintlig)
**Typ:** Landningssida, inte lärapp — inget entry i index.yaml
**Målgrupp:** Barn 8–9 (primär) + vuxna (sekundär)

---

## Syfte

Landningssidan ska vara en visuell kunskapskarta som visar:
1. **Startpunkt** — var börjar man (kemi-1-atomer)
2. **Lärvägar** — hur apparna hänger ihop via prerequisites/unlocks
3. **Status** — vad som är klart, byggt, och vad som kommer

Inspiration: skill trees i spel, men utan gamification-poäng.

---

## Data

All data ligger inline i JavaScript (ingen build-step, ingen fetch).
Strukturen speglar `index.yaml` så att uppdateringar är enkla.

```javascript
const appar = [
  {
    id: 'kemi-1-atomer',
    titel: 'Atomer',
    desc: 'Protoner bestämmer ämnet',
    ämne: 'kemi',
    icon: '⚛',
    status: 'klar',        // klar | byggd | design | kommande
    href: 'kemi/kemi-1-atomer/',
    prerequisites: [],
    unlocks: ['kemi-2-molekyler', 'el-1-ledare', 'astro-1-fusion'],
    x: 0.5, y: 0.08        // relativ position (0–1), se Layout nedan
  },
  // ... en entry per app i index.yaml
];
```

**Viktigt:** När en ny app läggs till i index.yaml ska den också läggas till i denna array. Positionen (x, y) sätts manuellt för att ge en bra visuell layout.

---

## Layout — Nodpositioner

Kartan ritas i ett responsivt SVG/canvas-liknande koordinatsystem.
Relativa koordinater (0–1) mappas till faktisk storlek via JavaScript.

```
            [Atomer]              y ≈ 0.08
           /    |    \
          /     |     \
   [Molekyler] [Ledare] [Fusion]  y ≈ 0.38
       |         |         |
  [Blandningar] [Kretsar] [Livscykel]  y ≈ 0.68
```

x-positioner (ungefär):
- Atomer: 0.5 (centrerad)
- Molekyler: 0.18, Ledare: 0.5, Fusion: 0.82
- Blandningar: 0.18, Kretsar: 0.5, Livscykel: 0.82

Dessa är startvärden. Justera vid behov för att undvika överlapp.

**Framtida noder** (finns ej i index.yaml ännu, men visa som "kommande"):
- kemi-3-blandningar (under molekyler)
- astro-2-livscykel (under fusion)

Dessa visas som låsta/gråa noder med texten "Kommer snart" så att barnet ser att kartan växer.

**Gravitation (planerad):** Om fysik-1-gravitation läggs till som prerequisite för astro-1-fusion, placeras den som en ny nod med `y ≈ 0.38` och en x-position mellan ledare och fusion. Layouten tål detta utan redesign — man lägger bara till en ny entry med x/y-koordinater och en prerequisite-linje.

---

## Visuell design

### Färgpalett (behåll från nuvarande sida)
- Kemi: grön (`#66bb6a`, bg `#e8f5e9`)
- El: gul (`#ffc107`, bg `#fff8e1`)
- Astro: lila (`#9575cd`, bg `#ede7f6`)
- Fysik (framtida): blå (`#42a5f5`, bg `#e3f2fd`)

### Noder
Varje app är en **rektangulär nod med rundade hörn** (inte cirkel — mer plats för text).

- **Storlek:** ca 140×80 px desktop, 110×65 px mobil
- **Innehåll:** Icon (emoji) + titel (1–2 ord) + liten statusindikator
- **Touch target:** Hela noden är klickbar, minst 60×60 px (WCAG + barn)

**Visuella states:**

| Status | Bakgrund | Ram | Opacity | Interaktion |
|--------|----------|-----|---------|-------------|
| klar | Ämnesfärg (mättad) | 2px solid mörkare nyans | 1.0 | Klickbar, länk till app |
| byggd | Ämnesfärg (ljus) | 2px solid ämnesfärg | 1.0 | Klickbar, länk till app |
| design | Vit | 2px dashed ämnesfärg | 0.8 | Klickbar men markerad "beta" |
| kommande | Ljusgrå (`#f0f0f0`) | 1px solid `#ddd` | 0.5 | Ej klickbar, text "Kommer snart" |

**Klar-markering:** En liten bock-ikon (checkmark) i hörnet av klara appar. Ingen stjärna, inga poäng.

### "Börja här"-markering
Kemi-1-atomer (den enda appen utan prerequisites) får:
- En pulsande ring runt noden (CSS animation, respekterar `prefers-reduced-motion`)
- Texten "Börja här!" ovanför noden i en liten pratbubbla/badge
- Denna markering visas alltid, oavsett status

### Linjer (prerequisites → unlocks)
- **Typ:** Raka eller svagt böjda linjer (SVG `<line>` eller `<path>`)
- **Riktning:** Uppifrån ner (prerequisite → unlock). Ingen pilspets behövs — riktningen är implicit (uppifrån ner = framsteg)
- **Färg:** Linjerna färgas efter det ämne de leder TILL (unlock-nodens ämne)
- **Status:** Linjer till kommande/låsta noder är streckade och blekare
- **Bredd:** 2–3 px

### Rubrik och intro
- **H1:** "Barnappen" (som idag)
- **Undertitel:** "Utforska naturvetenskap — välj din väg!" (kort, uppmuntrande)
- Placeras ovanför kartan

### Legend (valfritt, nere)
En liten förklaring under kartan:
- Fylld cirkel + "Klar" / Ljus cirkel + "Redo att testa" / Grå + "Kommer snart"
- Ska vara diskret, inte ta fokus

---

## Teknisk implementation

### Struktur: HTML + inline SVG + CSS + JS

```
<!DOCTYPE html>
<html lang="sv">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Barnappen — Kunskapskarta</title>
  <style>/* all CSS inline */</style>
</head>
<body>
  <h1>Barnappen</h1>
  <p class="subtitle">...</p>

  <div class="map-container">
    <svg class="map-lines" aria-hidden="true">
      <!-- Linjer ritas här av JS -->
    </svg>
    <div class="map-nodes">
      <!-- Noder (HTML-element) positioneras här av JS -->
    </div>
  </div>

  <div class="legend">...</div>

  <script>/* all JS inline */</script>
</body>
</html>
```

### Hur det funkar

1. **Data-arrayen** definieras i JS (se Data ovan)
2. **Noder** skapas som HTML-element (`<a>` för klickbara, `<div>` för kommande) och positioneras med `position: absolute` + `left/top` i procent baserat på x/y
3. **Linjer** ritas i SVG-lagret under noderna. JS räknar ut start/slut-koordinater från nodernas positioner
4. **Responsivitet:** `map-container` har en fast aspect ratio (t.ex. 3:4 på mobil, 16:10 på desktop). Koordinaterna är relativa (0–1) så allt skalas automatiskt
5. **Resize:** `ResizeObserver` eller `window.resize` räknar om linjepositioner vid storleksändring

### Container-dimensioner

```css
.map-container {
  position: relative;
  width: 100%;
  max-width: 800px;
  /* Höjden beror på antal rader i grafen */
  aspect-ratio: 4 / 3;   /* Bra startpunkt, justera vid behov */
}

.map-lines {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
}

.map-nodes {
  position: absolute;
  inset: 0;
}
```

### Nod-HTML (genereras av JS)

```html
<a class="node kemi status-klar" href="kemi/kemi-1-atomer/"
   style="left: 50%; top: 8%;">
  <span class="node-icon">⚛</span>
  <span class="node-title">Atomer</span>
  <span class="node-check" aria-label="Klar">✓</span>
</a>
```

Notera `transform: translate(-50%, -50%)` på `.node` så att x/y pekar på nodens centrum.

### Touch och interaktion

- **Pointer Events** (inte mouse events) — fungerar touch + mus + penna
- **Hover (desktop):** Noden lyfts subtilt (`translateY(-2px)` + skugga) — behåll från nuvarande design
- **Focus:** Tydlig fokusring för tangentbordsnavigering
- `prefers-reduced-motion`: Stäng av pulsanimation på "Börja här", ta bort hover-transform

### Tillgänglighet

- SVG-linjer: `aria-hidden="true"` (dekorativa)
- Noder: semantiska `<a>`-taggar med beskrivande text
- Kommande noder: `<div>` utan länk, `aria-disabled="true"`
- Kontrast: Alla texter ska klara WCAG AA
- Tangentbordsordning: Tabba genom noderna i logisk ordning (uppifrån ner, vänster till höger)

---

## Responsivitet

| Bredd | Beteende |
|-------|----------|
| < 480px | Noderna krymps (110×65), fontstorlek minskas. Kartan kan få `aspect-ratio: 3/4` (mer vertikal). Om det blir för trångt: stacka noder vertikalt inom varje rad med mer y-spacing |
| 480–800px | Standardlayout |
| > 800px | `max-width: 800px`, centrerad |

---

## Vad sidan INTE gör

- Ingen gamification (inga poäng, inga stjärnor, ingen XP-bar)
- Ingen progress-tracking via localStorage (framtida möjlighet, men inte nu)
- Inget interaktivt — sidan är navigation, inte en lärapp
- Inga externa beroenden (inga bibliotek, inga fonter via CDN)
- Ingen animation förutom subtil "Börja här"-puls och hover-effekter

---

## Byggordning för Sonnet

> Instruktion: `bygg docs/landing-design.md`
> Målfil: `docs/index.html` (ersätt hela befintliga filen)

Eftersom detta ersätter en befintlig fil och inte är en lärapp med steg,
anpassa byggordningen:

1. **Write** — Skriv grundstruktur (~120 rader): DOCTYPE, head, CSS-variabler, body med h1/subtitle, tom `map-container` med SVG + nodes-div, och ett JS-skelett med data-arrayen + tom `render()`-funktion. Inga noder renderade än.

2. **Edit** — Implementera `render()`: skapa nod-element från data, positionera dem, sätt rätt klasser/states, gör klara/byggda klickbara.

3. **Edit** — Implementera `drawLines()`: rita SVG-linjer mellan prerequisite-noder. Lägg till `ResizeObserver` för omritning.

4. **Edit** — Lägg till all CSS: nod-styling per status, ämnesfärger, hover/focus, "Börja här"-puls, legend, responsiva breakpoints.

5. **Edit** — Finslipa: `prefers-reduced-motion`, tabindex-ordning, aria-attribut, legend-sektion.

6. Self-check mot denna design.

### Self-check

- [ ] Alla appar från index.yaml finns med (5 st) + 2 kommande
- [ ] Linjer visar prerequisites → unlocks korrekt
- [ ] Kemi-1-atomer har "Börja här"-markering
- [ ] Klara appar har bock-ikon
- [ ] Kommande appar är gråa och ej klickbara
- [ ] Touch targets ≥ 60×60 px
- [ ] `prefers-reduced-motion` hanteras
- [ ] Fungerar på 360px bred skärm
- [ ] Inga externa beroenden
- [ ] Pointer Events, inte mouse events
- [ ] Tangentbordsnavigering fungerar
- [ ] astro-1-fusion visar status "byggd" (inte "design" som buggen idag)
