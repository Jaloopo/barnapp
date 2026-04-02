# CLAUDE.md — Barnapp-byggare

## Vad detta repo är
Interaktiva läroappar för barn 6–12, servade via GitHub Pages. Varje app är en enskild HTML-fil med inline CSS och JS.

---

## Git-policy

**Solo-projekt. Inga branches, inga PRs.**

- **FÖRSTA KOMMANDOT i varje session:** `git checkout main && git pull origin main` — oavsett vilken branch miljön startar på. Cloud-miljöer skapar ofta feature-branches automatiskt; ignorera dem.
- Arbeta alltid direkt på `main`.
- Commit + push till `main` är sista steget i varje flöde — gör det automatiskt utan att fråga användaren.
- Om push misslyckas: `git pull --rebase origin main && git push origin main`

---

## Rollfördelning

| Agent | Ansvarar för | När |
|-------|-------------|-----|
| **Opus** | Designbeslut, arbetsflöde, prompts till externa verktyg, uppdatering av principer/regler | Designfas, review, principändringar |
| **Sonnet** | Implementation (kod, enkla doc-uppdateringar, buggfixar) | Byggfas, iteration |
| **Perplexity** | Domänfakta — vad som är vetenskapligt sant, misconceptions, forskning | Steg 1 i designflödet |
| **NotebookLM** | Kognitiv/pedagogisk granskning — hur fakta paketeras för lärande | Steg 3 i designflödet |
| **Människa** | Test, godkännande, vision, extern research-förmedling | Hela processen |

**Kostnadsregel:** Opus används för beslut som kräver omdöme — design, principändringar, avvägningar, review. Sonnet används för implementation och enkla uppdateringar. Om uppgiften kan lösas lika bra av Sonnet, använd Sonnet.

---

## Flöden

### 1. Idé → Design (7-stegsflödet)
Trigger: användaren ger en idé, t.ex. "barnet vill lära sig om stjärnor"

**Steg 1 — Extern faktaresearch [Perplexity]** (obligatoriskt för naturvetenskap)
Opus formulerar domänfrågor och ger användaren en färdig prompt:
- Vilka misconceptions har barn X år om konceptet?
- Vilken forskning finns om effektiva vardagsexempel?
- Vilka förenklingar är försvarbara vs. skapar seglivade fel?
- Korsreferera mot `docs/misconceptions-register.md`

**Steg 2 — Preliminär modulplan [Opus]**
1. Läs `docs/index.yaml` — vad har barnet gjort? Vilka koncept är upplåsta?
2. Föreslå 2–3 vägar med bryggor från tidigare appar
3. Användaren väljer väg
4. **Prerequisite-analys (obligatorisk):**
   - Vilka koncept *förutsätter* den nya appen att barnet redan förstår?
   - Finns det en befintlig app i index.yaml som täcker varje prerequisite-koncept?
   - Om ett prerequisite-koncept saknas → föreslå att den modulen byggs först
   - **Tumregel:** Om mer än ett konceptsteg hoppas över saknas en prerequisite-app.
5. **Developmental progression-check:** Kontrollera att varje steg i planen maximalt introducerar *ett* nytt koncept. Om ett steg förutsätter en insikt som inte etablerats i föregående steg — lägg till ett mellansteg.
6. Lista övningar/steg + lärandemål per steg (inte fullständigt designdokument ännu)

**Steg 3 — Kognitiv/pedagogisk granskning [NotebookLM]** (pre-flight check)
Opus formulerar en prompt och ger användaren. Obligatorisk input: preliminärplan + `docs/misconceptions-register.md`. Prompten frågar:
1. Vilka naïve theories har barn om detta, och hur ska visualiseringen korrigera snarare än förstärka dem?
2. Finns steg som bryter mot Mayers multimediaprinciper (Spatial Contiguity, Coherence, Temporal Contiguity)?
3. Hur kan stealth assessment byggas in?
4. Saknas något developmental progression-steg?

**Steg 4 — Kompletterande research [Perplexity, vid behov]**
Om NotebookLM identifierar frågor utanför sitt corpus.

**Steg 5 — Fullständigt designdokument [Opus]**
1. Läs `docs/principer.md` + `docs/design-prompt.md` (+ `docs/ui-mini-system.md` när designen påverkar gemensamma UI-mönster eller landing page)
2. Sammanväg Perplexity + NotebookLM-svar
3. Skriv `design.md` i rätt mapp (`docs/[ämne]/[ämne]-[nr]-[slug]/design.md`)
   - Inkludera obligatorisk tabell: **Visuella variabler**
   - Markera kontraintuitiva moment med **prediction-steg**
4. **Språkgranskning av skärmtexter (obligatorisk gate innan commit):**
   Opus samlar alla "Text på skärmen"-fält och feedbacktexter ur design.md och formulerar prompter till användaren:
   - **Perplexity-prompt:** "Vilka av dessa formuleringar är sannolikt svåra för ett barn på [ålder] att förstå? Föreslå enklare alternativ. Följande fackord används medvetet och ska behållas: [lista]."
   - **NotebookLM-prompt:** "Bryter någon av dessa texter mot Mayers Coherence-, Spatial Contiguity- eller Temporal Contiguity-princip? Finns formuleringar som riskerar att förstärka naïva teorier om [ämne]?"
   - Opus reviderar texterna i design.md baserat på svaren. Texterna i design.md är sedan **låst kopia** som kopieras ordagrant vid implementation.
5. Uppdatera `docs/index.yaml` med ny entry (status: design)
6. Uppdatera `docs/misconceptions-register.md` med nya entries
7. Commit + push till main

**Review-gate före implementation**
När en moduldesign kommer från Codex, och alltid för prerequisite-moduler eller moduler med tydliga kontraintuitiva moment, gör en kort Opus-review innan Steg 6 (implementation).

**Steg 6 — Implementation [Sonnet]**
Avsluta med copy-paste-instruktion: `Skicka detta i en ny session: "/bygg docs/[ämne]/[ämne]-[nr]-[slug]"`

**Steg 7 — Test + buggrapport [Människa]**
Rapport enligt `docs/feedback-mall.md` → Opus tar beslut om justering.

### 2. Design → Bygg (Sonnet)
Trigger: användaren säger `/bygg [mapp]` eller `bygg [mapp]`

**→ Använd `/bygg`-skillen** (`.claude/skills/bygg/SKILL.md`). Den hanterar hela flödet: läs design → validera mot principer → bygg inkrementellt → self-check → simplify → uppdatera index + landningssida → commit+push.
Vid visuellt arbete som ska följa repots gemensamma baseline: läs också `docs/ui-mini-system.md`.

### 3. Feedback → Iteration (Sonnet, Opus vid designfrågor)
Trigger: användaren rapporterar problem efter testning

1. Läs feedback (helst enligt `docs/feedback-mall.md`)
2. Läs aktuell `design.md` + `index.html`
3. **Sonnet** fixar buggar och implementationsfel
4. **Opus** kallas in om feedbacken avslöjar designproblem (felaktig visuell semantik, saknade steg, misconception-risker)
5. Kör self-check (se `/bygg`-skillen för checklistan), commit + push till main

### 4. Review → Lärande (Opus)
Trigger: efter att en app testats och godkänts

1. Skriv `review.md` i appens mapp:
   - Vad fungerade
   - Problem och lösningar
   - Ny princip? (signal att uppdatera principer.md)
2. Uppdatera `docs/misconceptions-register.md` med lärdomar
3. Uppdatera `docs/index.yaml` (status: klar)
4. Commit + push till main (se Git-policy)

---

## Mappstruktur
```
docs/
  principer.md              ← pedagogiska riktlinjer
  design-prompt.md          ← mall för design.md
  ui-mini-system.md         ← liten visuell baseline för startsida och kommande moduler
  index.yaml                ← övningsindex med koncept/prerequisites/unlocks
  feedback-mall.md          ← mall för testfeedback
  misconceptions-register.md ← kända naïve theories per ämne (obligatorisk input i steg 3)
  [ämne]/
    [ämne]-[nr]-[slug]/
      design.md         ← skrivs i flöde 1
      index.html        ← byggs i flöde 2
      review.md         ← skrivs i flöde 4
```
GitHub Pages serverar från `docs/`. App-URL: `https://jaloopo.github.io/barnapp/[ämne]/[ämne]-[nr]-[slug]/`

---

## Skills

| Skill | Syfte |
|-------|-------|
| `/bygg` | Bygger index.html från design.md — hela Flöde 2 |
| `barnapp-design` | Visuellt designsystem för barnappar (överstyr frontend-design) |
| `frontend-design` | Anti-AI-slop baseline (officiell Anthropic-skill) |
| `/simplify` | Kodkvalitet-pass efter bygge (inbyggd) |

Skills ligger i `.claude/skills/`. `barnapp-design` och `frontend-design` aktiveras automatiskt vid bygge. `/bygg` triggas av användaren.

---

## Tekniska regler

**Format:** En enda HTML-fil. CSS och JS inline. Inga externa beroenden utom Google Fonts via CDN.

**Välj rätt verktyg:**
- Vanilla HTML/JS för enkla appar (en interaktionstyp)
- React via CDN (unpkg) om appen har komplex state (quiz-träd, dynamisk scaffolding)

**Feature-prioritetsordning** (om filen växer förbi ~500 rader):
1. Interaktionslogik (kärnan)
2. Visuell feedback (färg, animation)
3. Scaffolding-nivåer
4. Ljud (auditory icons via Web Audio API)
5. Stealth assessment-datainsamling

**Tekniska constraints:**
- Web Audio API för auditory icons (korta ljud, inga melodier)
- Drag-and-drop: HTML5 Pointer Events, undvik tunga bibliotek
- Touch targets: minimum 44×44 CSS px (WCAG), gärna 60–80 px för barn
- Inga element blinkar > 3 ggr/sek
- Animationer avbrytbara — blockera inte input under animation
- Respektera `prefers-reduced-motion`
- localStorage tillåtet — wrappa i try/catch (privat surfning kan blocka)

**Byggordning:** Se `/bygg`-skillen — skriv ALDRIG hela index.html i ett enda Write-anrop.

---

## Parallellt arbete med Codex

Detta repo används av både Claude Code och Codex. Reglerna:

- **`docs/` är enda källan till sanning** för innehåll och regler (`principer.md`, `design-prompt.md`, `ui-mini-system.md`, `index.yaml`, `misconceptions-register.md`, `feedback-mall.md`, alla `design.md`/`index.html`/`review.md`)
- **CLAUDE.md och AGENTS.md är separata adapterlager** — de innehåller verktygsspecifika instruktioner. Ändra aldrig det andra verktygets filer utan anledning.
- **Vid ändring av gemensamma dokument** (`docs/principer.md`, `docs/design-prompt.md`, `docs/ui-mini-system.md`, skill-innehåll): uppdatera båda adapterlagren i samma commit om de påverkas.
- **Skill-spegling:** Tillåtna skillnader mellan `.claude/skills/` och `.agents/skills/` är metadata, verktygssyntax och lätt språkjustering. Inga workflow-skillnader utan uttryckligt beslut i `CLAUDE.md`. Vid ändring uppdateras båda.
- **Börja alltid med `git pull`** — den andra agenten kan ha pushat.
- **Hooks är bekvämlighet, inte beroende.** Arbetsregler som gäller båda verktygen ska finnas som text i CLAUDE.md/AGENTS.md, inte bara i hook-automation.

---

## Externa workflow-verktyg (Superpowers m.fl.)

Agenter kan ha globala workflow-skills installerade (t.ex. `obra/superpowers`). Policy:

- **Repo-workflow har alltid företräde.** Barnappens flöden (Flöde 1–4), git-policy och mappstruktur gäller oavsett vilka globala skills som är installerade.
- **Superpowers är personligt overlay**, inte repots officiella workflow. Använd det som komplement där det inte krockar.
- **Rekommenderade skills:** `verification-before-completion`, `systematic-debugging`, `brainstorming` (endast för större designfrågor; det får inte dra vidare till `writing-plans`, worktrees eller branch-baserad execution när det krockar med repo-workflowet).
- **Använd inte i detta repo:** `using-git-worktrees`, `finishing-a-development-branch` (krockar med main-only), `writing-plans` som obligatoriskt steg (vi har design.md), `subagent-driven-development` som standard (överdimensionerat), `test-driven-development` som standard (ingen testinfrastruktur).

---

## Framtida utveckling
- **`/design`-skill:** Kapsla in Flöde 1 (7-stegsflödet) som skill — efter att flödet validerats manuellt i minst en modul
- **`/fix`-skill:** Kapsla in Flöde 3 (Feedback → Iteration)
- **`/review`-skill:** Kapsla in Flöde 4 (Review → Lärande) inkl. misconceptions-register-uppdatering
- **Review-hook:** Post-push hook som påminner om review.md
- **CI:** Validera index.yaml + self-check som GitHub Action
