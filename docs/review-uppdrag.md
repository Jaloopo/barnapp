# Uppdrag: Granska barnapp-workflow

Du är en erfaren pedagogisk teknolog och AI-workflow-designer. Granska detta repo och ge konkret feedback.

## Vad du granskar

Detta är ett system för att bygga interaktiva läroappar för barn 6–12. Upplägget är:

1. **Människa** skriver en kort brief (idé + åldersgrupp)
2. **Opus** (Claude.ai) genererar en `design.md` via en promptmall
3. **Sonnet** (Claude Code) läser `design.md` + `principer.md` och bygger `index.html`
4. **Människa** testar på GitHub Pages och ger feedback
5. Iteration: feedback → Sonnet justerar koden

## Tillgängliga AI-verktyg i ekosystemet

Utöver Claude Code (Sonnet) och Claude.ai (Opus) finns:

- **NotebookLM (RAG)** — laddad med källor om pedagogik, UX och matematik. Används för att undersöka forskningsunderlag, kolla om en designbeslut stöds av evidens, eller fördjupa sig i ett ämnesområde.
- **Perplexity** — websökning. Används för aktuell fakta om ämnen barnet möter i apparna, eller för att hitta extern information som inte finns i NotebookLM.

Dessa används av människan, inte av den kodande AI:n. Typiska användningsfall:
- Innan design.md: "Vad säger forskningen om X?" → NotebookLM
- Vid oklart designbeslut: "Finns det evidens för Y?" → NotebookLM
- Ämnesinnehåll till en app (t.ex. fakta om elektroner): → NotebookLM eller Perplexity

## Dokument att läsa

Läs dessa i ordning:

1. `CLAUDE.md` — instruktioner till den kodande AI:n (Sonnet)
2. `docs/principer.md` — pedagogiska designprinciper (A–I)
3. `docs/design-prompt.md` — mall för att generera design.md per app

## Frågor att besvara

### 0. Din övergripande bedömning av upplägget
Du är själv en del av detta system (som Opus-designern). Ge din ärliga syn:
- Är detta ett vettigt sätt att arbeta — eller finns ett bättre upplägg?
- Vad är den svagaste länken i kedjan människa → Opus → Sonnet → GitHub Pages?
- Är rollfördelningen mellan Opus och Sonnet rätt, eller bör något göras annorlunda?

### 1. Är arbetsdelningen rätt?
- Är det rätt att Opus designar och Sonnet kodar, eller bör något göras annorlunda?
- Vad riskerar falla mellan stolarna i överlämningen Opus → Sonnet?

### 2. Är design.md-mallen tillräcklig?
- Vilka beslut saknas som Sonnet sannolikt kommer behöva fråga om?
- Är något i mallen överspecificerat (styr fel saker)?

### 3. Är CLAUDE.md:s instruktioner till Sonnet kompletta?
- Vilka vanliga misstag täcks INTE av "Vanliga misstag att undvika"?
- Är self-checken tillräcklig, eller saknas viktiga kontrollpunkter?

### 4. Är principer.md lämplig som referens för AI?
- Är dokumentet skrivet för att en AI ska kunna tillämpa det, eller är det skrivet för människor?
- Vad behöver förtydligas eller omstruktureras?

### 5. Iteration och feedback
- Hur bör feedback från testning struktureras för att Sonnet ska kunna agera på den effektivt?
- Föreslå ett enkelt feedbackformat att använda efter testning.

## Leverans

Ge din feedback som:
- **Kritiska brister** (blockar bygget)
- **Viktiga förbättringar** (värt att fixa nu)
- **Mindre förbättringar** (kan vänta)

Avsluta med en reviderad version av `CLAUDE.md` och/eller `design-prompt.md` om du har konkreta ändringsförslag.
