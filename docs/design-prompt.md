# Mall: Generera design.md för en barnlärapp

Använd denna mall när du (Opus) skriver en design.md. Läs alltid `docs/principer.md` först — designen måste följa principerna.

---

## INPUT

**Appen ska handla om:**
[BRIEF — beskriv konceptet, lärandemålet, ev. interaktionsidé]

**Målgrupp:** [ÅLDER, t.ex. "8–9 år"]

**Research-underlag (om det finns):**
[Klistra in ev. svar från NotebookLM/Perplexity, annars skriv "inget"]

---

## INSTRUKTIONER

Producera en `design.md` med exakt dessa sektioner. Inga vaga formuleringar — varje beslut ska vara så konkret att en kodare kan implementera utan att fråga.

Referera till `docs/principer.md` för:
- Språknivå/LIX per ålder (princip C)
- Touch target-storlekar per ålder (princip G)
- CRA-progression (princip F)
- Scaffolding-regler (princip E)

---

## SEKTIONER I design.md

### Prerequisite-analys
Lista varje koncept appen förutsätter. För varje koncept:
- **Koncept:** [vad barnet måste förstå innan]
- **Täcks av:** [app-id från index.yaml] eller **Saknas** → [förslag på app att bygga först]

Om ett prerequisite saknas: designa INTE vidare förrän prerequisite-appen finns (eller ett aktivt beslut tagits att hoppa över, med motivering).

### Misconceptions (obligatoriskt för naturvetenskap)
Hämta kända misconceptions från `docs/misconceptions-register.md`. Lista de som är relevanta för denna modul:
- **Misconception:** [vad barnet troligen tror]
- **Adresseras i steg:** [nummer] — **Hur:** [kort beskrivning]
- **Risk att förstärka:** [ja/nej] — om ja, beskriv skyddsåtgärd

Nya misconceptions som identifierats via Perplexity/NotebookLM → lägg till i registret.

### Lärandemål
Ett enda, mätbart lärandemål. Formulera som: "Eleven ska förstå att X, inte Y."

### Målgrupp och enhet
- Ålder:
- Primär enhet (mobil/iPad/laptop):
- Touch target-storlek (px):

### Visuella variabler (obligatoriskt)
Deklarera varje visuell variabel som bär information i modulen. Variabeln ska användas konsekvent genom alla steg — om den ändrar betydelse mellan steg, deklarera det explicit.

| Variabel | Representerar | Konsekvent i hela modulen? |
|---|---|---|
| [t.ex. Piltjocklek] | [t.ex. kraft — alltid lika i bägge riktningar] | [Ja/Nej + förklaring] |
| [t.ex. Animationshastighet] | [t.ex. rörelseeffekt/acceleration] | [Ja/Nej + förklaring] |
| [t.ex. Storlek] | [t.ex. massa] | [Ja/Nej + förklaring] |

### Sessionsstruktur
Lista varje skärm/steg i ordning. För varje steg:
- **Steg N — [namn]**
  - Do-komponent (vad gör eleven aktivt?):
  - CRA-nivå (Konkret / Representationell / Abstrakt):
  - Layout (beskriv i ord var elementen ligger, t.ex. "tre bollar i rad, drag-zone under"):
  - Text på skärmen (**slutgiltig kopia** — skriv ut exakt vad som ska stå. Detta är låst text som kopieras ordagrant vid implementation. Ingen parafrasering tillåten. Använd barnets ordförråd direkt. Max enligt ålderstabellen i principer.md):
  - Interaktionstyp (tap / drag / slider / etc.):
  - Visuell feedback vid rätt svar:
  - Visuell feedback vid fel svar:
  - **Kontraintuitivt moment?** Om ja → markera med ⚡ och beskriv prediction-steg (gissning → utfall → förklaring)

### Guided challenge (steg 1)
Beskriv exakt hur appen börjar med en utmaning INNAN förklaring.
Vardagsförankring: vilken vardagsupplevelse kopplas till?

### Scaffolding-nivåer
Beskriv vad som händer vid:
- Fel 1:
- Fel 2:
- Fel 3 (full scaffold):

### Gate-keeping
Vilka steg kräver rätt svar innan eleven går vidare? (Inte steg 1.)

### Konsolidering (sista steget)
- Hur sammanfattas det barnet lärt sig?
- Återkoppling till guided challenge i steg 1?
- Reflektionsfråga (flerval/visuellt val, aldrig textfält):

### Metakognition
- Hur visas framsteg? (Karta/stegindikator, inte poäng)
- Lärandemål: visas riktning i början, full återkoppling i slutet

### Responsivt beteende
- Mobilvy (8"): vad ändras jämfört med baslayout?
- Surfplatta (13"): baslayout
- Laptop (16"): vad kan läggas till?

### Auditory icons
Lista ljud-händelser och karaktär (kort/mjukt/skarpt):
- Rätt svar:
- Fel svar:
- Progression (går till nästa steg):

### Tekniska beslut
- Vanilla JS eller React (motivera):
- Animationer (lista konkret vad som animeras):
- Rörliga targets? Nej (om inte starkt motiverat):

### Developmental progression-check (obligatorisk)
Gå igenom stegen i sekvens. Kontrollera för varje stegpar (N → N+1):

**Kontroll 1 — Ett koncept per steg:**
- Introducerar steg N+1 ett koncept som inte etablerats i steg N eller tidigare?
- Om ja → lägg till ett mellansteg som bygger bryggan.

**Kontroll 2 — Begreppskontroll (inga odefinierade ord):**
- Använder steg N+1 ett ord, en metafor eller en visuell representation som inte *definierats genom handling* i ett tidigare steg?
- "Definierad genom handling" = barnet har själv gjort något som etablerar ordets betydelse (tryckt, dragit, sett resultatet). Att bara ha läst ordet i en text räknas inte.
- Om ja → lägg till ett steg där begreppet *upplevs* innan det *nämns*.
- **Vanliga fällor:** "knuff" (definieras genom att barnet knuffar), "kedja/rad" (definieras genom att barnet ser delar i rad), "granne" (definieras genom att barnet ser atomer sida vid sida), materialegenskaper (definieras genom att barnet jämför).

**Kontroll 3 — Visuell kontext:**
- Förutsätter steg N+1 att barnet tolkar en visuell variabel (t.ex. en zon, en form, en färg) som inte introducerats explicit? Om barnet ser "en djup skål" måste skålformen ha visats i ett tidigare steg — den får inte dyka upp för första gången samtidigt som den bär information.

**Tumregel:** Varje steg ska introducera maximalt *ett* nytt koncept. Varje begrepp ska definieras genom handling, inte genom text. Om ett steg kräver att barnet gör två kognitiva språng samtidigt, saknas ett mellansteg.

### Stealth assessment (obligatoriskt)
Lista 3–5 datapunkter att samla in utan att barnet märker det:
- Vad mäts (t.ex. "gissning i prediction-steg")?
- Vad indikerar det (t.ex. "bär på misconception X")?
- I vilket steg?

### Vad appen INTE gör
Lista 3–5 saker som medvetet utelämnats och varför.
Inkludera alltid: "Vilket nästa steg i ämnet utelämnas medvetet, och varför är det lämpligt för denna åldersgrupp?"
