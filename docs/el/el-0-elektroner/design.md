# Design: el-0-elektroner — "Elektroner på utsidan"

## Prerequisite-analys

- **Koncept:** Atomer har en kärna och elektroner
  - **Täcks av:** `kemi-1-atomer` — delvis. Appen etablerar delarna, men `el-0` repeterar elektronen som brygga till el.
- **Koncept:** Elektronen hör till atomens utsida, inte kärnan
  - **Täcks av:** `kemi-1-atomer` — delvis. Visas i tidigare app, men är inte tidigare lärandemål och behöver därför byggas om explicit här.
- **Koncept:** Material består av många atomer i rad
  - **Täcks av:** `kemi-1-atomer` — delvis. Barnet vet att materia består av atomer; `el-0` gör om detta till materialkedjor.

**Beslut:** Designen kan fortsätta. Ingen separat prerequisite-app saknas före `el-0`, men appen måste själv lägga ett tydligt bryggsteg från "atomer har elektroner" till "många elektroner kan ta små steg vidare".

## Misconceptions (obligatoriskt för naturvetenskap)

- **Misconception:** Atomer är som planetsystem med elektroner i banor
  - **Adresseras i steg:** 2
  - **Hur:** Elektronen visas som en prick i en ytterzon utan ringar, banor eller rotation.
  - **Risk att förstärka:** Ja — skyddas genom att inga cirkelbanor eller "kretsar runt"-formuleringar används.
- **Misconception:** En elektron åker hela vägen genom materialet
  - **Adresseras i steg:** 6
  - **Hur:** ⚡ Prediction-steg mellan två animationer följs av observation där alla elektroner tar ett steg samtidigt.
  - **Risk att förstärka:** Ja — skyddas genom att ingen enskild elektron får vara "hjälte" i animationen.
- **Misconception:** Elektroner är samma sak som energi, ljus eller "el"
  - **Adresseras i steg:** 2, 7
  - **Hur:** Elektronen hålls som en partikelprick vid en atom, medan batteri, blixtsymbol och lamp-ljus inte används som elektronbilder.
  - **Risk att förstärka:** Ja — skyddas genom att ordet `ström` skjuts upp och att blixtsymbol bara används för knuffknappen, inte för elektronen.
- **Misconception:** Elektricitet är något som skickas ut och tar slut
  - **Adresseras i steg:** 6, 7
  - **Hur:** Barnet ser en kedja där alla positioner redan är fyllda; ingen elektron lämnar kedjan och ingen "källa" visas ännu.
  - **Risk att förstärka:** Nej — skyddas mot genom att batteri, krets och ordet `ström` medvetet utelämnas i denna modul.

## Lärandemål

Eleven ska förstå att elektroner sitter på atomens utsida och att många elektroner i vissa material kan ta små steg vidare, en position i taget, inte att en enda elektron åker långt genom materialet.

## Målgrupp och enhet

- Ålder: 8–9 år
- Primär enhet (mobil/iPad/laptop): iPad 13–14"
- Touch target-storlek (px): minst 80×80 px

## Visuella variabler (obligatoriskt)

| Variabel | Representerar | Konsekvent i hela modulen? |
|---|---|---|
| Gul prick | Elektron | Ja — samma färg och form i alla steg |
| Orange/rött kärnkluster | Atomkärnan | Ja — kärnan ändrar aldrig betydelse |
| Ljus ytterzon runt kärnan | Platsen där elektronen sitter på utsidan | Ja — används i steg 2–7 utan ringbanor |
| Skålformens djup | Hur hårt materialet håller elektronen | Ja — djup skål = hårdare, grund skål = lösare. Ersätter den tidigare abstrakta "ytterzonens bredd". |
| Återfjädringens hastighet | Hur hårt materialet håller elektronen | Ja — snabb/stel retur = hårdare, långsammare/mjuk retur = lösare |
| Vita hempositioner i kedjan | Att varje elektron bara får flytta ett steg i taget | Ja — varje steg i kedjeanimationen landar i nästa position, aldrig längre |
| Blå knuffvåg | En yttre knuff som sprider rörelse i kedjan | Ja — används bara när barnet själv startar en knuff |

**Begränsning för hela modulen:** Bara en synlig elektron visas per atom i alla steg. Detta är ett medvetet pedagogiskt val för att undvika att implementationen råkar återskapa ett skal- eller banmönster.

## Sessionsstruktur

### Steg 1 — Inuti sladden (Guided challenge)

- **Do-komponent (vad gör eleven aktivt?):** Barnet väljer mellan två materialkedjor och gissar i vilken en liten knuff lättast kan åka vidare.
- **CRA-nivå (Konkret / Representationell / Abstrakt):** Konkret → Representationell
- **Layout (beskriv i ord var elementen ligger, t.ex. "tre bollar i rad, drag-zone under"):** Överst en enkel vardagsbild av en sladd till en lampa. Under sladden ett förstoringsglas som zoomar in till två stora kedjekort sida vid sida. Kedjekorten ska vara extremt visuellt enkla: bara fyra runda former i rad med en gul prick nära utsidan på varje, inga etiketter och inget som kräver att barnet redan vet vad en atom är.
- **Text på skärmen (skriv ut exakt, max enligt ålderstabellen i principer.md):** "Har du sett en sladd? Inuti finns pyttesmå delar som sitter på rad efter varandra. I vilken rad tror du att en liten knuff kan åka vidare lättast?"
- **Interaktionstyp (tap / drag / slider / etc.):** Tap på vänster eller höger kedja
- **Visuell feedback vid rätt svar:** Inget rätt/fel här. Vald kedja får varm glöd och texten "Bra gissning! Nu zoomar vi in."
- **Visuell feedback vid fel svar:** Inget fel i guided challenge
- **Kontraintuitivt moment?** Nej

### Steg 2 — Vilken prick är elektronen?

- **Do-komponent (vad gör eleven aktivt?):** Barnet trycker på olika delar av en stor atom för att hitta elektronen.
- **CRA-nivå (Konkret / Representationell / Abstrakt):** Representationell
- **Layout (beskriv i ord var elementen ligger, t.ex. "tre bollar i rad, drag-zone under"):** En stor atom i mitten. Kärnan är ett orange kluster i centrum. En gul prick syns i ytterzonen till höger. Tre stora tryckytor: kärna, ytterzon och gul prick.
- **Text på skärmen (skriv ut exakt, max enligt ålderstabellen i principer.md):** "Tryck på den lilla gula pricken. Det är elektronen!"
- **Interaktionstyp (tap / drag / slider / etc.):** Tap
- **Visuell feedback vid rätt svar:** Den gula pricken pulserar, etiketten "Elektron" dyker upp precis intill, och texten blir "Ja! Elektronen sitter på utsidan av kärnan."
- **Visuell feedback vid fel svar:** Fel del skakar mjukt. Efter andra felet tonas resten ner och den gula pricken får en mjuk puls.
- **Kontraintuitivt moment?** Nej

### Steg 3 — Kärnan håller fast

- **Do-komponent (vad gör eleven aktivt?):** Barnet drar den gula pricken lite åt sidan och ser hur den fjädrar tillbaka.
- **CRA-nivå (Konkret / Representationell / Abstrakt):** Konkret → Representationell
- **Layout (beskriv i ord var elementen ligger, t.ex. "tre bollar i rad, drag-zone under"):** Samma stora atom som i steg 2, nu med en diskret finger-ikon vid elektronen. Under atomen en kort textremsa.
- **Text på skärmen (skriv ut exakt, max enligt ålderstabellen i principer.md):** "Dra elektronen lite åt sidan. Ser du? Kärnan håller fast den."
- **Interaktionstyp (tap / drag / slider / etc.):** Drag
- **Visuell feedback vid rätt svar:** Elektronen rör sig en kort bit och fjädrar tillbaka. En kort mjuk linje visar att den hålls kvar.
- **Visuell feedback vid fel svar:** Om barnet drar i kärnan händer inget, och elektronen pulserar som nästa ledtråd.
- **Kontraintuitivt moment?** Nej

### Steg 4 — Knuffa elektronen

- **Do-komponent (vad gör eleven aktivt?):** Barnet trycker på en knuffknapp och ser hur en liten kraft träffar elektronen utifrån. Elektronen rör sig — och fjädrar tillbaka.
- **CRA-nivå (Konkret / Representationell / Abstrakt):** Konkret → Representationell
- **Layout (beskriv i ord var elementen ligger, t.ex. "tre bollar i rad, drag-zone under"):** Samma stora atom som i steg 3. Till vänster om atomen finns en stor knapp med en liten pil som pekar mot elektronen — det är knuffknappen. Under atomen en kort textremsa.
- **Text på skärmen (skriv ut exakt, max enligt ålderstabellen i principer.md):** "Tryck på knappen. Den knuffar elektronen. Vad händer?"
- **Interaktionstyp (tap / drag / slider / etc.):** Tap på knuffknappen
- **Visuell feedback vid rätt svar:** En synlig blå puff åker från knappen och träffar elektronen. Elektronen rör sig en bit utåt — och fjädrar tillbaka. Texten blir: "Elektronen fick en knuff! Men kärnan drog tillbaka den."
- **Visuell feedback vid fel svar:** Ingen felväg; om barnet väntar börjar knuffknappen pulsera.
- **Kontraintuitivt moment?** Nej
- **Designmotivering:** Detta steg definierar "knuff" som extern kraft genom handling. Barnet har dragit elektronen själv (steg 3) och ser nu att en utifrån-knuff gör samma sak. Utan detta steg möter barnet ordet "knuff" i steg 5 utan att ha upplevt vad det betyder.

### Steg 5 — Samma knuff, olika lätt

- **Do-komponent (vad gör eleven aktivt?):** Barnet trycker på samma knuffknapp under två atomer sida vid sida och jämför hur mycket elektronerna rör sig. Ytterzonen runt varje atom visas som en *skålform* — en djup skål respektive en grund skål. Barnet väljer sedan vilken atom som höll elektronen lösare.
- **CRA-nivå (Konkret / Representationell / Abstrakt):** Representationell
- **Layout (beskriv i ord var elementen ligger, t.ex. "tre bollar i rad, drag-zone under"):** Två stora atomer sida vid sida. Under varje atom visas ytterzonen som en skålformad kurva — en tydligt djup och en tydligt grund. Under varje atom finns en knuffknapp. Efter att barnet knuffat båda visas två valknappar: "vänster" och "höger".
- **Text på skärmen (skriv ut exakt, max enligt ålderstabellen i principer.md):** "Knuffa båda lika. I vilken är det lättare att flytta elektronen?"
- **Interaktionstyp (tap / drag / slider / etc.):** Tap (knuffknapp × 2, sedan valknapp)
- **Visuell feedback vid rätt svar:** Rätt atom (grund skål) får grön ram. Replay i slow motion. Text: "Ja! I den grunda skålen är det lättare. Kärnan håller inte lika hårt."
- **Visuell feedback vid fel svar:** Båda knuffarna spelas upp igen med tydligare markering av hur långt elektronen rörde sig. Skålformerna förstärks visuellt.
- **Kontraintuitivt moment?** Nej
- **Designmotivering:** Skålanalogin ersätter det abstrakta "sitter lösare" med en visuell metafor som 8-åringar har taktil erfarenhet av — en boll i en djup skål vs en grund skål. Analogin mappar korrekt mot potentialbrunnens fysik och undviker antropomorfisering och magnetanalogi.

### Steg 6 — Först händer inget

- **Do-komponent (vad gör eleven aktivt?):** Barnet tittar på en kort rad med två atomer och märker att inget händer förrän barnet själv trycker på knuffknappen.
- **CRA-nivå (Konkret / Representationell / Abstrakt):** Representationell
- **Layout (beskriv i ord var elementen ligger, t.ex. "tre bollar i rad, drag-zone under"):** En kort rad med två atomer. Den första elektronen har en vit hemposition ett steg framför sig (mellan atom 1 och atom 2). Under raden finns en stor knapp: "Knuffa".
- **Text på skärmen (skriv ut exakt, max enligt ålderstabellen i principer.md):** "Titta. Inget händer av sig själv. Tryck på knuffen!"
- **Interaktionstyp (tap / drag / slider / etc.):** Tap på stor knapp
- **Visuell feedback vid rätt svar:** En blå knuff träffar den första elektronen. Den tar ett steg till nästa vita position och stannar. Animationen pausar tydligt. Text: "Elektronen flyttade sig ett steg. Men bara när du knuffade!"
- **Visuell feedback vid fel svar:** Ingen felväg; om barnet väntar börjar knuffknappen pulsera.
- **Kontraintuitivt moment?** Nej

### Steg 7 — Vad händer med grannen?

- **Do-komponent (vad gör eleven aktivt?):** Barnet knuffar den första elektronen i en kort rad med 3 atomer och ser hur elektronen landar, stannar — och sedan knuffar nästa elektron vidare. Barnet trycker på "Knuffa" och ser hela sekvensen i slow motion.
- **CRA-nivå (Konkret / Representationell / Abstrakt):** Representationell
- **Layout (beskriv i ord var elementen ligger, t.ex. "tre bollar i rad, drag-zone under"):** En rad med 3 atomer med vita hempositioner mellan dem. Varje atom har sin gula elektron. Under raden en stor "Knuffa"-knapp. Under animationen visas en kort textremsa som uppdateras i takt med animationen.
- **Text på skärmen (skriv ut exakt, max enligt ålderstabellen i principer.md):** Före knuff: "Vad händer med grannens elektron? Tryck och titta!" Under animationen (synkad med rörelsen): "Elektron 1 flyttar sig…" → [paus] → "…och knuffar elektron 2 vidare!" Efter: "Varje elektron knuffar sin granne ett steg."
- **Interaktionstyp (tap / drag / slider / etc.):** Tap på knuffknapp. Barnet kan trycka "Igen" för att se replay.
- **Visuell feedback vid rätt svar:** Animationen körs sekventiellt och långsamt: (1) Elektron 1 lämnar sin position, glider till nästa vita plats och *stannar synligt* med en kort paus och en liten studs. (2) Elektron 2 rör sig därefter till sin nästa vita plats och stannar. (3) Elektron 3 rör sig sist. Varje elektron fastnar tydligt i sin nya position — ingen elektron passerar förbi.
- **Visuell feedback vid fel svar:** Ingen felväg; steget är observation med replay-möjlighet.
- **Kontraintuitivt moment?** Nej
- **Designmotivering:** Detta steg etablerar *överföringsmekanismen* — att elektroner kan knuffa varandra vidare — som barnet behöver för att kunna prediktera i steg 8. Utan detta steg möter barnet valkorten "en åker långt" vs "alla flyttar sig" utan att ha sett hur rörelse sprids från en elektron till nästa.

### Steg 8 — Vilken bild stämmer?

- **Do-komponent (vad gör eleven aktivt?):** Barnet väljer först vilken av två små bilder som det tror stämmer. Sedan visas utfallet i en längre rad.
- **CRA-nivå (Konkret / Representationell / Abstrakt):** Representationell → Abstrakt
- **Layout (beskriv i ord var elementen ligger, t.ex. "tre bollar i rad, drag-zone under"):** Två stora valkort överst. Kort A visar en enda gul prick som far långt förbi flera atomer. Kort B visar många gula prickar som alla flyttar sig en position. Under korten finns den riktiga raden med 4–5 atomer.
- **Text på skärmen (skriv ut exakt, max enligt ålderstabellen i principer.md):** "I en längre rad — vad tror du händer? Välj en bild."
- **Interaktionstyp (tap / drag / slider / etc.):** Tap på ett valkort, sedan tap på "Se vad som händer"
- **Visuell feedback vid rätt svar:** Raden visar att alla prickar flyttar sig ett steg nästan samtidigt. Text direkt under raden: "Alla flyttar sig ett steg. Ingen åker hela vägen."
- **Visuell feedback vid fel svar:** Samma riktiga animation visas ändå, men felkortet tonas ner och rätt kort får ljusram. Text direkt under de rörliga prickarna: "Titta — inte bara en prick rör sig. Alla prickar tar ett litet steg var."
- **Kontraintuitivt moment?** Ja → ⚡ **Prediction-steg:** barnet väljer först mellan "en åker långt" och "alla flyttar sig ett steg". **Observe:** den riktiga raden visar det nästan simultana ett-stegs-skiftet. **Explain:** texten säger explicit att ingen åker hela vägen.

### Steg 9 — Det här lärde du dig

- **Do-komponent (vad gör eleven aktivt?):** Barnet väljer en bild som bäst visar vad en elektron är.
- **CRA-nivå (Konkret / Representationell / Abstrakt):** Abstrakt
- **Layout (beskriv i ord var elementen ligger, t.ex. "tre bollar i rad, drag-zone under"):** Tre sammanfattningskort i en kolumn: "på utsidan", "djup eller grund skål", "alla knuffar vidare". Under dem tre bildval: gul prick vid atom, blixt, batteri.
- **Text på skärmen (skriv ut exakt, max enligt ålderstabellen i principer.md):** "Elektronen sitter på utsidan. Vissa material håller fast elektronen hårdare — som en djup skål. I vissa material kan alla elektroner knuffa varandra vidare, ett steg i taget. Vilken bild visar en elektron?"
- **Interaktionstyp (tap / drag / slider / etc.):** Tap
- **Visuell feedback vid rätt svar:** Bilden med gul prick vid atomen får grön markering. Sluttext: "Ja! Nästa gång får du testa i vilka riktiga material elektroner lätt kan ta små steg."
- **Visuell feedback vid fel svar:** Blixt- eller batteribilden tonas ner. Den riktiga elektronen pulserar bredvid ett sammanfattningskort. Text: "Blixten och batteriet visar inte elektronen. Titta på den gula pricken vid atomen."
- **Kontraintuitivt moment?** Nej

## Guided challenge (steg 1)

Appen börjar med ett vardagsobjekt barnet känner igen: en sladd till en lampa. Barnet får inte först en förklaring om elektroner, utan en fråga om ett fenomen inne i sladden: "I vilken rad tror du att en liten knuff kan åka vidare lättast?" Vardagsförankringen är att sladdar finns hemma och i skolan, men det osynliga inuti är nytt. Guided challenge sparar barnets första gissning och återkopplas i sista steget när modulen sammanfattas.

## Scaffolding-nivåer

- **Fel 1:** Rätt del eller rätt kedja får en mjuk puls eller glöd.
- **Fel 2:** En kort textledtråd visas precis intill det relevanta elementet, till exempel "Titta på ytterpricken" eller "Jämför hur långt de rör sig".
- **Fel 3 (full scaffold):** Händelsen spelas upp i slow motion med markerade hempositioner och rätt val förklaras i en enda kort mening.

## Gate-keeping

- **Steg 2:** Barnet måste trycka på elektronen innan det går vidare.
- **Steg 4:** Barnet måste trycka på knuffknappen och se att elektronen fjädrar tillbaka.
- **Steg 5:** Barnet måste identifiera vilken atom som höll elektronen lösare.
- **Steg 6:** Barnet måste själv utlösa knuffen.
- **Steg 8:** Barnet måste se den riktiga animationen och välja om efter behov.
- **Steg 1, 3, 7, 9:** Ingen gate-keeping.

## Konsolidering (sista steget)

- **Hur sammanfattas det barnet lärt sig?** Tre kort återger modulens tre kärninsikter: elektronen sitter på utsidan, olika material håller fast olika hårt (skålanalogin), och i en rad kan alla elektroner knuffa varandra vidare ett steg i taget.
- **Återkoppling till guided challenge i steg 1?** Barnets första gissning från steg 1 visas igen som "Du gissade på den här raden först". Därefter visas vilken rad som faktiskt lät knuffen åka vidare lättare.
- **Reflektionsfråga (flerval/visuellt val, aldrig textfält):** Ingen separat extra reflektionsuppgift i appen. Konsolideringen hålls till ett enda bildval för att undvika för hög kognitiv belastning i sista steget.

## Metakognition

- **Hur visas framsteg? (Karta/stegindikator, inte poäng):** En enkel rad med nio stora punkter i toppen. Aktuell punkt glöder, tidigare blir gröna.
- **Lärandemål: visas riktning i början, full återkoppling i slutet:** I början står "Idag ser du vad som finns inuti en sladd." I slutet sammanfattas exakt vad barnet nu vet, med teaser mot nästa modul: "Nästa gång får du testa i vilka riktiga material elektroner lätt kan ta små steg."

## Responsivt beteende

- **Mobilvy (8"): vad ändras jämfört med baslayout?** Atomerna i steg 5 staplas vertikalt (en i taget). Bara en atom visas åt gången i steg 5. Texten kortas till max två rader. Ingen samtidig jämförelse mellan tre kort i slutsteget; de blir svepkort.
- **Surfplatta (13"): baslayout** Baslayouten är två rader sida vid sida i steg 1, två atomer sida vid sida i steg 5, två valkort överst i steg 8 och tre sammanfattningskort i kolumn i steg 9.
- **Laptop (16"): vad kan läggas till?** Vardagsbilden av sladden kan ligga kvar i vänsterkolumn samtidigt som mikrovyn visas till höger. Slow-motion replay i steg 5 och 8 kan visas i en liten sidopanel.

## Auditory icons

- **Rätt svar:** Kort mjuk dubbel-pling, varm och lugn
- **Fel svar:** Dovt litet bonk, neutralt och icke-straffande
- **Progression (går till nästa steg):** Litet pop-swoosh
- **Knuff:** Kort fingertapp-klick
- **Fjäderretur (steg 3, 4):** Mjukt boing — markerar att elektronen hålls kvar
- **Granne-knuff (steg 7):** Kort dov klick vid varje ny position — markerar att varje elektron stannar
- **Samtidigt ett-stegsskifte (steg 8):** Fyra snabba tick i följd, nära varandra i tid

## Tekniska beslut

- **Vanilla JS eller React (motivera):** React via CDN. Modulen har flera steg med sparade prediction-val, synkroniserade animationer, slow-motion replay och flera små state-övergångar som blir tydligare i komponentform.
- **Animationer (lista konkret vad som animeras):**
  - zoom från sladd till materialrader i steg 1
  - mjuk puls på elektronen i steg 2
  - drag + fjäderretur i steg 3
  - blå knuffpuff + fjäderretur i steg 4
  - synkron replay av två atomer med skålformer i steg 5
  - kort knuffmarkering vid första atomen i steg 6
  - sekventiell långsam kedjereaktion (elektron 1 → 2 → 3) i steg 7
  - nästan simultant ett-stegsskifte i steg 8
  - kort slow-motion replay i steg 5 och 8
- **Rörliga targets? Nej (om inte starkt motiverat):** Nej. Alla tryckytor är statiska när barnet ska interagera med dem. Rörelse sker först efter att input redan givits.
- **Viktig implementationsnot — knuffvisualisering:** Knuffen får inte visualiseras som något som "åker genom" hela raden. Den blå markeringen ska vara mycket kortlivad och bara synas nära första atomen.
- **Viktig implementationsnot — steg 7 vs steg 8:** Steg 7 visar överföringen *sekventiellt och långsamt* (en elektron i taget, med tydlig paus). Steg 8 visar samma mekanism *snabbt och nästan simultant*. Skillnaden i animationshastighet är pedagogiskt avsiktlig — steg 7 bygger förståelse, steg 8 visar vad som "egentligen" händer i ett material.

## Developmental progression-check (obligatorisk)

Gå igenom stegen i sekvens. Kontrollera för varje stegpar (N → N+1):
- **Steg 1 → 2:** Steg 1 visar rader av pyttesmå delar. Steg 2 zoomar in på en atom och frågar var elektronen sitter. Nytt koncept: elektronens position. ✓ Ett koncept.
- **Steg 2 → 3:** Steg 2 identifierar elektronen. Steg 3 lägger till att kärnan håller fast den. Nytt koncept: fasthållning. ✓ Ett koncept.
- **Steg 3 → 4:** Steg 3 visar fasthållning via drag. Steg 4 introducerar extern knuff som gör samma sak. Nytt koncept: knuff utifrån. ✓ Ett koncept. Nyckelord "knuff" definieras här genom handling.
- **Steg 4 → 5:** Steg 4 visar knuff på en atom. Steg 5 jämför två atomer med olika skåldjup. Nytt koncept: olika material håller olika hårt. ✓ Ett koncept. Ordet "knuff" är redan definierat i steg 4.
- **Steg 5 → 6:** Steg 5 visar skillnad mellan material. Steg 6 visar att en elektron kan ta ett steg i en rad. Nytt koncept: rörelse i en rad kräver knuff utifrån. ✓ Ett koncept.
- **Steg 6 → 7:** Steg 6 visar att en elektron rör sig efter knuff. Steg 7 visar vad som händer med grannen — överföringsmekanismen. Nytt koncept: elektroner kan knuffa varandra vidare. ✓ Ett koncept.
- **Steg 7 → 8:** Steg 7 visar sekventiell överföring i 3 atomer. Steg 8 frågar vad som händer i en längre rad (prediction). Nytt koncept: extrapolering + simultanitet. ✓ Ett koncept (prediction-steget hanterar det kontraintuitiva momentet).
- **Steg 8 → 9:** Steg 9 konsoliderar utan nytt ämnesinnehåll. ✓

**Begreppskontroll:** Varje ord och begrepp som steg N+1 använder ska vara definierat genom handling i steg N eller tidigare:
- "Knuff" — definieras i steg 4 (knuffknappen).
- "Rad" — definieras visuellt i steg 1, benämns i text från steg 1.
- "Granne" — definieras visuellt i steg 6 (atomer sida vid sida), benämns först i steg 7.
- "Skål" — introduceras visuellt i steg 5. Ingen text nämner ordet "skål" förrän barnet sett formen.

**Tumregel:** Varje steg ska introducera maximalt *ett* nytt koncept. Varje begrepp ska definieras genom handling, inte genom text.

## Stealth assessment (obligatoriskt)

- **Vad mäts:** Barnets första val i steg 1
  - **Vad indikerar det:** Om barnet spontant kan läsa av vilken rad som verkar hålla lösare respektive hårdare
  - **I vilket steg:** 1
- **Vad mäts:** Första tryckpunkt i steg 2 (kärna, tom zon eller gul prick)
  - **Vad indikerar det:** Om barnet redan placerar elektronen på utsidan eller blandar ihop delarna
  - **I vilket steg:** 2
- **Vad mäts:** Hur långt barnet drar elektronen i steg 3 innan det släpper
  - **Vad indikerar det:** Om barnet tolkar elektronen som fri partikel eller som något som faktiskt hålls kvar
  - **I vilket steg:** 3
- **Vad mäts:** Antal omspelningar och svar i steg 5
  - **Vad indikerar det:** Om barnet uppfattar skåldjup som materialegenskap eller bara gissar
  - **I vilket steg:** 5
- **Vad mäts:** Val mellan "en åker långt" och "alla flyttar sig ett steg" i steg 8
  - **Vad indikerar det:** Om barnet fortfarande bär på den sekventiella felmodellen
  - **I vilket steg:** 8

## Vad appen INTE gör

1. **Ordet `ström` används inte som ny etikett här.**
   Det skjuts upp till senare modul för att inte aktivera source-consumer-felmodellen innan barnet sett krets och batteri.

2. **Batteri, spänning och volt utelämnas helt.**
   Det är nästa steg i ämnet och hör hemma i `el-2-kretsar`, inte i denna prerequisite-modul.

3. **Ledare och isolator som fackord introduceras inte ännu.**
   Barnet får först uppleva fenomenet "lösare/hårdare" innan orden namnges i `el-1-ledare`.

4. **Banor, skal och flera elektroner per atom visas inte.**
   Det minskar risken för planetsystemsmodellen och för att barnet frågar varför "fel" elektron hoppar. Bara en synlig elektron per atom används genom hela modulen.

5. **Vilket nästa steg i ämnet utelämnas medvetet, och varför är det lämpligt för denna åldersgrupp?**
   Nästa steg är att testa riktiga material och sätta orden `ledare` och `isolator` på skillnaden. Det utelämnas här för att 8–9-åringen först ska få en stabil mikromodell utan ytterligare fackord.
