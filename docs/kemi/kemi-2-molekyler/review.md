# Review: kemi-2-molekyler
*Datum: 2026-03-28 | Status: testad och godkänd*

---

## Vad fungerade

**Drag-and-drop som inlärningsrörelse** — Att fysiskt dra atomer till byggzonen ger en embodied upplevelse av att "sätta ihop" molekyler. Gesterna matchar konceptet (princip I).

**Molekylverkstaden (steg 5)** — Fri utforskning med galleri fungerade motiverande. Barnet ville prova alla kombinationer för att fylla galleriet utan att det kändes som ett test.

**Återkoppling till steg-1-gissningen (steg 6)** — Att återvisa barnets egna ord skapade ett tydligt "nu vet jag mer"-ögonblick. Bra konsolidering.

**Auditory icons** — Pop/blub/pling upplevdes som tydlig och icke-störande feedback.

**Scaffolding 3 nivåer** — Progressionen glow → text → pilar fungerade. Barn som fastnade i steg 2 hittade rätt kombination utan att ge upp.

---

## Problem och lösningar

### 1. Vetenskaplig precision: "blandas" vs "reagerar kemiskt"
**Problem:** Design-fasen inkluderade ingen Perplexity-research om hur H₂ + O₂ → H₂O faktiskt fungerar. Appens text är inte fel — "sätter ihop sig till något nytt" är korrekt — men ett viktigt faktum saknades i designbeslutet:

> Väte och syre *reagerar kemiskt*, de blandas inte bara. Reaktionen kräver energi för att starta (aktiveringsenergi). Det är därför de kan existera sida vid sida som gaser utan att spontant bli vatten.

**Konsekvens:** Appen visar atomer som bara "dras ihop" utan energiinput — det kan ge felintuitionen att det sker av sig självt. Alternativ A i steg 1 ("De blandas till en ny gas") markeras som fel, vilket är rätt — men förklaringen till *varför* är otydlig.

**Medvetet val för kemi-2 (8–9 år):** Aktiveringsenergi och exoterma reaktioner sparas till en framtida app (kemi-3 eller kemi-4). Det är en rimlig avgränsning. **Men det borde ha stått explicit i design.md** under "Vad appen INTE gör".

**Lösning för nästa version:** Lägg till i steg 2 en liten visuell "gnista" eller "energi-puff" innan atomerna snäpper ihop — behöver inte förklaras i text, men ger rätt intuition. Se kemi-3-design-kriteriet nedan.

### 2. Git-policy: bygget nådde inte main direkt
**Problem:** Cloud-miljön injicerade en feature-branch-instruktion som överstyrde CLAUDE.md:s "pusha alltid till main". Appen nådde main via manuell merge efteråt.
**Lösning:** CLAUDE.md uppdateras med explicit checkout-steg i Flöde 2. (Se separat commit.)

### 3. Steg 5: ogiltig kombinationsfeedback saknades
**Problem:** Om barnet lägger 5 atomer som inte bildar en känd molekyl händer ingenting — ingen "Den finns inte"-text visas förrän zonen töms manuellt.
**Workaround i nuvarande version:** Zonen kan ha max 5 atomer; barnet klickar bort och försöker igen. Feedback-text saknas dock.
**Lösning till nästa iteration:** Lägg till kontroll: om total ≥ 4 och ingen känd molekyl matchas → visa "Den finns inte — prova en annan kombination!" och autoåterställ efter 1.5s.

---

## Ny princip?

### Signal till principer.md: Faktagranskning för naturvetenskap

**Observation:** För appar med ämnesinnehåll (kemi, fysik, biologi) finns risk att Claude designar med "ungefär rätt" fakta som saknar viktiga nyanser. Exempelfall här: väte + syre kräver aktiveringsenergi.

**Föreslagen tillägg till principer.md (under Flöde 1, steg 4):**

> **Naturvetenskap-regel:** För appar med faktainnehåll — Perplexity-research är inte valfritt. Verifiera alltid: (1) är det vetenskapligt korrekt på rätt abstraktionsnivå? (2) finns det en vanlig felintuitition hos barn som appen riskerar förstärka?

**Föreslagen tillägg till design.md-mallen (under "Vad appen INTE gör"):**

> Lägg alltid till: "Vilket nästa steg i ämnet *utelämnas* medvetet, och varför är det lämpligt för denna åldersgrupp?"

### Signal till kemi-3-design: Reaktioner behöver energi

Kemi-3 bör ha "aktiveringsenergi" som ett av sina koncept — att atomer inte automatiskt reagerar, utan behöver en knuff (ljus, värme, gnista). Detta bygger rätt intuition ovanpå kemi-2.

---

## Sammantagen bedömning

Appen uppfyller sitt lärandemål: *atomer kan binda ihop sig till molekyler med nya egenskaper*. Den vetenskapliga förenklingen (inga aktiveringsenergi) är åldersmässigt försvarbar men borde ha dokumenterats. Steg 5 har ett mindre UX-hål (ingen feedback vid ogiltig kombination) som bör fixas innan appen används regelbundet.
