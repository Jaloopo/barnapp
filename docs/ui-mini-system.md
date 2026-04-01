# UI Mini-System — Barnapp

Detta dokument beskriver den lilla visuella baseline som nu används på startsidan i `docs/index.html`.

Syftet är inte att låsa hela projektet, utan att ge en stabil gemensam grund för nya moduler och framtida polish-pass.

## 1. Karaktär

- Varm, lugn och vänlig
- Barnvänlig utan att bli babyaktig
- Tydlig och förutsägbar snarare än spelig
- Taktil och polerad, men återhållsam

Kort sagt: tänk "välgjord lärmiljö" snarare än "app store", "spel" eller "dashboard".

## 2. Basprinciper

- Enkel struktur först. Barnet ska snabbt förstå var man är och vad man kan trycka på.
- En tydlig visuell familj. Liknande kort och paneler ska kännas som delar av samma system.
- Färg används främst för ämnesidentitet och vägledning, inte som dekoration.
- Prominence ska vara subtil. Startpunkt eller rekommenderad väg får lyftas fram, men inte genom ett helt annat komponentmönster.
- Kommande innehåll visas lugnt och tydligt, utan badges eller "produktstatusspråk".

## 3. Visuella byggstenar

### Typografi

- Huvudfont: `Nunito`
- Vikter som används nu: `600`, `700`, `800`
- Rubriker: mjukt rundad sans-serif, tydlig men inte lekfull på ett överdrivet sätt
- Brödtext: kort, varm och lättläst

### Basfärger

- Bakgrund: `#faf5ee`
- Djupare bakgrundston: `#f3eadf`
- Yta: `#fffdfa`
- Mjuk yta: `#fff8f1`
- Kant: `#e6d8c6`
- Primär text: `#2d241d`
- Dämpad text: `#6f6256`

### Ämnesfärger

- Kemi:
  - accent `#c86252`
  - mjuk accent `#f5dfd9`
  - accenttext `#9d4a3b`
- Elektricitet:
  - accent `#d2a32a`
  - mjuk accent `#f7ebc8`
  - accenttext `#8e6c13`
- Fysik:
  - accent `#4f84c4`
  - mjuk accent `#dfeafb`
  - accenttext `#315f97`
- Astronomi:
  - accent `#8660c9`
  - mjuk accent `#e9e0f8`
  - accenttext `#6247a2`

## 4. Layoutregler

- Standardbredd för lugna innehållssidor: cirka `700px`
- Enkolumnslayout är default för översikter och listor
- Luft ska kännas generös, men inte tom
- Rubrik och undertitel centreras på landningssidan
- Ämnesgrupper får egen etikett i versaler med respektive ämnesaccent

Två kolumner kan användas senare när innehållet verkligen kräver det, men ska inte vara default för barnets första överblick.

## 5. Kortsystem

### Standardkort

- Rundade hörn runt `20px`
- Ljus, varm panel med lätt gradient
- Tunn neutral kant
- Mjuk skugga
- Färgad vänsteraccent som huvudmarkör för ämne
- Ikonbricka i ämnets mjuka accentfärg
- Innehållsordning:
  1. titel
  2. kort beskrivning
  3. eventuell kort notis

### Featured-kort

Används sparsamt, till exempel för första rekommenderade startpunkt.

- Samma komponent som vanliga kort
- Lite starkare skugga
- Lite mer padding
- Marginellt kraftigare accent
- Ingen pil, badge eller separat specialgrafik

### Upcoming-kort

Används för innehåll som ännu inte går att öppna.

- Ingen länk
- Nedtonat uttryck
- Ingen badge
- Status skrivs i kortets text, till exempel `Kommer snart`

## 6. Språk på UI-nivå

- Skriv varmt, kort och konkret
- Undvik produkt- eller projektstatusspråk som `klar`, `byggd`, `design` som primära UI-element för barnet
- Föredra barnnära vägledning som:
  - `Börja här om du är ny.`
  - `Kommer snart`
- Texten ska hjälpa barnet att välja nästa steg, inte förklara utvecklingsstatus

## 7. Vad kommande moduler kan återanvända

Nya moduler behöver inte se exakt ut som startsidan, men bör gärna återanvända:

- varm bakgrundston
- `Nunito`
- rundade paneler/kort
- mjuka skuggor
- ämnesfärg som accent
- korta beskrivningar och tydlig hierarki

När en modul blir mer interaktiv får den gärna vara mer levande än startsidan, men den bör fortfarande kännas som samma produktfamilj.

## 8. Undvik

- badges som standardmönster
- pilar och handritade "börja här"-markörer
- dekorativa blobbar utan semantisk funktion
- app-store-känsla
- spelifiering som primär ton
- hård asymmetri eller stökiga grid-layouter
- kalla, tekniska blåvita miljöer
- alltför många visuella signaler samtidigt

## 9. Status

Detta är en praktisk baseline, inte ett slutgiltigt designsystem.

Om flera nya moduler börjar återanvända samma mönster kan detta senare växa till ett större systemdokument med fler komponenter, states och exempel.
