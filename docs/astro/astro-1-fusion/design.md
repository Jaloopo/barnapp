# Design: Stjärnköket — fusion i stjärnor

## Lärandemål

Eleven ska förstå att stjärnor lyser för att vätekärnor pressas ihop till heliumkärnor av den extrema hettan i stjärnans inre, och att denna process (fusion) frigör energi i form av ljus och värme — inte för att stjärnor "brinner" som eld.

## Målgrupp och enhet

- Ålder: 8–9 år
- Primär enhet: iPad 13–14"
- Touch target: ≥ 80×80 px (drag-and-drop)
- Språknivå: LIX 15–25, max 8–10 ord/mening, max 100–200 ord/skärm

## Prerequisites

- **kemi-1-atomer** (protoner bestämmer ämnet) — barnet vet att väte har 1 proton, helium har 2
- **kemi-2-molekyler** (atomer binder ihop sig) — barnet vet att atomer kan slå sig samman

## Sessionsstruktur

### Steg 1 — Varför är solen så het? (Guided challenge)

- **Do-komponent:** Barnet ser en sol/stjärna och tre alternativ: "Eld 🔥", "Elektricitet ⚡", "Något annat 🤔". Barnet tappar på sitt val. (Constructive — förutsägelse)
- **CRA-nivå:** Konkret
- **Layout:** Stor sol centrerad i övre halvan. Tre valknappar (80×80 px) i rad under solen. Text ovanför knapparna.
- **Text:** "Solen är vår närmaste stjärna. Den är otroligt het. Vad tror du gör den så het?"
- **Interaktion:** Tap på ett av tre val
- **Feedback vid val:** Alla val accepteras utan rätt/fel. Svaret sparas och visas igen i steg 6. Kort bekräftelse: "Spännande tanke! Låt oss ta reda på det."
- **Vardagsförankring:** Solen som barnet känner — den värmer, den lyser, den finns varje dag.

**Missuppfattning som aktivt bemöts:** "Solen brinner som eld" — den vanligaste feltolkningen. Appen adresserar detta explicit i steg 3.

### Steg 2 — Zooma in i stjärnan

- **Do-komponent:** Barnet "zoomar in" i solen genom pinch-to-zoom-gest (eller tap på en förstoringsikon). Tre zoom-nivåer: sol utifrån → solens yta → solens kärna full av vätekärnor. (Constructive — utforskning)
- **CRA-nivå:** Konkret → Representationell
- **Layout:** Stor cirkel (solen) centrerad. Förstoringsglas-ikon nere till höger. Vid varje zoom ändras vyn med animerad övergång. I sista zoom-nivån: massa små cirklar (vätekärnor, märkta "H") som studsar runt snabbt i ett hett rött/orange fält.
- **Text per zoom-nivå:**
  1. "Det här är solen. Tryck på förstoringsglaset!"
  2. "Solens yta. Hett! Men vi måste längre in."
  3. "Solens kärna! Här inne är det 15 miljoner grader. Vätekärnorna rusar runt jättesnabbt."
- **Interaktion:** Tap (förstoringsglas) × 3
- **Feedback:** Varje zoom ger en kort "whoosh"-animation + temperaturindikator som ökar (visuell, ej siffror — färg går från gul → orange → djupröd)

**Pre-training:** Barnet ser att kärnan är full av vätekärnor (H) — detta förbereder steg 3.

### Steg 3 — Hettan pressar ihop (kärnkonceptet)

- **Do-komponent:** Barnet ser fyra vätekärnor (H, 1 proton vardera, visade som ljusblå cirklar med "H" och en liten proton-prick). Barnet ska dra och pressa ihop dem till mitten mot ett motstånd (embodied cognition — "pressa"-gesten). När alla fyra möts i centrum: flash + energivåg → en heliumkärna (He, 2 protoner) dyker upp. (Constructive — barnet bygger helium)
- **CRA-nivå:** Konkret (drag-and-drop) + Representationell (atomsymboler)
- **Layout:** Fyra H-cirklar (80×80 px) placerade i fyra hörn. Central zon markerad med pulsande glöd ("Presszon"). Under: kort text.
- **Text:** "Hettan inne i stjärnan pressar ihop vätekärnorna. Dra dem till mitten!"
- **Interaktion:** Drag-and-drop med motstånd (haptic-känsla via animation — cirklarna "kämpar emot" och går sakta, som att trycka ihop magneter). Pointer Events.
- **Feedback vid ihoppressning:**
  - Progressiv: varje H som når zonen ger en liten "tick"-ljud och glöder
  - Vid 4/4: stor ljusblixt (vit → gul), energi-tryckvåg som sprider sig utåt, "BOOM-pling"-ljud. Texten ändras till: "Fyra vätekärnor blev en heliumkärna! Energi frigjordes — ljus och värme!"
  - Den nya He-kärnan visas som en större cirkel, guldfärgad, med "He" och 2 proton-prickar
- **Scaffold om barnet inte drar:**
  - Fel 1 (5 sek): En H-kärna pulserar/glöder
  - Fel 2 (10 sek): Pil från en H-kärna mot centrum
  - Fel 3 (15 sek): En H-kärna dras automatiskt halvvägs mot mitten, barnet tar över

**Visuell "energi-spark":** Innan atomerna snäpper ihop visas en kort gnist-animation i presszonen — ger korrekt intuition att energi behövs för att starta processen (utan att förklara aktiveringsenergi).

**Koppling till kemi-1:** "Kommer du ihåg? Väte har 1 proton. Helium har 2. Du ändrade just antalet protoner — och skapade ett nytt ämne!"

### Steg 4 — Det är inte eld! (Missuppfattning)

- **Do-komponent:** Barnet ser två bilder sida vid sida: "Eld i en brasa" och "Solen". Under varje bild: "Behöver syre? Ja/Nej". Barnet tappar på rätt svar för varje bild. (Constructive — jämförelse/kontrast)
- **CRA-nivå:** Representationell
- **Layout:** Två kort (280×200 px) sida vid sida. Brasa till vänster, sol till höger. Under varje kort: två knappar "Ja" / "Nej" (80×44 px).
- **Text ovan:** "Eld behöver syre för att brinna. Behöver solen syre?"
- **Interaktion:** Tap × 2 (ett val per bild)
- **Feedback:**
  - Brasa + Ja: grön bock + "Rätt! Eld behöver syre."
  - Sol + Nej: grön bock + ljusblixt + "Rätt! Solen har inget syre. Den lyser inte av eld — den lyser av fusion!"
  - Sol + Ja (fel): mjuk orange markering + "Hmm, det finns nästan inget syre i rymden. Solen använder något annat! Tryck på Nej."
- **Gate-keeping:** Barnet måste svara rätt på båda innan vidare.

### Steg 5 — Stjärnfabriken (fri utforskning)

- **Do-komponent:** Barnet har en pool av vätekärnor och kan pressa ihop dem upprepade gånger. Varje lyckad fusion ger ljus-energi som samlas i en "stjärnmätare". Barnet ser stjärnan lysa starkare för varje fusion. (Constructive — upprepat byggande)
- **CRA-nivå:** Representationell → Abstrakt (mätare visar ackumulerad energi)
- **Layout:** Vänster sida: pool av H-kärnor. Center: presszon (samma som steg 3). Höger sida: en stjärna som växer i ljusstyrka. Under stjärnan: en enkel mätare "Energi" som fylls.
- **Text:** "Stjärnan gör detta miljontals miljarder gånger! Pressa ihop fler vätekärnor och se stjärnan lysa."
- **Interaktion:** Samma drag-and-drop som steg 3, men snabbare (mindre motstånd — expertise reversal). Kan göras 3–5 gånger.
- **Feedback:** Varje fusion → ljusblixt (mindre än steg 3, snabbare), stjärnan lyser starkare, mätare fylls. Vid full mätare: "Stjärnan lyser för fullt!"
- **Ingen gate-keeping** — detta är fri utforskning.

### Steg 6 — Vad lärde du dig? (Konsolidering)

- **Do-komponent:** Återkoppling till steg 1. Barnet ser sitt ursprungliga svar. Sedan: "Nu vet du mer! Vad gör solen het?" med tre nya val: "Eld 🔥", "Fusion — väte pressas ihop till helium ⚛️", "Elektricitet ⚡". (Constructive — reflektiv jämförelse)
- **CRA-nivå:** Abstrakt
- **Layout:** Övre halva: kort som visar barnets svar från steg 1 ("Du gissade: [X]"). Under: tre valknappar.
- **Text:** "I steg 1 trodde du att solen är het på grund av [X]. Vad tror du nu?"
- **Interaktion:** Tap
- **Feedback vid "Fusion":** Stor animation — stjärnan pulsar, konfetti av ljuspartiklar + triumfljud. Text: "Precis! Hettan inne i stjärnan pressar ihop vätekärnor till heliumkärnor. Det frigör energi — ljus och värme. Det kallas fusion!"
- **Feedback vid fel:** Mjuk ledtråd: "Kommer du ihåg vad du gjorde i steg 3? Du pressade ihop vätekärnor..." → nytt försök.
- **Avslutning:** "Solen är vår närmaste stjärna. Den har gjort fusion i 4,5 miljarder år! Fråga en vuxen: vad tror du händer när vätet tar slut?"

## Scaffolding-nivåer (globalt)

- **Fel 1:** Visuell markering — rätt element pulserar/glöder
- **Fel 2:** Delvis ledtråd — text + pil som visar riktning
- **Fel 3:** Fullständig scaffold — animation visar halva lösningen, barnet slutför

## Gate-keeping

- **Steg 3:** Barnet måste pressa ihop alla 4 H till He (dock fritt antal försök, inget "fel" möjligt — bara ogjort)
- **Steg 4:** Båda frågorna måste besvaras rätt
- **Steg 6:** Rätt svar krävs (med scaffold)
- **Steg 1, 2, 5:** Ingen gate-keeping

## Metakognition

- **Framsteg:** 6 cirklar i en rad högst upp (som kemi-2-molekyler), fylls progressivt. Ingen poäng.
- **Lärandemål:** Steg 1 antyder riktningen ("Vad gör solen het?"). Steg 6 ger full återkoppling.

## Responsivt beteende

- **Mobil (8"):** Steg 4: bilderna staplas vertikalt istället för sida vid sida. Steg 5: presszon och stjärnmätare staplas. Zoom i steg 2 via tap (ej pinch).
- **Surfplatta (13–14"):** Baslayout som beskrivet ovan.
- **Laptop (16"):** Steg 3 och 5: visa en mini-stjärna i hörnet som reagerar i realtid på fusionen. Steg 2: hover-effekt på förstoringsglaset.

## Auditory icons

| Händelse | Ljud |
|----------|------|
| Zoom (steg 2) | Mjukt "whoosh" — fallande ton |
| H-kärna når presszon | Kort "tick" — hög, skarp |
| Fusion lyckas | Kraftig "boom-pling" — bas + klocka |
| Energivåg | Snabbt svepande "swish" |
| Rätt svar (steg 4, 6) | Mjukt "pling" — stigande |
| Fel svar | Dovt "bonk" — kort, ej straffande |
| Steg-progression | Litet "pop" |

## Tekniska beslut

- **React via CDN** — komplex state (sparar steg 1-svar, drag-motstånd, stjärn-ljusstyrka, mätare). Samma approach som kemi-1-atomer och el-apparna.
- **Animationer:**
  - Zoom-transition (scale + fade, 400ms)
  - Drag-motstånd (CSS transform med spring-easing via JS)
  - Ljusblixt vid fusion (radial gradient, opacity 0→1→0, 600ms)
  - Energi-tryckvåg (expanderande cirkel, 800ms)
  - Stjärnans glöd (CSS box-shadow, stegvis ökning)
  - Konfetti-partiklar i steg 6 (canvas eller CSS-animation)
- **Rörliga targets:** Nej — H-kärnorna är statiska i sina startpositioner, barnet drar dem.
- **Pointer Events** för all drag-and-drop (ej mouse events)
- **prefers-reduced-motion:** Alla animationer byts till instant transitions
- **Web Audio API** för alla ljud

## Vad appen INTE gör

1. **Deuterium och He-3 som mellansteg** — den verkliga pp-kedjan har flera delsteg. Vi förenklar till "4 H → 1 He + energi" vilket är korrekt som nettoformel (Britannica-bekräftat). Mellanstegen sparas till en framtida fördjupningsapp.

2. **Neutriner, positroner, gammastrålning** — subatomära partiklar som frigörs vid fusion utelämnas helt. Kräver antimateria-förståelse som ligger långt utanför åldersgruppen.

3. **Kvantmekanisk tunnling** — den egentliga mekanismen som gör fusion möjlig trots elektrisk repulsion. Kontraintuitivt och kräver vågfunktionsförståelse. Vi visar "motstånd" i drag-gesten som en korrekt-riktad analogi.

4. **E=mc² och massdefekt** — vi visar att energi frigörs men förklarar inte varför (att massa "försvinner"). Formeln sparas till 10–12 år. Steg 6-texten antyder idén ("energi i form av ljus och värme") utan att nämna massa.

5. **Stjärnans livscykel** — vad som händer när vätet tar slut (röd jätte, nebulosa, vit dvärg). Naturligt nästa steg i en framtida app (astro-2-livscykel). Steg 6 planterar frågan: "Vad händer när vätet tar slut?"

**Medveten förenkling — "tryck" vs "hetta":** Perplexity-research visar att trycket (gravitation) håller ihop stjärnan, men det är *hettan* som ger vätekärnorna tillräcklig energi att övervinna repulsionen. Appen betonar "hettan" som primär drivkraft i text, och använder drag-motståndet som metafor för repulsion — inte för tryck. Formuleringen "Hettan inne i stjärnan pressar ihop vätekärnorna" är en medveten förenkling som är korrekt i riktning om än inte fullständig.
