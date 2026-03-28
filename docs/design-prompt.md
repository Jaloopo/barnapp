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

### Lärandemål
Ett enda, mätbart lärandemål. Formulera som: "Eleven ska förstå att X, inte Y."

### Målgrupp och enhet
- Ålder:
- Primär enhet (mobil/iPad/laptop):
- Touch target-storlek (px):

### Sessionsstruktur
Lista varje skärm/steg i ordning. För varje steg:
- **Steg N — [namn]**
  - Do-komponent (vad gör eleven aktivt?):
  - CRA-nivå (Konkret / Representationell / Abstrakt):
  - Layout (beskriv i ord var elementen ligger, t.ex. "tre bollar i rad, drag-zone under"):
  - Text på skärmen (skriv ut exakt, max enligt ålderstabellen i principer.md):
  - Interaktionstyp (tap / drag / slider / etc.):
  - Visuell feedback vid rätt svar:
  - Visuell feedback vid fel svar:

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

### Vad appen INTE gör
Lista 3–5 saker som medvetet utelämnats och varför.
