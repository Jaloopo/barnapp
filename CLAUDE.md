# CLAUDE.md — Barnapp-byggare

## Vad detta repo är
Interaktiva läroappar för barn 6–12, servade via GitHub Pages. Varje app är en enskild HTML-fil med inline CSS och JS.

## AI-ekosystem
Flera AI-verktyg används i olika roller:
- **Claude Opus (Claude.ai)** — pedagogisk designer, genererar design.md och granskar upplägg
- **Claude Sonnet (Claude Code)** — kodare, bygger index.html utifrån design.md
- **NotebookLM** — RAG med källor om pedagogik, UX och matematik. Används av människan för att undersöka forskningsunderlag eller ämnesinnehåll innan/under design
- **Perplexity** — websökning för aktuell fakta om ämnen i apparna

Du (Sonnet) behöver inte känna till de andra verktygen — de används av människan utanför din session.

## Arbetsflöde
1. Användaren lägger en `design.md` i rätt ämnesmapp (skapad i Claude.ai)
2. Du läser `design.md` — den innehåller bindande beslut som inte får ändras
3. Du läser `docs/principer.md` för pedagogiska riktlinjer
4. Du bygger `index.html` i samma mapp
5. Du kör self-check mot design.md:s beslut
6. Du committar och pushar direkt till `main` — inga feature branches, inga PRs
   - Kör alltid: `git add [filer] && git commit -m "..." && git push origin main`
   - Om push misslyckas: `git pull --rebase origin main && git push origin main`

## Mappstruktur
```
docs/
  principer.md
  [ämne]/
    [ämne]-[nr]-[slug]/
      design.md      ← från Claude.ai
      index.html     ← du bygger denna
```
Exempel: `docs/el/el-1-ledare/index.html`

GitHub Pages serverar från `docs/`. Appen nås på: `https://[user].github.io/barnapp/el/el-1-ledare/`

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
- localStorage tillåtet (apparna körs som vanliga webbsidor)

**Byggordning — iterativt:**
1. Skriv skeleton: steg-navigation + layout, inga detaljer
2. Implementera interaktionslogik per steg
3. Lägg till visuell feedback + animationer
4. Lägg till scaffolding-nivåer
5. Lägg till ljud
6. Self-check mot design.md

## Self-check
Innan du rapporterar klart, verifiera mot design.md:
- [ ] Touch targets matchar beslutet?
- [ ] CRA-nivåer implementerade som specificerat?
- [ ] Scaffolding-djup stämmer?
- [ ] Gate-keeping på rätt ställen?
- [ ] Har varje skärm en do-komponent (minst Constructive)?
- [ ] Börjar appen med guided challenge, inte förklaring?
- [ ] Vardagsförankring i steg 1?

## Vanliga misstag att undvika
- Rörliga touch targets (pulsera/glöd istället för rotera)
- Poetiska metaforer i text (test: kan en 7-åring rita det?)
- Facktermer utan trestegsbrygga: upplevelse → vardag → etikett
- Fler än ett lärandemål (flagga om design.md verkar täcka flera)
- Text som inte sitter intill det den beskriver
