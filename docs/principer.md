# Designprinciper för barnläroappar (A–I)
*Referensdokument — läses av Claude Code vid bygge*

---

**Prioriteringsordning vid konflikter:** A > C > E > B > D > F–I.

---

## A. KÄRNARKITEKTUR — Sessionssekvens

*Kognitiv belastning styr allt — överlasta aldrig arbetsminnet.*

1. **Guided challenge först** — Förutsägelse eller kort utmaning *innan* konceptet förklaras
   - **Vardagsförankring obligatorisk:** Mönster: vardagserfarenhet → fråga → koncept. Nytt innehåll utan koppling till barnets schema förblir abstrakt.
   - Barn 6–10: guided prediction, contrasting cases, eller vicarious failure
   - **Alltid** avsluta med konsolidering efteråt
2. **Ett koncept per skärm** — Max 2–5 min per mikrosteg
3. **Scaffolding i designen** — Affordances, constraints, visuella ledtrådar. Inte textblock. Fasa ut gradvis.
4. **Fri utforskning sist** — Guided discovery, aldrig ostrukturerad free play
5. **Blanda och repetera** — Varva problemtyper

**Ett lärandemål per session. 5–15 minuter total längd.**

### Prerequisite-analys (obligatorisk)

Innan design påbörjas: kartlägg vilka koncept appen *förutsätter* att barnet redan förstår. Kontrollera mot `index.yaml` om det finns en app som täcker varje prerequisite-koncept.

**Tumregel:** Om ett konceptsteg hoppas över (t.ex. "atomer → ström" utan att barnet förstår elektroner, eller "fusion" utan gravitation) saknas en prerequisite-app. Bygg den först.

**Lärdomen:** el-1-ledare förutsatte att barnet visste vad elektroner var och att de rör sig — men kemi-1-atomer lärde bara ut protoner. astro-1-fusion sa "hettan pressar ihop" utan att förklara varifrån trycket kom (gravitation). Båda hade osynliga prerequisite-luckor som märktes först vid barntest.

### Faktagranskning för naturvetenskap (obligatorisk)

För appar med ämnesinnehåll (kemi, fysik, biologi, astronomi): Perplexity-research i design-fasen är **inte valfritt**. Verifiera alltid:
1. Är det vetenskapligt korrekt på rätt abstraktionsnivå?
2. Finns det en vanlig felintuition hos barn som appen riskerar förstärka?
3. Vilket nästa steg i ämnet utelämnas medvetet — och dokumentera det i design.md under "Vad appen INTE gör".

*Lärdomen: "väte och syre reagerar kemiskt" ≠ "de blandas". Appen kan vara åldersmässigt förenklad, men förenklingen ska vara ett aktivt val, inte en miss.*

---

## B. INTERAKTIVITETSDESIGN

*Att göra har ~6x större läreffekt än att läsa.*

- Varje skärm: en **do-komponent** — eleven genererar, förutsäger, bygger eller förklarar
- **Miniminivå: Constructive** — inte bara klicka/dra
- Direkt visuell feedback < 300ms
- Implicit scaffolding: stödet i designen, inte i instruktioner
- **Ljud:** Auditory icons (poppande, klickande) — inte earcons eller bakgrundsmusik. Talad feedback stödjer lärande via modalitetsprincipen.

---

## C. VISUELL DESIGN — Mayers principer

*Irrelevant information konkurrerar aktivt med lärande.*

- **Coherence:** Ta bort allt som inte tjänar lärandemålet
- **Spatial contiguity:** Text *precis intill* det den beskriver. Visuell feedback före text.
- **Signaling:** Pilar, highlight, färg — sparsamt
- **Segmenting:** Eleven styr takten, aldrig auto-progression
- **Redundancy:** Ej identisk info i text + ljud + bild samtidigt. Undantag: kort text + ljud OK för 6–7 år.
- **Pre-training:** Nyckelbegrepp innan huvudinnehåll
- **Personalization:** Konversationell ton ("du"), värme
- Max 3–4 val per skärm

**Språknivå per ålder (LIX):**

| Ålder | LIX | Max ord/mening | Max ord/skärm |
|-------|-----|----------------|---------------|
| 6–7 år | 10–20 | 5–7 | 50–100 |
| 7–9 år | 15–25 | 8–10 | 100–200 |
| 9–10 år | 20–30 | 10–12 | 200–500 |
| 10–12 år | 25–35 | 12–15 | 500–1 000 |

Barn 6–8: inga bisatser, inga passiva former, inga facktermer utan bildstöd, max ett instruktionssteg per mening.

**Metafor-regel:** Undvik abstrakta liknelser. Test: kan en 7-åring rita det? Animationen agerar metafor — texten ska vara bokstavlig.

**Expertise Reversal:** Minska scaffolding när eleven visar förståelse.

**Seductive details:** Lekfullhet OK om separerat från lärinnehållet.

---

## D. MOTIVATION — Self-Determination Theory

- **Autonomi:** Meningsfulla val om *hur* eleven utforskar
- **Kompetens:** Optimal utmaning + informativ feedback ("Du hittade mönstret!" — inte "Rätt!")
- **Tillhörighet:** Värme i systemets röst

Designa för nyfikenhet. Fail state: "Intressant! Vad hände?" — aldrig poängavdrag.

---

## E. FORMATIV BEDÖMNING

*Bedömning genom handlingar, inte testfrågor.*

- **Stealth assessment:** Spåra antal försök, feltyper (systematiska = misconception), tid per steg
- **Adaptionsregel:** Fel 1 → visuell markering. Fel 2 → delvis ledtråd. Fel 3 → fullständig scaffold.
- **Kombinerad feedback:** Motiverande + förklarande + nivåanpassning — alla tre krävs.
- **Gate-keeping:** Demonstrera förståelse innan nästa moment — som utforskning, inte test. Gäller INTE under guided challenge (A1).
- **Maskot-feedback** för barn ("Björnen ser förvirrad ut — prova igen?")

---

## F. CRA-PROGRESSION (Konkret → Abstrakt)

**Sträva efter simultan CRA** (konkret + representationellt + abstrakt samtidigt).

**Om inte möjligt (liten skärm):**
1. Micro-steps med elevkontroll
2. Partiell synlighet / concreteness fading
3. Animerad övergång
4. Verbal brygga

**Facktermsregel:** Formella termer kräver tre steg: (1) konkret upplevelse → (2) koppling till vardag → (3) termen som etikett. Termen är ett namn på något barnet redan förstår.

| Domän | Konkret | Representationellt | Abstrakt |
|---|---|---|---|
| Fysik | Dra/skjuta objekt | Kraftpilar | Newtons lagar |
| Kemi | Färgade bollar | Strukturformler | Periodsystemet |
| Ekosystem | Animerade populationer | Flödesschema | Energikedjor |
| Programmering | Block-kod | Flödesdiagram | Textbaserad kod |

---

## G. BARN — Interaktion och skärm

**Motorisk progression:**

| Ålder | Primär interaktion | Tekniska krav |
|-------|-------------------|---------------|
| 6–7 | Tap/tryck | Target ≥ 60×60 px, acceptera slir-drag |
| 7–8 | Tap + enkel slider | Stort handtag, begränsad räckvidd |
| 8–9 | Drag-and-drop | Target ≥ 80×80 px, snap-to-zone, space-making |
| 9–12 | Alla gester | Kan hantera precision |

Kritiska ytor centralt eller i botten. Inga blink > 3/sek. Inga tidsgränser.

**Skärmanpassning:**

| Enhet | Strategi |
|-------|---------|
| 8" mobil | Sekventiell CRA, en interaktion per vy, talad instruktion |
| 13–14" iPad | Simultant konkret + representationellt, sidopanel, drag-and-drop |
| 16" MacBook | Full CRA-triad, hover-states, detaljrika animationer |

**Dual-layer:** Fungerar ensam MEN designad för samspel. Motorik = barnet. Kontext = vuxen. "Fråga en vuxen"-prompts vid nyckelpunkter.

Variera knappposition mellan steg (holdover-effekt).

---

## H. METAKOGNITION

- Reflect: flerval/visuellt val — aldrig textfält
- Lärandemål: visa riktning i början, fullständig återkoppling i slutet
- Framsteg som karta, inte poängsystem

---

## I. TRANSFER & EMBODIED COGNITION

- Varied practice: samma koncept i olika kontexter
- Embodied interaction: gester som känns som konceptet
- Space-making vid drag-and-drop

---

## TRADE-OFF-REGLER

| Konflikt | Regel |
|---|---|
| Text ↔ Feedback | Visuell feedback + auditory icon först. Text som komplement. Barn 6–8: ljud/maskot. |
| Fri utforskning ↔ Fast sekvens | Barn < 8: fast sekvens. Fri lek som bonus efter grundsekvens. |
| Simultan CRA ↔ Liten skärm | Micro-steps + partiell synlighet + verbal brygga. |

---

## UNDVIK ALLTID
- Linjär text+bild (lärobok, inte app)
- Poängsystem/stjärnor som primär motivator
- Passiva animationer utan interaktion
- Auto-progression
- Textfält för barns reflektion
- Bakgrundsmusik
- Animationer som blockerar input

---

## FAKTAGRANSKNING — Naturvetenskap

**Naturvetenskap-regel:** För appar med faktainnehåll (kemi, fysik, biologi) — Perplexity-research är inte valfritt. Verifiera alltid:
1. Är det vetenskapligt korrekt på rätt abstraktionsnivå?
2. Finns det en vanlig felintuition hos barn som appen riskerar förstärka?
3. Vilka förenklingar görs medvetet — och varför är de försvarbara för åldersgruppen?

Dokumentera förenklingar explicit i design.md under "Vad appen INTE gör".
