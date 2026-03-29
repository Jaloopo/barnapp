# Design: fysik-1-gravitation — "Allt drar i allt"

## Prerequisite-analys

| Koncept | Täcks av | Status |
|---------|----------|--------|
| Materia består av atomer — allt runtomkring oss är gjort av smådelar | `kemi-1-atomer` | klar |
| Massa som "mängd materia" | **Delvis** — kemi-1-atomer visar att atomer har protoner, men "massa" som begrepp introduceras inte explicit. Appen inför massa som brygga i steg 1: "Mer atomer = mer massa = tyngre." Inget eget konceptsteg hoppas över. | Accepterat gap med motivering |

**Beslut:** Designen kan fortsätta. Massa är ett halvsteg från "allt är atomer", inte ett helt konceptsteg.

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

### Steg 3 — Kärnkoncept: "Allt drar i allt"

- **Do-komponent:** Två bollar på en tom yta (inget golv, rymdbakgrund). De dras långsamt mot varandra. Barnet kan dra dem isär, men de glider tillbaka. Pilar visas åt båda håll — boll A drar i B, B drar i A.
- **CRA-nivå:** Representationell (pilar visar kraften)
- **Layout:** Rymdbakgrund. Två bollar (80×80 px) med synliga pilar emellan. Pilarna pulserar svagt.
- **Text:** "Titta! Boll A drar i boll B. Men boll B drar också i boll A. Dra isär dem — vad händer?"
- **Interaktionstyp:** Drag-and-drop (dra isär, de glider tillbaka)
- **Feedback:** Pillarna syns alltid åt båda håll. När barnet drar isär: "De drar i varandra hela tiden. Det kallas gravitation."
- **Nyckeldesign:** Pilar alltid åt BÅDA håll — adresserar direkt missuppfattningen "bara Jorden drar."

### Steg 4 — Mer massa, starkare drag

- **Do-komponent:** Barnet har en slider som gör en av bollarna större (fler atomer syns inuti). Pilarna ändrar tjocklek: större boll = tjockare pilar åt båda håll. Barnet experimenterar fritt.
- **CRA-nivå:** Representationell → Abstrakt (pilarnas tjocklek = kraftens styrka)
- **Layout:** Samma rymdbakgrund. Två bollar centrerade. Slider i botten ("Lägg till massa"). Piltjocklek uppdateras i realtid.
- **Text:** "Dra reglaget. Vad händer med dragningen när bollen får mer massa?"
- **Interaktionstyp:** Slider (stort handtag, 80 px)
- **Feedback:** Pilarna tjocknar synligt. Text efter utforskning: "Mer massa = starkare dragning. Alla drar mer!"
- **Gate-keeping:** Barnet måste dra slidern till max en gång och observera pilarna innan "Nästa" aktiveras.

### Steg 5 — Tillbaka till vardagen: Jorden och äpplet

- **Do-komponent:** Samma pilar-vy, men nu är ena bollen en liten jordglob och andra ett äpple. Pilar åt båda håll — men pilen från Jorden är ENORMT mycket tjockare. Fråga: "Äpplet drar också i Jorden. Varför märker vi det inte?"
- **CRA-nivå:** Representationell (pilar) + koppling tillbaka till konkret (äpplet från steg 1)
- **Layout:** Jordglob (stor, vänster) med synliga atomer. Äpple (litet, höger). Pilar emellan — Jordens pil dominant.
- **Svarsalternativ (tap):** (A) "Jorden har så mycket mer massa" (B) "Äpplet är för litet" (C) "Äpplet drar inte alls"
- **Feedback rätt (A):** "Precis! Jorden har enormt mycket mer massa. Därför märker vi bara Jordens drag." Jordgloben lyser kort.
- **Feedback fel (C):** "Äpplet drar faktiskt i Jorden! Men Jordens massa är så stor att Jorden knappt rör sig. Titta på pilarna."
- **Feedback fel (B):** "Nästan! Äpplet drar lite — men Jorden drar MYCKET mer. Det handlar om massa."

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
- **Svarsalternativ (tap):** (A) "Äpplet och Jorden drar i varandra. Jorden har mer massa, så äpplet rör sig mest." (B) "Äpplet är tungt" (C) "Inget håller upp det"
- **Feedback rätt (A):** Fireworks-animation + "Du förstår gravitation! Allt med massa drar i allt annat. Mer massa = starkare drag."
- **Reflektionsfråga (visuellt val):** "Vad var mest förvånande?" — tre bildkort: (1) Äpplet drar i Jorden (2) Månen har gravitation (3) Allt drar i allt. Barnet trycker på ett kort, kort animation.
- **Teaser till astro-1-fusion:** Animerat gasmoln som dras ihop av pilar. Text: "Gravitation drar ihop gasmolnet. Vad händer när det pressas ihop tillräckligt? Det tar vi nästa gång!"

---

## Scaffolding-nivåer

Gäller steg 2, 4, 5, 6 (ej steg 1 — guided challenge):

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

## Vad appen INTE gör

1. **Förklarar inte fallhastighet.** "Tunga saker faller snabbare" är den segaste misconceptionen — appen undviker medvetet att jämföra fallhastighet. Steg 1 visar att fjädern faller långsammare, men förklarar det inte (luftmotstånd är ett eget koncept för senare).
2. **Nämner inte "neråt" som absolut riktning.** Gravitation drar mot centrum, men det kräver förståelse av klotformen. Appen säger "mot Jorden" utan att definiera riktning.
3. **Använder inte magnet-analogin.** Magnetism är selektiv (bara vissa material) — analogin skapar en felaktig mental modell som är svår att rätta.
4. **Introducerar inte gravitationskonstanten eller formler.** Abstrakt matematik kommer långt senare. Appen stannar vid "mer massa = starkare drag" som kvalitativ princip.
5. **Medvetet utelämnat nästa steg:** Avståndets roll (gravitationen avtar med avstånd²). Det kräver proportionellt tänkande som 8–9-åringar inte har. Nämns inte alls för att undvika half-förklaringar. Är lämpligt för 11–12 år.
