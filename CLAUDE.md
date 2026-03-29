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

## Flöden

### 1. Idé → Design (Opus)
Trigger: användaren ger en idé, t.ex. "barnet vill lära sig om stjärnor"

1. Läs `docs/index.yaml` — vad har barnet gjort? Vilka koncept är upplåsta?
2. Föreslå 2–3 vägar med bryggor från tidigare appar
3. Användaren väljer väg
4. **Prerequisite-analys (obligatorisk):**
   - Vilka koncept *förutsätter* den nya appen att barnet redan förstår?
   - Finns det en befintlig app i index.yaml som täcker varje prerequisite-koncept?
   - Om ett prerequisite-koncept saknas → föreslå att den modulen byggs först
   - Dokumentera analysen explicit: "Appen förutsätter X. Täcks av [app-id] / Saknas → bygga [förslag] först."
   - **Tumregel:** Om mer än ett konceptsteg hoppas över (t.ex. "atomer → ström" utan "elektroner") saknas en prerequisite-app.
5. Bedöm research-behov:
   - 🟢 **Klarar mig** — principer.md + index + tidigare reviews räcker
   - 🟡 **Perplexity rekommenderas** — sakfakta jag är osäker på → ge färdig prompt
   - 🔴 **NotebookLM rekommenderas** — pedagogisk fråga utan stöd i principer.md → ge färdig prompt
6. Om research: användaren klistrar svar, annars gå vidare
7. Läs `docs/principer.md` + designmallen i `docs/design-prompt.md`
8. Skriv `design.md` i rätt mapp (`docs/[ämne]/[ämne]-[nr]-[slug]/design.md`)
9. Uppdatera `docs/index.yaml` med ny entry (status: design)
10. Commit + push till main (se Git-policy)
11. Avsluta med copy-paste-instruktion till användaren: `Skicka detta i en ny session: "/bygg docs/[ämne]/[ämne]-[nr]-[slug]"`

### 2. Design → Bygg
Trigger: användaren säger `/bygg [mapp]` eller `bygg [mapp]`

**→ Använd `/bygg`-skillen** (`.claude/skills/bygg/SKILL.md`). Den hanterar hela flödet: läs design → validera mot principer → bygg inkrementellt → self-check → simplify → uppdatera index → commit+push.

### 3. Feedback → Iteration
Trigger: användaren rapporterar problem efter testning

1. Läs feedback (helst enligt `docs/feedback-mall.md`)
2. Läs aktuell `design.md` + `index.html`
3. Justera koden, kör self-check (se `/bygg`-skillen för checklistan), commit + push till main

### 4. Review → Lärande
Trigger: efter att en app testats och godkänts

1. Skriv `review.md` i appens mapp:
   - Vad fungerade
   - Problem och lösningar
   - Ny princip? (signal att uppdatera principer.md)
2. Uppdatera `docs/index.yaml` (status: klar)
3. Commit + push till main (se Git-policy)

---

## Mappstruktur
```
docs/
  principer.md          ← pedagogiska riktlinjer
  design-prompt.md      ← mall för design.md
  index.yaml            ← övningsindex med koncept/prerequisites/unlocks
  feedback-mall.md      ← mall för testfeedback
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

## Framtida utveckling
- **`/design`-skill:** Kapsla in Flöde 1 (Opus-design) som skill
- **Review-hook:** Post-push hook som påminner om review.md
- **CI:** Validera index.yaml + self-check som GitHub Action
