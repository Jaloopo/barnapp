# Design: Molekyler — atomer som sätter ihop sig

## Lärandemål
Eleven ska förstå att atomer kan binda ihop sig till molekyler, och att en molekyl har andra egenskaper än de enskilda atomerna.

(Inte: hur bindningen fungerar kemiskt, inte elektronpar, inte kemiska formler som notation.)

## Målgrupp och enhet
- Ålder: 8–9 år
- Primär enhet: iPad 13"
- Touch target: 80×80 px (drag-and-drop med snap-to-zone)
- Språknivå: LIX 15–25, max 8–10 ord/mening, max 100–200 ord/skärm

## Sessionsstruktur

### Steg 1 — Vattenhemligheten (guided challenge)
- **Do-komponent:** Förutsäg vad som händer när väte och syre möts (flerval, 3 alternativ)
- **CRA-nivå:** Konkret
- **Layout:** Två stora cirklar (väte = liten ljusblå, syre = större röd) på var sin sida. Fråga i mitten. Tre svarsalternativ i botten.
- **Text på skärmen:** "Du dricker vatten varje dag. Väte är en osynlig gas. Syre är också en gas. Vad tror du händer om de möts?" Alternativ: (A) "De blandas till en ny gas" (B) "De sätter ihop sig till något nytt" (C) "Ingenting"
- **Interaktionstyp:** Tap (välj alternativ)
- **Visuell feedback vid val:** Ingen "rätt/fel" här — alla svar bekräftas med "Spännande tanke! Låt oss testa." Valet sparas för konsolidering.
- **Vardagsförankring:** Vatten — något barnet dricker och känner till. Väte och syre känner de igen som grundämnen från atom-appen.

### Steg 2 — Bygg vatten
- **Do-komponent:** Dra 2 väteatomer och 1 syreatom till en byggzon i mitten. De snäpper ihop till en vattenmolekyl.
- **CRA-nivå:** Konkret
- **Layout:** Atomlåda till vänster (väte-atomer staplade, syre-atomer staplade). Byggzon i mitten (rundad yta med tunn streckad kontur). Resultatruta till höger (tom, visar molekylen efter bygge).
- **Text på skärmen:** "Dra atomer till byggzonen. Vatten behöver 2 väte och 1 syre."
- **Interaktionstyp:** Drag-and-drop med snap-to-zone (Pointer Events)
- **Visuell feedback vid rätt:** Atomerna snäpper ihop med en kort "pop"-animation + vattenmolekyl bildas (två små blå cirklar kopplade till en röd). Mjukt pop-ljud. Texten: "Du byggde en vattenmolekyl!"
- **Visuell feedback vid fel (fel kombination):** Atomerna studsar tillbaka till lådan. Mjukt "blub"-ljud.

### Steg 3 — Något helt nytt
- **Do-komponent:** Jämför egenskaper genom att tappa på atomer vs molekylen och se skillnader (tap för att "testa" varje)
- **CRA-nivå:** Konkret → Representationell
- **Layout:** Tre kolumner: Väte | Syre | Vatten. Under varje: ikon-rad som visar egenskaper (gas/vätska, färg, om man kan dricka den). Barnet tappar på varje för att "testa".
- **Text på skärmen:** "Tryck på varje för att se vad den är." Under väte: "Osynlig gas." Under syre: "Osynlig gas." Under vatten: "En vätska du kan dricka!"
- **Interaktionstyp:** Tap
- **Visuell feedback:** Varje kolumn "aktiveras" med en kort glöd-animation. Vattenmolekylen visar en liten vattendroppe-animation. Sammanfattningsrad dyker upp: "Molekylen är något helt nytt!"
- **Visuell feedback vid fel:** Ej tillämpligt — utforskande steg.

### Steg 4 — Bygg koldioxid
- **Do-komponent:** Dra 1 kolatom och 2 syreatomer till byggzonen → koldioxidmolekyl.
- **CRA-nivå:** Konkret
- **Layout:** Samma som steg 2. Atomlåda nu med kol (svart cirkel) och syre. Ny molekyl i resultatrutan.
- **Text på skärmen:** "Nu ska du bygga det du andas ut! Koldioxid behöver 1 kol och 2 syre."
- **Interaktionstyp:** Drag-and-drop med snap-to-zone
- **Visuell feedback vid rätt:** Koldioxidmolekyl bildas (svart i mitten, röd på sidorna). "Du byggde koldioxid! Det andas du ut varje gång."
- **Visuell feedback vid fel:** Atomerna studsar tillbaka.

### Steg 5 — Molekylverkstad (guided discovery)
- **Do-komponent:** Välj fritt bland atomer (väte, syre, kol) och bygg molekyler. Appen visar vad som bildas om kombinationen finns, eller "Den molekylen finns inte — prova annat!" om den inte finns.
- **CRA-nivå:** Konkret → Representationell
- **Layout:** Atomlåda till vänster (alla tre atomtyper). Större byggzon i mitten. Resultatgalleri i botten (visar alla molekyler barnet byggt, som en samling).
- **Text på skärmen:** "Vad kan du bygga? Dra atomer och testa!"
- **Interaktionstyp:** Drag-and-drop
- **Visuell feedback vid giltig molekyl:** Pop-animation + molekylens namn visas + läggs till i galleriet.
- **Visuell feedback vid ogiltig kombination:** Atomerna skakar lätt och studsar tillbaka. "Den finns inte — prova en annan kombination!"
- **Möjliga molekyler:** H2 (vätgas), O2 (syrgas), H2O (vatten), CO2 (koldioxid), CH4 (metan — "finns i kossornas fisar!"). Max 5 möjliga för att hålla scope.

### Steg 6 — Konsolidering
- **Do-komponent:** Reflektionsfråga (flerval) + återkoppling till steg 1.
- **CRA-nivå:** Representationell → Abstrakt (ord)
- **Layout:** Överst: "Kommer du ihåg? Du gissade att..." + barnets svar från steg 1. Under: reflektionsfråga. Längst ned: samling av alla byggda molekyler.
- **Text på skärmen:** "Du gissade [barnets svar]. Nu vet du: atomer sätter ihop sig till molekyler. Molekyler är något helt nytt!" Reflektionsfråga: "Vad stämmer om molekyler?" (A) "De är bara blandade atomer" (B) "De är nya ämnen med nya egenskaper" (C) "De är samma som atomer, fast större"
- **Interaktionstyp:** Tap
- **Visuell feedback vid rätt (B):** Alla molekyler i galleriet gör en liten studs-animation. "Precis! En vattenmolekyl är inte bara väte och syre bredvid varandra — det är något helt nytt."
- **Visuell feedback vid fel:** Scaffolding (se nedan).

## Scaffolding-nivåer
- **Fel 1:** Visuell markering — rätt atoms/zon lyser upp kort med gul puls.
- **Fel 2:** Delvis ledtråd — text dyker upp, t.ex. "Vatten har 2 väte. Du har bara 1."
- **Fel 3:** Full scaffold — pilar ritas från rätt atomer till rätt position i byggzonen. Atomerna pulserar i turordning.

## Gate-keeping
- **Steg 2:** Måste bygga korrekt vattenmolekyl innan steg 3.
- **Steg 4:** Måste bygga korrekt koldioxid innan steg 5.
- **Steg 6:** Reflektionsfrågan gate-keepar inte — oavsett svar visas förklaring och appen avslutas.
- **Steg 1, 3, 5:** Ingen gate-keeping (utforskande).

## Metakognition
- **Framsteg:** Stegindikator i toppen — 6 cirklar, den aktiva fylld, avklarade har en liten molekyl-ikon. Inte poäng.
- **Lärandemål i början (steg 1):** "Idag ska du bygga molekyler!" visas kort som undertitel.
- **Lärandemål i slutet (steg 6):** "Du lärde dig att atomer sätter ihop sig till molekyler — och att molekylen är något helt nytt."

## Responsivt beteende
- **Mobil (8"):** Atomlåda ovanför byggzon istället för bredvid. Resultat under byggzon. En kolumn. Steg 3: egenskaper i vertikal lista, inte tre kolumner.
- **Surfplatta (13"):** Baslayout som beskriven ovan. Tre kolumner i steg 3.
- **Laptop (16"):** Större byggzon. I steg 5: resultatgalleri som sidopanel till höger. Hover-state på atomer visar namn.

## Auditory icons
- **Rätt svar / molekyl bildas:** Mjukt "pop" (kort, runt, 200ms)
- **Fel / ogiltig kombination:** Mjukt "blub" (kort, dovt, 150ms)
- **Progression (nästa steg):** Kort "pling" uppåt (stigande ton, 250ms)
- **Steg 5, ny molekyl i galleri:** Dubbel-pop (pop-pop, 300ms)

## Tekniska beslut
- **Vanilla JS** — appen har linjär progression med enkla drag-and-drop-interaktioner, inget komplext state-träd som motiverar React.
- **Animationer:** (1) Atomer som snäpper ihop — scale + position-transition, 300ms ease-out. (2) Molekyl-bildning — kort partikel-burst (CSS keyframes). (3) Puls/glow på scaffolding-hints — box-shadow animation. (4) Steg 3 kolumn-aktivering — opacity + scale. (5) Studs-tillbaka vid fel — translateX wiggle.
- **Rörliga targets:** Nej. Atomer ligger stilla i lådan. Pulserar med glow vid scaffolding, men rör sig inte.
- **Pointer Events** för all drag-and-drop (touch + mus).
- **prefers-reduced-motion:** Alla animationer reduceras till enkel opacity-fade. Inga partikel-bursts.

## Vad appen INTE gör
1. **Förklarar inte kemiska bindningar** — barnet behöver inte veta varför atomer binder, bara att de gör det. Elektron-delning sparas till senare.
2. **Använder inte kemiska formler som notation** — vi skriver "2 väte + 1 syre", inte "H₂O". Formella symboler är nästa steg.
3. **Visar inte periodiska systemet** — det var atom-appens domän. Här fokuserar vi enbart på kombinationer.
4. **Har inget poängsystem** — framsteg visas som stegindikator och molekylgalleri, inte stjärnor/poäng.
5. **Låter inte barnet skriva** — all reflektion sker via flerval eller visuellt val.
