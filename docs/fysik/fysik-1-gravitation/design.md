# Design: fysik-1-gravitation — "Allt drar i allt"

## Prerequisite-analys

| Koncept | Täcks av | Status |
|---------|----------|--------|
| Materia består av atomer — allt runtomkring oss är gjort av smådelar | `kemi-1-atomer` | klar |
| Massa som "mängd materia" | **Delvis** — kemi-1-atomer visar att atomer har protoner, men "massa" som begrepp introduceras inte explicit. Appen inför massa som brygga i steg 1: "Mer atomer = mer massa = tyngre." Inget eget konceptsteg hoppas över. | Accepterat gap med motivering |

**Beslut:** Designen kan fortsätta. Massa är ett halvsteg från "allt är atomer", inte ett helt konceptsteg.

---

## Visuella variabler

| Variabel | Representerar | Konsekvent i hela modulen? |
|---|---|---|
| Piltjocklek (SVG stroke-width) | Kraft (Newton 3) — alltid lika i bägge riktningar | Ja — i alla steg där pilar visas (3–8) |
| Animationshastighet (bollrörelse) | Rörelseeffekt / acceleration — lättare boll rör sig snabbare | Ja — steg 3, 4, 5 |
| Fartstreck (korta linjer bakom boll) | Signaling för hastighet — förstärker animationshastighet visuellt | Ja — visas när boll rör sig, längre streck = snabbare |
| Bollstorlek + antal atomprickar | Massa | Ja — genom hela modulen |
| Auditory icon: dovhet/tyngd i ljud | Massa — dovare ljud = mer massa | Ja — synkad med slider/massändring |

**Designbeslut:** Pilar representerar kraft, inte acceleration. Lika tjocka åt båda håll oavsett massaskillnad (Newton 3, kvalitativt). Acceleration visas enbart via animationshastighet + fartstreck + förklarande text. Barnet behöver aldrig härleda kopplingen själv — texten förklarar explicit.

---

## Misconceptions (från misconceptions-register.md)

| Misconception | Adresseras i steg | Hur |
|---|---|---|
| "Bara Jorden drar" | 3, 5, 6 | Pilar åt båda håll, Månen drar astronaut |
| "Gravitation kräver luft" | 6 | Månen har ingen luft men drar ändå |
| "Gravitation = magnetism" | — | Skyddas mot: analogi undviks helt |
| "Gravitation bara vid fall" | 3 | Bollar dras kontinuerligt, inte bara vid fall |
| "Tyngre har starkare kraft åt sitt håll" | 4 ⚡ | Prediction-steg → lika pilar → "lättare rör sig mer" |
| "Tyngre faller snabbare" | — | Medvetet utelämnat (se "Vad appen INTE gör") |

---

## Lärandemål

**Eleven ska förstå att allt med massa drar i allt annat (gravitation), och att mer massa ger starkare dragning — inte att bara Jorden drar, och inte att gravitation bara finns när saker faller.**

---

## Målgrupp och enhet

- **Ålder:** 8–9 år
- **Primär enhet:** iPad 13" (surfplatta)
- **Touch targets:** ≥ 80×80 px (drag-and-drop), snap-to-zone
- **Språknivå:** LIX 15–25, max 8–10 ord/mening, max 100–200 ord/skärm

---

## Bryggor

- **Från kemi-1-atomer:** "Du vet att allt är gjort av atomer. Ju fler atomer, desto mer massa. Nu ska du se vad massan gör."
- **Till astro-1-fusion:** Avslutningen visar ett gasmoln som dras ihop av gravitation → teaser: "Vad händer när allt pressas ihop så hårt att det börjar lysa?"

---

## Sessionsstruktur

### Steg 1 — Guided challenge: "Vad händer om du släpper?"

- **Do-komponent:** Barnet drar ett äpple uppåt på skärmen och släpper. Äpplet faller. Sedan drar barnet en fjäder uppåt och släpper. Fjädern faller också (men långsammare pga luftmotstånd-animation). Fråga: "Varför föll båda ner? Tryck på det du tror."
- **Vardagsförankring:** "Du har släppt saker tusen gånger. Allt faller. Men varför?"
- **CRA-nivå:** Konkret (bekanta objekt, direkt manipulation)
- **Layout:** Stor himmel/mark-bakgrund. Objekt (äpple, fjäder) centrerat. Drag-zon i övre halvan, mark i nedre. Tre svarsknappar i botten.
- **Text på skärmen:** "Dra äpplet uppåt och släpp. Vad händer?" → efter fall → "Dra fjädern uppåt och släpp." → efter fall → "Varför föll båda ner?"
- **Svarsalternativ (tap):** (A) "De är tunga" (B) "Jorden drar i dem" (C) "Inget håller upp dem"
- **Interaktionstyp:** Drag-and-drop + tap
- **Feedback vid val:** Inget rätt/fel här — alla svar accepteras med "Bra gissning! Låt oss ta reda på det." (guided challenge, ingen gate-keeping)

### Steg 2 — Massa-intro: "Mer atomer, mer massa"

- **Do-komponent:** Barnet ser två genomskinliga bollar: en liten med få synliga atomer (prickar), en stor med många atomer. Barnet drar varje boll till en våg. Vågen tippar mer för den stora.
- **CRA-nivå:** Konkret → Representationell (atomerna syns som prickar inuti bollen)
- **Layout:** Två bollar överst (vänster: liten/få atomer, höger: stor/många atomer). Våg centrerad i botten. Drag-zon med snap.
- **Text:** "Varje prick är atomer. Vilken boll har mer massa? Dra den till vågen."
- **Interaktionstyp:** Drag-and-drop med snap-to-zone
- **Feedback rätt:** Vågen tippar, mjukt "dunk"-ljud. Text: "Fler atomer = mer massa. Tyngre!"
- **Feedback fel:** Vågen tippar lite. "Den har lite massa. Men den andra har ännu fler atomer. Prova den!"

### Steg 2b — Massa drar från alla håll (nytt mellansteg)

- **Do-komponent:** En ensam stor boll i rymden (rymdbakgrund, inget golv). Rymddamm (små prickar) dras långsamt mot bollen *från alla håll* — ovanifrån, underifrån, från sidorna. Barnet drar en liten sten till olika positioner runt bollen (vänster, höger, ovanför, under) och ser att stenen alltid glider mot bollen oavsett riktning.
- **Vardagsförankring → abstraktion:** Raderar "upp/ner"-paradigmet från steg 1–2 innan ömsesidighet introduceras i steg 3.
- **CRA-nivå:** Konkret → Representationell (rymddamm synliggör dragningen)
- **Layout:** Rymdbakgrund. Stor boll med synliga atomprickar centrerad. Liten sten (dragbar, 80×80 px) som barnet placerar fritt. Rymddamm som partiklar.
- **Text:** "Massa drar. Inte bara nedåt — från alla håll! Dra stenen var du vill."
- **Interaktionstyp:** Drag-and-drop (fritt placera stenen)
- **Feedback:** Stenen glider alltid mot bollen. "Massan drar från alla riktningar. Det finns inget 'ner' i rymden!"

### Steg 3 — Kärnkoncept: "Allt drar i allt"

- **Do-komponent:** Två bollar på en tom yta (inget golv, rymdbakgrund). De dras långsamt mot varandra. Barnet kan dra dem isär, men de glider tillbaka. Pilar visas åt båda håll — boll A drar i B, B drar i A.
- **CRA-nivå:** Representationell (pilar visar kraften)
- **Layout:** Rymdbakgrund. Två bollar (80×80 px) med synliga pilar emellan. Pilarna pulserar svagt.
- **Text:** "Titta! Boll A drar i boll B. Men boll B drar också i boll A. Dra isär dem — vad händer?"
- **Interaktionstyp:** Drag-and-drop (dra isär, de glider tillbaka)
- **Feedback:** Pillarna syns alltid åt båda håll. När barnet drar isär: "De drar i varandra hela tiden. Det kallas gravitation."
- **Nyckeldesign:** Pilar alltid åt BÅDA håll — adresserar direkt missuppfattningen "bara Jorden drar."

### Steg 4 — Mer massa, starkare drag ⚡

- **⚡ Kontraintuitivt moment: Newton 3 — krafterna är lika stora åt båda håll oavsett massaskillnad.**
- **Do-komponent:**
  1. **Predict:** Barnet ser två bollar med olika massa. Fråga: "Om den stora bollen drar i den lilla — vilken pil tror du blir tjockast?" Barnet trycker på en boll.
  2. **Observe:** Slider som ökar massaskillnaden. Pilarna förblir lika tjocka åt båda håll. Men animationen visar att den lättare bollen rör sig snabbare mot den tunga. Fartstreck bakom den lättare bollen. Auditory icon: svisch-ljud vars intensitet matchar hastighet.
  3. **Explain:** "Överraskning! Krafterna är alltid lika stora åt båda håll. Men den lilla bollen är lättare att flytta på — titta, den rör sig mer!" (Text visas exakt samtidigt som animationen — temporal contiguity.)
- **CRA-nivå:** Representationell → Abstrakt (pilarnas tjocklek = kraft, animationshastighet = rörelseeffekt)
- **Layout:** Samma rymdbakgrund. Två bollar centrerade. Slider i botten ("Lägg till massa"). Piltjocklek lika i realtid. Fartstreck bakom snabbare boll.
- **Interaktionstyp:** Tap (prediction) + Slider (stort handtag, 80 px)
- **Feedback:** Pilar lika tjocka, lättare boll rör sig snabbare med fartstreck. Text + animation synkade.
- **Gate-keeping:** Barnet måste (1) göra en prediction, (2) dra slidern till max en gång, (3) se förklaringstexten innan "Nästa" aktiveras.

### Steg 5 — Tillbaka till vardagen: Jorden och äpplet

- **Do-komponent:** Samma pilar-vy, men nu är ena bollen en liten jordglob och andra ett äpple. Pilar lika tjocka åt båda håll (konsekvent med steg 4 — kraft är lika). Animationen visar att äpplet rör sig (faller) medan Jorden står stilla. Fartstreck bakom äpplet. Fråga: "Samma kraft åt båda håll. Varför rör sig bara äpplet?"
- **CRA-nivå:** Representationell (pilar) + koppling tillbaka till konkret (äpplet från steg 1)
- **Layout:** Jordglob (stor, vänster) med synliga atomer. Äpple (litet, höger). Pilar emellan — lika tjocka. Äpplet animeras mot Jorden, Jorden står stilla. Fartstreck bakom äpplet.
- **Svarsalternativ (tap):** (A) "Jorden har så mycket massa att den knappt rör sig" (B) "Äpplet är lättare att flytta på" (C) "Äpplet drar inte alls"
- **Feedback rätt (A eller B):** "Precis! Samma kraft — men Jorden har så enorm massa att den knappt rör sig. Du drar också i Jorden! Men Jorden märker det inte." Jordgloben lyser kort.
- **Feedback fel (C):** "Äpplet drar faktiskt i Jorden — lika mycket! Men Jorden har så enorm massa att den knappt rör sig. Titta på pilarna — lika tjocka!" (Pilar pulserar — signaling.)

### Steg 6 — Månen: gravitation finns överallt

- **Do-komponent:** Barnet ser en astronaut på Månens yta. De drar astronauten uppåt och släpper — astronauten faller tillbaka, men långsammare än på Jorden. Fråga: "Varför faller astronauten tillbaka?"
- **CRA-nivå:** Konkret (bekant bild) + Representationell (pilar visas efter svaret)
- **Layout:** Månlandskap. Astronaut centrerad. Drag uppåt, faller tillbaka.
- **Text:** "Dra astronauten uppåt och släpp."  → efter fall → "Månen har också massa. Månen drar också!"
- **Svarsalternativ (tap):** (A) "Månen har massa och drar" (B) "Det finns luft på Månen" (C) "Rymddräkten är tung"
- **Feedback rätt (A):** "Ja! Månen har massa — mindre än Jorden, men den drar ändå. Gravitation finns överallt där det finns massa."
- **Feedback fel (B):** "Det finns nästan ingen luft på Månen. Men Månen har massa — och allt med massa drar!" Pilar visas.
- **Nyckeldesign:** Adresserar direkt "gravitation kräver luft" och "Månen har ingen gravitation."

### Steg 7 — Fri utforskning: rymdlabbet

- **Do-komponent:** Tre objekt i rymden: stenplanet, gasplanet (stor), måne (liten). Barnet drar en testboll nära varje objekt och ser hur starkt den dras (pilar + hastighet). Barnet kan testa alla kombinationer fritt.
- **CRA-nivå:** Representationell → Abstrakt (barnet förutsäger baserat på massa)
- **Layout:** Rymdbakgrund med tre objekt utspridda. Testboll (dragbar) i mitten. Pilar visas dynamiskt.
- **Text:** "Dra testbollen nära varje planet. Var dras den mest?"
- **Interaktionstyp:** Drag-and-drop, fritt
- **Feedback:** Pilar + dragningshastighet varierar med massa. Inget rätt/fel — utforskande.

### Steg 8 — Konsolidering: "Vad lärde du dig?"

- **Do-komponent:** Återkoppling till steg 1. Samma äpple, samma fråga: "Varför faller äpplet?" Men nu med pilar och massa-kunskap.
- **CRA-nivå:** Abstrakt (barnet formulerar principen)
- **Layout:** Samma äpple + mark som steg 1, men nu med synliga pilar.
- **Svarsalternativ (tap):** (A) "Äpplet och Jorden drar i varandra lika mycket. Men Jorden är så tung att bara äpplet rör sig." (B) "Äpplet är tungt" (C) "Inget håller upp det"
- **Feedback rätt (A):** Pilar visas (lika tjocka åt båda håll) + fartstreck bakom äpplet + fireworks-animation. "Du förstår gravitation! Allt med massa drar i allt annat — lika mycket åt båda håll!"
- **Feedback fel (B/C):** Pilar visas (triggas *innan* texten) + pilar pulserar. "Titta på pilarna — de pekar åt båda håll, lika tjocka! Jorden och äpplet drar lika mycket. Men äpplet är lättare, så det rör sig mest." (State-feedback sync: pilar synliga och signalerade före texten.)
- **Reflektionsfråga (visuellt val):** "Vad var mest förvånande?" — tre bildkort: (1) Äpplet drar i Jorden (2) Månen har gravitation (3) Allt drar i allt. Barnet trycker på ett kort, kort animation.
- **Teaser till astro-1-fusion:** Animerat gasmoln som dras ihop av pilar. Text: "Gravitation drar ihop gasmolnet. Vad händer när det pressas ihop tillräckligt? Det tar vi nästa gång!"

---

## Scaffolding-nivåer

Gäller steg 2, 4, 5, 6 (ej steg 1 — guided challenge, ej steg 2b/3/7 — utforskande):

- **Fel 1:** Pilar blinkar kort mot rätt svar. Ingen text.
- **Fel 2:** Text-ledtråd: "Titta på pilarna. Vilken är tjockast?" / "Titta på atomerna inuti. Vilken har flest?"
- **Fel 3 (full scaffold):** Rätt svar markeras grönt + förklaring: "Jorden har miljontals gånger fler atomer. Därför drar den så mycket starkare."

---

## Gate-keeping

- **Steg 2:** Barnet måste dra rätt boll till vågen (eller korrigeras via scaffold).
- **Steg 4:** Barnet måste dra slidern till max minst en gång.
- **Steg 5:** Barnet måste svara rätt (med scaffold vid behov).
- **Steg 6:** Barnet måste svara rätt (med scaffold vid behov).
- **Steg 1, 3, 7:** Ingen gate-keeping (utforskande).

---

## Metakognition

- **Framstegsindikator:** Horisontell "rymdresa"-karta i toppen — 8 planeter/punkter, aktuellt steg lyser. Inte poäng.
- **Lärandemål:** Steg 1 visar riktning: "Idag ska du upptäcka varför saker faller." Steg 8 visar full återkoppling: "Nu vet du: allt med massa drar i allt annat!"

---

## Responsivt beteende

- **Mobil (8"):** Sekventiell layout. Bollar ovanför varandra istället för sida vid sida. Slider i fullbredd. Pilar enklare (bara tjocklek, ingen puls-animation). En interaktion per vy.
- **Surfplatta (13"):** Baslayout som beskrivet ovan. Bollar sida vid sida. Pilar med puls.
- **Laptop (16"):** Simultant CRA — atom-prickar syns inuti bollarna hela tiden. Hover-states på objekt visar massa-info. Steg 7 rymdlabb kan visa kraftvärde som siffra bredvid pilarna.

---

## Auditory icons

- **Drag-and-drop:** Mjukt "lyft"-ljud vid pickup (kort, luftigt)
- **Boll faller / äpple faller:** Dov "dunk" (kort, lågfrekvent)
- **Rätt svar:** Mjukt stigande "pling" (två toner uppåt)
- **Fel svar:** Kort dovt "bonk" (neutralt, inte straffande)
- **Pilar visas:** Svagt vibrerande "hmm"-ljud (representerar dragning)
- **Progression:** Kort "swoosh" vid stegbyte
- **Fireworks (steg 8):** Tre snabba poppljud

---

## Tekniska beslut

- **Vanilla JS** — appen har linjär progression med enkel state (aktuellt steg + scaffold-nivå). Ingen komplex state-trädstruktur som motiverar React.
- **Animationer:**
  - Äpple/fjäder-fall (steg 1, 6): CSS transition + JS timing
  - Pilar som pulserar (steg 3–7): CSS animation (pulse opacity)
  - Piltjocklek som svarar på slider (steg 4): JS realtidsuppdatering av SVG stroke-width
  - Bollar som glider mot varandra (steg 3): requestAnimationFrame
  - Fireworks (steg 8): canvas-partiklar eller CSS keyframes
  - Gasmoln-teaser (steg 8): CSS scale-animation
- **Rörliga targets:** Nej. Bollarna i steg 3 glider men är ej interaktionsmål under rörelse — barnet drar dem när de står stilla.
- **SVG för pilar** — stroke-width styrs dynamiskt för att visa kraftstyrka.
- **`prefers-reduced-motion`:** Pulsanimationer, fireworks och gasmoln-teaser avstängs. Fall-animationer förkortas. Pilar visas statiskt.

---

## Stealth assessment

| Datapunkt | Steg | Indikerar |
|---|---|---|
| Prediction choice i steg 4 (vilken boll barnet tror har tjockast pil) | 4 | Bär barnet på "tyngre = starkare kraft åt sitt håll"? |
| Dwell time efter surprise (sekunder innan "Nästa" efter att lika pilar visats) | 4 | Längre paus = kognitiv bearbetning av anomali |
| Systematisk parameterändring (drar slider extremt + pausar vs. sveper oavbrutet) | 4, 7 | Hypotesprövning vs. slumpmässigt utforskande |
| Aktiv placering av testboll (strategiskt nära tung planet vs. slumpmässigt) | 7 | Applicerad förståelse för massa → dragning |
| Korrekt svar steg 8 utan scaffold | 8 | Konceptuell förståelse etablerad |

---

## Developmental progression-check

| Steg → Steg | Nytt koncept | Brygga | OK? |
|---|---|---|---|
| 1 → 2 | Massa som "mängd materia" | "Varje prick är atomer. Fler atomer = mer massa." | Ja |
| 2 → 2b | Massa drar i alla riktningar, inte bara "ner" | Rymdbakgrund, inget golv, rymddamm från alla håll | **Nytt steg (insatt efter NLM-granskning)** |
| 2b → 3 | Ömsesidighet — båda drar i varandra | Från "en boll drar damm" till "två bollar drar varandra" | Ja |
| 3 → 4 | Newton 3 — lika kraft, olika rörelse | Prediction-steg, explicit förklaring | Ja (⚡ prediction) |
| 4 → 5 | Tillbaka till vardag — Jorden + äpple | Samma pilsemantik, konkret koppling | Ja |
| 5 → 6 | Generalisering — gravitation på Månen | Bekant bild (astronaut), samma logik | Ja |
| 6 → 7 | Fri utforskning | Applicera allt, inga nya koncept | Ja |
| 7 → 8 | Konsolidering | Återkoppling till steg 1 | Ja |

---

## Vad appen INTE gör

1. **Förklarar inte fallhastighet.** "Tunga saker faller snabbare" är den segaste misconceptionen — appen undviker medvetet att jämföra fallhastighet. Steg 1 visar att fjädern faller långsammare, men förklarar det inte (luftmotstånd är ett eget koncept för senare).
2. **Nämner inte "neråt" som absolut riktning.** Gravitation drar mot centrum, men det kräver förståelse av klotformen. Appen säger "mot Jorden" utan att definiera riktning.
3. **Använder inte magnet-analogin.** Magnetism är selektiv (bara vissa material) — analogin skapar en felaktig mental modell som är svår att rätta.
4. **Introducerar inte gravitationskonstanten eller formler.** Abstrakt matematik kommer långt senare. Appen stannar vid "mer massa = starkare drag" som kvalitativ princip.
5. **Medvetet utelämnat nästa steg:** Avståndets roll (gravitationen avtar med avstånd²). Det kräver proportionellt tänkande som 8–9-åringar inte har. Nämns inte alls för att undvika half-förklaringar. Är lämpligt för 11–12 år.
