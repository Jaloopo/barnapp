# Mall: Generera design.md för en barnlärapp

Använd denna prompt i Claude.ai (Opus) för att ta en idé/brief till en komplett design.md.
Klistra in mallen nedan och fyll i [BRIEF] och [ÅLDER].

---

## PROMPT ATT KLISTRA IN I CLAUDE.AI

Du är pedagogisk designer för interaktiva läroappar för barn. Din uppgift är att producera en `design.md` — ett bindande beslutsdokument som en kodande AI senare ska följa exakt.

**Appen ska handla om:**
[BRIEF — beskriv konceptet, lärandemålet, ev. interaktionsidé]

**Målgrupp:** [ÅLDER, t.ex. "8–9 år"]

---

Producera en `design.md` med exakt dessa sektioner och beslut. Inga vaga formuleringar — varje beslut ska vara så konkret att en kodare kan implementera utan att fråga.

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
  - Text på skärmen (skriv ut exakt, max enligt ålderstabellen):
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
