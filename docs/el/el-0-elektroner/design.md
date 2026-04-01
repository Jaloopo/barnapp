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
| Ytterzonens bredd | Hur lätt elektronen kan röra sig i just det materialet | Ja — bredare zon = lösare, smalare zon = hårdare |
| Återfjädringens hastighet | Hur hårt materialet håller elektronen | Ja — snabb/stel retur = hårdare, långsammare/mjuk retur = lösare |
| Vita hempositioner i kedjan | Att varje elektron bara får flytta ett steg i taget | Ja — varje steg i kedjeanimationen landar i nästa position, aldrig längre |
| Blå knuffvåg | En yttre knuff som sprider rörelse i kedjan | Ja — används bara när barnet själv startar en knuff |

## Sessionsstruktur

### Steg 1 — Inuti sladden (Guided challenge)

- **Do-komponent (vad gör eleven aktivt?):** Barnet väljer mellan två materialkedjor och gissar i vilken en liten knuff lättast sprider sig.
- **CRA-nivå (Konkret / Representationell / Abstrakt):** Konkret → Representationell
- **Layout (beskriv i ord var elementen ligger, t.ex. "tre bollar i rad, drag-zone under"):** Överst en enkel vardagsbild av en sladd till en lampa. Under sladden ett förstoringsglas som zoomar in till två stora kedjekort sida vid sida. Varje kedja visar 4 atomer i rad med en gul prick på utsidan av varje atom.
- **Text på skärmen (skriv ut exakt, max enligt ålderstabellen i principer.md):** "Har du sett en sladd? Inuti finns pyttesmå delar i kedjor. I vilken kedja tror du att en liten knuff sprider sig lättast?"
- **Interaktionstyp (tap / drag / slider / etc.):** Tap på vänster eller höger kedja
- **Visuell feedback vid rätt svar:** Inget rätt/fel här. Vald kedja får varm glöd och texten "Bra gissning! Nu zoomar vi in."
- **Visuell feedback vid fel svar:** Inget fel i guided challenge
- **Kontraintuitivt moment?** Nej

### Steg 2 — Vilken prick är elektronen?

- **Do-komponent (vad gör eleven aktivt?):** Barnet trycker på olika delar av en stor atom för att hitta elektronen.
- **CRA-nivå (Konkret / Representationell / Abstrakt):** Representationell
- **Layout (beskriv i ord var elementen ligger, t.ex. "tre bollar i rad, drag-zone under"):** En stor atom i mitten. Kärnan är ett orange kluster i centrum. En gul prick syns i ytterzonen till höger. Tre stora tryckytor: kärna, ytterzon och gul prick.
- **Text på skärmen (skriv ut exakt, max enligt ålderstabellen i principer.md):** "Vilken prick är elektronen? Tryck på den."
- **Interaktionstyp (tap / drag / slider / etc.):** Tap
- **Visuell feedback vid rätt svar:** Den gula pricken pulserar, etiketten "Elektron" dyker upp precis intill, och texten blir "Ja. Elektronen sitter på utsidan av kärnan."
- **Visuell feedback vid fel svar:** Fel del skakar mjukt. Efter andra felet tonas resten ner och den gula pricken får en mjuk puls.
- **Kontraintuitivt moment?** Nej

### Steg 3 — Kärnan håller fast

- **Do-komponent (vad gör eleven aktivt?):** Barnet drar den gula pricken lite åt sidan och ser hur den fjädrar tillbaka.
- **CRA-nivå (Konkret / Representationell / Abstrakt):** Konkret → Representationell
- **Layout (beskriv i ord var elementen ligger, t.ex. "tre bollar i rad, drag-zone under"):** Samma stora atom som i steg 2, nu med en diskret finger-ikon vid elektronen. Under atomen en kort textremsa.
- **Text på skärmen (skriv ut exakt, max enligt ålderstabellen i principer.md):** "Prova att dra elektronen lite. Ser du? Kärnan håller fast den."
- **Interaktionstyp (tap / drag / slider / etc.):** Drag
- **Visuell feedback vid rätt svar:** Elektronen rör sig en kort bit och fjädrar tillbaka. En kort mjuk linje visar att den hålls kvar.
- **Visuell feedback vid fel svar:** Om barnet drar i kärnan händer inget, och elektronen pulserar som nästa ledtråd.
- **Kontraintuitivt moment?** Nej

### Steg 4 — Samma lilla knuff, olika hårt

- **Do-komponent (vad gör eleven aktivt?):** Barnet trycker på samma "putta lite"-knapp under två materialkedjor och jämför hur mycket de yttre elektronerna rör sig. Sedan väljer barnet vilken kedja som höll lösare.
- **CRA-nivå (Konkret / Representationell / Abstrakt):** Representationell
- **Layout (beskriv i ord var elementen ligger, t.ex. "tre bollar i rad, drag-zone under"):** Två kedjekort sida vid sida. Under varje kort finns en stor knapp med ett finger. Efter jämförelsen visas två valknappar: "vänster kedja" och "höger kedja".
- **Text på skärmen (skriv ut exakt, max enligt ålderstabellen i principer.md):** "Tryck lika på båda. I vilken kedja sitter elektronerna lösare?"
- **Interaktionstyp (tap / drag / slider / etc.):** Tap
- **Visuell feedback vid rätt svar:** Rätt kedja får grön ram och replay i slow motion. Text: "Ja. I den här kedjan sitter elektronerna lösare."
- **Visuell feedback vid fel svar:** Båda knuffarna spelas upp igen, nu med tydligare ytterzoner och returrörelse markerad.
- **Kontraintuitivt moment?** Nej

### Steg 5 — Först händer inget

- **Do-komponent (vad gör eleven aktivt?):** Barnet tittar på en lösare kedja och märker att inget rör sig förrän barnet själv trycker på knuffknappen.
- **CRA-nivå (Konkret / Representationell / Abstrakt):** Representationell
- **Layout (beskriv i ord var elementen ligger, t.ex. "tre bollar i rad, drag-zone under"):** En materialkedja med fyra atomer i rad. Varje atom har en gul prick på utsidan och en vit hemposition bredvid nästa atom. Under kedjan en stor knapp: "Knuffa".
- **Text på skärmen (skriv ut exakt, max enligt ålderstabellen i principer.md):** "Titta noga. Först händer inget. Tryck på knuffen."
- **Interaktionstyp (tap / drag / slider / etc.):** Tap på stor knapp
- **Visuell feedback vid rätt svar:** När barnet trycker går en blå knuffvåg genom kedjan och alla elektroner flyttar sig ett steg till nästa vita position.
- **Visuell feedback vid fel svar:** Ingen felväg finns; om barnet väntar länge börjar knuffknappen pulsera.
- **Kontraintuitivt moment?** Nej

### Steg 6 — Vilken bild stämmer?

- **Do-komponent (vad gör eleven aktivt?):** Barnet väljer först vilken av två små bilder som det tror stämmer. Sedan visas utfallet i en längre kedja.
- **CRA-nivå (Konkret / Representationell / Abstrakt):** Representationell → Abstrakt
- **Layout (beskriv i ord var elementen ligger, t.ex. "tre bollar i rad, drag-zone under"):** Två stora valkort överst. Kort A visar en enda gul prick som far långt. Kort B visar många gula prickar som alla flyttar sig en position. Under korten finns den riktiga kedjan i full bredd.
- **Text på skärmen (skriv ut exakt, max enligt ålderstabellen i principer.md):** "Vad tror du händer? Välj en bild först."
- **Interaktionstyp (tap / drag / slider / etc.):** Tap på ett valkort, sedan tap på "Se vad som händer"
- **Visuell feedback vid rätt svar:** Kedjan visar att alla prickar flyttar sig ett steg samtidigt. Texten tänds exakt under kedjan: "Alla tar ett steg samtidigt. Ingen åker hela vägen."
- **Visuell feedback vid fel svar:** Samma riktiga animation visas ändå, men felkortet tonas ner och rätt kort får ljusram. Texten läggs direkt under de rörliga prickarna: "Titta på alla prickar. Varje elektron tar bara ett litet steg."
- **Kontraintuitivt moment?** Ja → **Prediction-steg:** barnet väljer först mellan "en åker långt" och "alla tar ett steg". **Observe:** den riktiga kedjan visar det samtidiga ett-stegs-skiftet. **Explain:** texten säger explicit att ingen åker hela vägen.

### Steg 7 — Det här lärde du dig

- **Do-komponent (vad gör eleven aktivt?):** Barnet väljer en bild som bäst visar vad en elektron är, och trycker sedan på det som var mest överraskande idag.
- **CRA-nivå (Konkret / Representationell / Abstrakt):** Abstrakt
- **Layout (beskriv i ord var elementen ligger, t.ex. "tre bollar i rad, drag-zone under"):** Tre sammanfattningskort i en kolumn: "på utsidan", "lösare/hårdare", "alla små steg". Under dem tre bildval: gul prick vid atom, blixt, batteri. Längst ner tre reflektionskort med små illustrationer från appen.
- **Text på skärmen (skriv ut exakt, max enligt ålderstabellen i principer.md):** "Elektronen sitter på utsidan. Vissa material håller hårdare. I vissa kedjor kan alla ta små steg. Vilken bild visar en elektron?"
- **Interaktionstyp (tap / drag / slider / etc.):** Tap
- **Visuell feedback vid rätt svar:** Bilden med gul prick vid atomen får grön markering. Sluttext: "Ja. Nästa gång testar du vilka riktiga material där små steg är lätta."
- **Visuell feedback vid fel svar:** Blixt- eller batteribilden tonas ner. Den riktiga elektronen pulserar bredvid ett sammanfattningskort.
- **Kontraintuitivt moment?** Nej

## Guided challenge (steg 1)

Appen börjar med ett vardagsobjekt barnet känner igen: en sladd till en lampa. Barnet får inte först en förklaring om elektroner, utan en fråga om ett fenomen inne i sladden: "I vilken kedja tror du att en liten knuff sprider sig lättast?" Vardagsförankringen är att sladdar finns hemma och i skolan, men det osynliga inuti är nytt. Guided challenge sparar barnets första gissning och återkopplas i sista steget när modulen sammanfattas.

## Scaffolding-nivåer

- **Fel 1:** Rätt del eller rätt kedja får en mjuk puls eller glöd.
- **Fel 2:** En kort textledtråd visas precis intill det relevanta elementet, till exempel "Titta på ytterpricken" eller "Jämför hur långt de rör sig".
- **Fel 3 (full scaffold):** Händelsen spelas upp i slow motion med markerade hempositioner och rätt val förklaras i en enda kort mening.

## Gate-keeping

- **Steg 2:** Barnet måste trycka på elektronen innan det går vidare.
- **Steg 4:** Barnet måste identifiera vilken kedja som höll lösare.
- **Steg 5:** Barnet måste själv utlösa knuffen.
- **Steg 6:** Barnet måste se den riktiga animationen och välja om efter behov.
- **Steg 1, 3, 7:** Ingen gate-keeping.

## Konsolidering (sista steget)

- **Hur sammanfattas det barnet lärt sig?** Tre kort återger modulens tre kärninsikter: elektronen sitter på utsidan, olika material håller olika hårt, och i en kedja tar alla små steg samtidigt.
- **Återkoppling till guided challenge i steg 1?** Barnets första gissning från steg 1 visas igen som "Du gissade på den här kedjan först". Därefter visas vilken kedja som faktiskt lät knuffen sprida sig lättare.
- **Reflektionsfråga (flerval/visuellt val, aldrig textfält):** "Vad var mest överraskande?" med tre bildkort: elektronen på utsidan, lösare/hårdare, alla tar ett steg samtidigt.

## Metakognition

- **Hur visas framsteg? (Karta/stegindikator, inte poäng):** En enkel kedja med sju stora punkter i toppen. Aktuell punkt glöder, tidigare blir gröna.
- **Lärandemål: visas riktning i början, full återkoppling i slutet:** I början står "Idag tittar du in i sladden." I slutet sammanfattas exakt vad barnet nu vet, med teaser mot nästa modul: "Nästa gång testar du riktiga material."

## Responsivt beteende

- **Mobilvy (8"): vad ändras jämfört med baslayout?** Kedjekorten staplas vertikalt. Bara en kedja visas åt gången i steg 4 och 6. Texten kortas till max två rader. Ingen samtidig jämförelse mellan tre kort i slutsteget; de blir svepkort.
- **Surfplatta (13"): baslayout** Baslayouten är två kedjekort sida vid sida i steg 1 och 4, två valkort överst i steg 6 och tre sammanfattningskort i kolumn i steg 7.
- **Laptop (16"): vad kan läggas till?** Vardagsbilden av sladden kan ligga kvar i vänsterkolumn samtidigt som mikrovyn visas till höger. Slow-motion replay i steg 4 och 6 kan visas i en liten sidopanel.

## Auditory icons

- **Rätt svar:** Kort mjuk dubbel-pling, varm och lugn
- **Fel svar:** Dovt litet bonk, neutralt och icke-straffande
- **Progression (går till nästa steg):** Litet pop-swoosh
- **Knuff:** Kort fingertapp-klick
- **Samtidigt ett-stegsskifte:** Fyra snabba tick i följd, nära varandra i tid

## Tekniska beslut

- **Vanilla JS eller React (motivera):** React via CDN. Modulen har flera steg med sparade prediction-val, synkroniserade kedjeanimationer, slow-motion replay och flera små state-övergångar som blir tydligare i komponentform.
- **Animationer (lista konkret vad som animeras):**
  - zoom från sladd till materialkedjor i steg 1
  - mjuk puls på elektronen i steg 2
  - drag + fjäderretur i steg 3
  - synkron replay av två kedjor i steg 4
  - blå knuffvåg genom kedjan i steg 5
  - samtidigt ett-stegsskifte i steg 5 och 6
  - kort slow-motion replay i steg 4 och 6
- **Rörliga targets? Nej (om inte starkt motiverat):** Nej. Alla tryckytor är statiska när barnet ska interagera med dem. Rörelse sker först efter att input redan givits.

## Developmental progression-check (obligatorisk)

Gå igenom stegen i sekvens. Kontrollera för varje stegpar (N → N+1):
- **Steg 1 → 2:** Steg 2 lägger bara till var elektronen sitter. Inget mellansteg behövs.
- **Steg 2 → 3:** Steg 3 lägger bara till att kärnan håller fast elektronen. Inget mellansteg behövs.
- **Steg 3 → 4:** Steg 4 lägger bara till att olika material håller olika hårt. Inget mellansteg behövs.
- **Steg 4 → 5:** Steg 5 lägger bara till att en knuff behövs för rörelse. Det bygger direkt på "lösare/hårdare" och hoppar inte till ordet `ström`.
- **Steg 5 → 6:** Steg 6 lägger bara till den kontraintuitiva insikten att alla tar ett steg samtidigt. Prediction-steg finns inbyggt, så inget extra mellansteg behövs.
- **Steg 6 → 7:** Steg 7 konsoliderar utan nytt ämnesinnehåll.

**Tumregel:** Varje steg ska introducera maximalt *ett* nytt koncept. Den tidigare planen att namnge `ström` här har tagits bort för att undvika två kognitiva språng i samma modul.

## Stealth assessment (obligatoriskt)

- **Vad mäts:** Barnets första val i steg 1
  - **Vad indikerar det:** Om barnet spontant kan läsa av vilken kedja som verkar hålla lösare respektive hårdare
  - **I vilket steg:** 1
- **Vad mäts:** Första tryckpunkt i steg 2 (kärna, tom zon eller gul prick)
  - **Vad indikerar det:** Om barnet redan placerar elektronen på utsidan eller blandar ihop delarna
  - **I vilket steg:** 2
- **Vad mäts:** Hur långt barnet drar elektronen i steg 3 innan det släpper
  - **Vad indikerar det:** Om barnet tolkar elektronen som fri partikel eller som något som faktiskt hålls kvar
  - **I vilket steg:** 3
- **Vad mäts:** Antal omspelningar och svar i steg 4
  - **Vad indikerar det:** Om barnet uppfattar "lösare/hårdare" som materialegenskap eller bara gissar
  - **I vilket steg:** 4
- **Vad mäts:** Val mellan "en åker långt" och "alla tar ett steg" i steg 6
  - **Vad indikerar det:** Om barnet fortfarande bär på den sekventiella felmodellen
  - **I vilket steg:** 6

## Vad appen INTE gör

1. **Ordet `ström` används inte som ny etikett här.**
   Det skjuts upp till senare modul för att inte aktivera source-consumer-felmodellen innan barnet sett krets och batteri.

2. **Batteri, spänning och volt utelämnas helt.**
   Det är nästa steg i ämnet och hör hemma i `el-2-kretsar`, inte i denna prerequisite-modul.

3. **Ledare och isolator som fackord introduceras inte ännu.**
   Barnet får först uppleva fenomenet "lösare/hårdare" innan orden namnges i `el-1-ledare`.

4. **Banor, skal och flera elektroner per atom visas inte.**
   Det minskar risken för planetsystemsmodellen och för att barnet frågar varför "fel" elektron hoppar.

5. **Vilket nästa steg i ämnet utelämnas medvetet, och varför är det lämpligt för denna åldersgrupp?**
   Nästa steg är att testa riktiga material och sätta orden `ledare` och `isolator` på skillnaden. Det utelämnas här för att 8–9-åringen först ska få en stabil mikromodell utan ytterligare fackord.
