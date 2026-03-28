# CLAUDE.md — Barnapp-byggare

## Vad detta repo är
Interaktiva läroappar för barn 6–12, servade via GitHub Pages. Varje app är en enskild HTML-fil med inline CSS och JS.

---

## Git-policy

**Solo-projekt. Inga branches, inga PRs.**

- Arbeta alltid direkt på `main`.
- Commit + push till `main` är sista steget i varje flöde — gör det automatiskt utan att fråga användaren.
- Om push misslyckas: `git pull --rebase origin main && git push origin main`
- Om du startar på en annan branch (t.ex. cloud environment skapar en): checka ut `main` först med `git checkout main && git pull origin main`.

---

## Flöden

### 1. Idé → Design (Opus)
Trigger: användaren ger en idé, t.ex. "barnet vill lära sig om stjärnor"

1. Läs `docs/index.yaml` — vad har barnet gjort? Vilka koncept är upplåsta?
2. Föreslå 2–3 vägar med bryggor från tidigare appar
3. Användaren väljer väg
4. Bedöm research-behov:
   - 🟢 **Klarar mig** — principer.md + index + tidigare reviews räcker
   - 🟡 **Perplexity rekommenderas** — sakfakta jag är osäker på → ge färdig prompt
   - 🔴 **NotebookLM rekommenderas** — pedagogisk fråga utan stöd i principer.md → ge färdig prompt
5. Om research: användaren klistrar svar, annars gå vidare
6. Läs `docs/principer.md` + designmallen i `docs/design-prompt.md`
7. Skriv `design.md` i rätt mapp (`docs/[ämne]/[ämne]-[nr]-[slug]/design.md`)
8. Uppdatera `docs/index.yaml` med ny entry (status: design)
9. Commit + push till main (se Git-policy)
10. Avsluta med copy-paste-instruktion till användaren: `Skicka detta i en ny session: "bygg docs/[ämne]/[ämne]-[nr]-[slug]"`

### 2. Design → Bygg (Sonnet räcker)
Trigger: användaren säger "bygg [mapp]" eller pekar på en design.md

1. Läs `design.md` i angiven mapp — bindande beslut som inte får ändras
2. Läs `docs/principer.md` för pedagogiska riktlinjer
3. **Om design.md strider mot principer.md → flagga till användaren, bygg inte vidare**
4. Bygg `index.html` i samma mapp — **följ Byggordningen steg för steg** (Write skeleton → Edit sektioner). Skriv INTE hela filen i ett Write-anrop.
5. Kör self-check
6. Uppdatera `docs/index.yaml` (status: byggd)
7. Commit + push till main (se Git-policy)

### 3. Feedback → Iteration
Trigger: användaren rapporterar problem efter testning

1. Läs feedback (helst enligt `docs/feedback-mall.md`)
2. Läs aktuell `design.md` + `index.html`
3. Justera koden, kör self-check, commit + push till main (se Git-policy)

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
GitHub Pages serverar från `docs/`. App-URL: `https://[user].github.io/barnapp/[ämne]/[ämne]-[nr]-[slug]/`

---

## Tekniska regler

**Format:** En enda HTML-fil. CSS och JS inline. Inga externa beroenden utom eventuellt Google Fonts via CDN.

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

**Byggordning — iterativt (viktigt för att undvika timeout):**

> **Teknisk regel:** Skriv ALDRIG hela index.html i ett enda Write-anrop.
> Filer över ~200 rader riskerar timeout. Bygg istället inkrementellt:

1. **Write** — Skriv skeleton (~100–150 rader): `<!DOCTYPE html>`, grundläggande CSS-variabler, steg-navigation, tomma steg-containers, och en minimal JS-struktur med event listeners men utan logik. Inga detaljer.
2. **Edit** — Implementera interaktionslogik för steg 1–3 (lägg till JS-funktioner och HTML-innehåll i respektive steg-containers)
3. **Edit** — Implementera interaktionslogik för steg 4–6 (eller resterande steg)
4. **Edit** — Lägg till visuell feedback + CSS-animationer
5. **Edit** — Lägg till scaffolding-nivåer
6. **Edit** — Lägg till ljud (Web Audio API)
7. Self-check mot design.md

Varje Edit-anrop ändrar bara en del av filen (~50–150 rader åt gången) och riskerar inte timeout.

---

## Self-check
Innan du rapporterar klart, verifiera mot design.md:
- [ ] Touch targets matchar beslutet?
- [ ] CRA-nivåer implementerade som specificerat?
- [ ] Scaffolding-djup stämmer?
- [ ] Gate-keeping på rätt ställen?
- [ ] Har varje skärm en do-komponent (minst Constructive)?
- [ ] Börjar appen med guided challenge, inte förklaring?
- [ ] Vardagsförankring i steg 1?

Verifiera även mot `docs/principer.md`:
- [ ] Språknivå och max ord/skärm stämmer med åldersgruppen?
- [ ] `prefers-reduced-motion` hanteras?
- [ ] Inga tidsgränser?
- [ ] Fail states är uppmuntrande, inte straffande?
- [ ] Touch: Pointer Events, inte mouse events?

---

## Vanliga misstag att undvika
- Rörliga touch targets (pulsera/glöd istället för rotera)
- Poetiska metaforer i text (test: kan en 7-åring rita det?)
- Facktermer utan trestegsbrygga: upplevelse → vardag → etikett
- Fler än ett lärandemål (flagga om design.md verkar täcka flera)
- Text som inte sitter intill det den beskriver
- Auto-progression (eleven styr takten, alltid)
- Textfält för barns reflektion (använd flerval/visuellt val)
- Poängsystem/stjärnor som primär motivator

---

## Framtida utveckling (v0.2)
- **Skills:** Opus-design och Sonnet-bygg som separata skills, triggas automatiskt
- **Hooks:** Post-push hook som påminner om review.md
- **Automatisk research:** WebSearch-integration istället för manuell Perplexity
- **CI:** Validera index.yaml + self-check som GitHub Action
