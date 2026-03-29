# Feedback & Förbättringsförslag: fysik-1-gravitation
**Version:** 1.1
**Datum:** 2026-03-29
**Testat av:** Vuxen (utvecklare)
**Enheter:** Mobil ca 8" + Desktop
**Källor:** Användaren (U) · NotebookLM (NLM) · Sonnet/RCA (S)
**Syfte:** Förbättra fysik-1-gravitation + generalisera arbetsflödet → skickas till Opus

---

## Del 1 – Buggrapport

### Problem 1
- **Steg:** 4 – Bollar med slider för massa
- **Vad hände:** När massan ökades växte båda pilarna lika mycket. Det implicita budskapet blev att bollarna drar i varandra med lika stor kraft oavsett massaskillnad.
- **Förväntat:** Pilen mot den tyngre bollen borde vara större — för att spegla att mer massa ger starkare dragning mot det tunga objektet.

### Problem 2
- **Steg:** 5 – "Äpplet drar också i Jorden"
- **Vad hände:** Pilen mot äpplet är stor (grön), pilen mot Jorden är liten (lila).
- **Förväntat:** Pilen mot Jorden borde vara större eftersom Jordens massa är mycket större — visualiseringen kommunicerar omvänt förhållande jämfört med lärandemålet.

### Problem 3
- **Steg:** 8 – Feedbacktext vid fel svar
- **Vad hände:** Texten "Titta på pilarna — de pekar åt båda håll!" visades men bara en stor pil syntes i arena.
- **Förväntat:** Feedbacktext som refererar till ett visuellt element kräver att elementet är aktivt och synligt.

### Fungerade bra
- Steg 3: Tydligt hur bollar dras mot varandra, gravitation namnges naturligt
- Steg 7: Testboll nära olika planeter — pedagogiskt stark struktur
- Steg 8: "Vad lärde du dig?" är ett bra pedagogiskt avslut
- Drag, klick och layout fungerar på ca 8" och desktop

---

## Del 2 – RCA

### Rotorsak 1: Odeklarerad semantik för visuella variabler

**Delar:** Problem 1 och 2

Designdokumentet angav aldrig explicit vad pillängd/tjocklek representerar: kraft (Newton 3) eller acceleration/rörelse. Appens steg 4 kodades med lika tjocka pilar åt båda håll — korrekt om pilar = kraft. Steg 5 kodades med en stor pil mot äpplet — korrekt om pilar = acceleration. De två stegen kodades mot *olika* implicita semantiker utan att det beslutades eller kommunicerades.

Barnet tolkar naturligt pilar som "hur starkt något dras" i rörelseriktning, inte som Newtons tredje lag. Resultatet: båda stegen motverkar lärandemålet "mer massa = starkare dragning" fast av olika anledningar.

**Designregel:** Varje visuell variabel (pillängd, tjocklek, animationshastighet, färg) ska deklareras explicit i designdokumentet: *"Piltjocklek = X"*. Variabeln används konsekvent i hela modulen. Deklarationen är ett obligatoriskt fält i design.md.

---

### Rotorsak 2: Feedback utan villkor på visuellt state

**Delar:** Problem 3

Feedbacktexten i steg 8 refererar till pilar som antas vara synliga, men arenaelementet i steg 8 har en annan konfiguration än steg 5 där pillogiken skrevs. Ingen kod verifierar att refererade element är aktiva och synliga innan texten visas.

**Designregel:** Feedbacktext som refererar till ett visuellt element (`if feedbackText references X`) är villkorad av att X är i aktivt state. Texten triggas av den visuella händelsen, aldrig asynkront. QA-steg: gå igenom alla feedbacktexter och verifiera att varje refererat element finns i arena vid den tidpunkten.

---

### Rotorsak 3 (latent): Kontraintuitiva koncept utan prediction-steg

**Delar:** Inte en synlig bugg — men en pedagogisk risk identifierad av NLM.

Steg 4 visar lika stora pilar utan att förbereda barnet på att det är överraskande. Barn 8–9 år förväntar sig att "mer massa = starkare dragning åt det hållet" — att se lika stora pilar utan ett prediction-steg skapar kognitiv dissonans som inte bearbetas. Utan bearbetning fastnar den naïva teorin kvar bredvid den korrekta.

**Designregel:** Kontraintuitiva visuella utfall ska alltid föregås av ett prediction-steg. Dokumentera kontraintuitiva koncept per modul i ett gemensamt register (se F5).

---

## Del 3 – Förslag till åtgärder och designregler

> Alla förslag är öppna — inget är beslutat. Opus tar beslut om implementering.

---

##### F1 – Pilsemantik måste deklareras explicit [U + S]

**Förslag:** Innan pilannoteringar används för första gången i en modul — visa en kort legend som kopplar pillängd/tjocklek till det abstrakta värdet den representerar.

**Designregel:** Obligatoriskt fält i design.md:
```
## Visuella variabler
| Variabel | Representerar | Enhet/skala |
|---|---|---|
| Piltjocklek | [kraft / acceleration / ?] | [relativ] |
| Animationshastighet | [?] | [relativ] |
```

---

##### F2 – Predict-and-Explain vid kontraintuitiva moment [NLM + S]

**Förslag:** När appen visualiserar ett fenomen som bryter mot barnets intuition:
1. Låt barnet gissa resultatet innan det visas
2. Visa utfallet
3. Förklara explicit varför med text som adresserar just diskrepansen

> *Exempel steg 4: "Vilken pil tror du blir störst?" → visar lika stora pilar → "Krafterna är alltid lika stora åt båda håll! Men den lättare bollen rör sig mer."*

**Designregel:** Kontraintuitiva koncept kräver alltid ett prediction-steg. Listan dokumenteras i misconceptions-registret (F5).

---

##### F3 – State-Feedback Sync och Visuell Signalering [U + NLM]

**Förslag:** Förklarande feedback måste vara villkorad av vad som faktiskt är synligt i appens state (Spatial Contiguity). Men på en 8-tumsskärm räcker det inte att elementet bara *finns* — det måste uppmärksammas för att undvika onödig visuell sökning (extraneous load).

**Designregel:**
1. Kodarkitekturen ska ha en explicit koppling: `if (feedbackText references component X) → assert(X is in active state)`
2. **Signaling-principen:** Om texten säger "Titta på pilarna" måste systemet lägga till en visuell signal (pilarna blinkar, highlightas eller pulserar) exakt samtidigt som texten visas.

---

##### F4 – Visuell representation: kraft vs. acceleration [U + NLM]

**Bakgrund:** Problem 1 och 2 rymmer en fysikalisk paradox. Newtons tredje lag säger att kraft är exakt lika stor åt båda håll oavsett massaskillnad — lika stora pilar är alltså *fysikaliskt korrekt* om pilarna representerar kraft. Men om de representerar rörelseeffekt/acceleration borde de vara olika stora.

**Varning gällande Alternativ B (Pedagogisk förenkling):** Kognitionsforskningen varnar starkt för att bekräfta barns felaktiga naïve theories (att tyngre objekt har starkare dragningskraft åt ena hållet) genom att rita felaktiga modeller i gränssnittet. Att lära ut fel fysik för att det "känns intuitivt" skapar *ontological miscategorizations* som är extremt svåra för barn att tvätta bort senare.

**Förslag till beslut för Sonnet och Opus:**

| Alternativ | Pilar representerar | Fysikaliskt korrekt | Intuitivt 8–9 år? |
|---|---|---|---|
| A | Kraft (Newton 3) — lika stora | Ja | Nej — kräver prediction error |
| ~~B~~ | ~~Acceleration — olika stora~~ | ~~Nej~~ | ~~Ja~~ |
| C | Två lager: pilar = kraft (lika), hastighet = acceleration | Ja | Kräver tydlig legend |

Alternativ B stryks. Välj A eller C och dokumentera beslutet i designdokumentet.

- **Alternativ A:** Kombinera med F2. Låt barnet gissa, bli överraskad av att pilarna är lika stora: *"Krafterna är alltid lika stora! Men den lätta bollen är lättare att flytta på."*
- **Alternativ C:** Pilar representerar alltid kraft (lika stora). Acceleration visas enbart dynamiskt via animationshastighet.

---

##### F5 – Generaliserbart register för kontraintuitiva koncept [U + S]

**Förslag:** Skapa `docs/misconceptions-register.md` — ett levande dokument med kända naïve theories per ämnesområde. Fylls på för varje ny modul. Obligatorisk input i pre-flight check.

---

##### F6 – Auditiva ikoner för osynliga krafter [NLM]

**Förslag:** Att titta på bollar, pilar och läsa text på en 8-tumsskärm skapar snabbt visuell överbelastning (split-attention). Abstrakta osynliga variabler som massa och gravitation kan förstärkas via arbetsminnets auditiva kanal utan att ta upp skärmutrymme.

**Designregel:** Använd *auditory icons* (ljud som låter som en fysisk handling, inte melodier):
- När reglaget för massa dras upp: ett ljud som gradvis blir dovare/tyngre
- När bollar dras mot varandra: ett spänt "sugande" ljud vars intensitet matchar dragningskraften

Ljud bär då matematisk/fysikalisk information utan att ta upp en enda pixel.

---

## Del 4 – Föreslaget arbetsflöde

### Nuvarande
```
Opus (plan + design) → Sonnet (bygger) → [Test]
```

### Föreslaget

```
Steg 1  EXTERN FAKTARESEARCH           [Perplexity]
        Opus skickar domänfrågor:
        - Vilka misconceptions har barn X år om konceptet?
        - Vilken forskning finns om effektiva vardagsexempel?
        - Vilka förenklingar är försvarbara vs. skapar seglivade fel?
        Output: Evidensbaserade svar med källciteringar

Steg 2  PRELIMINÄR MODULPLAN           [Opus]
        Utifrån Perplexity-research:
        - Lista på övningar/steg
        - Lärandemål per steg
        - Förslag på visuella representationer och interaktioner
        (Inget fullständigt designdokument ännu)

Steg 3  KOGNITIV / PEDAGOGISK          [NotebookLM]
        GRANSKNING (Pre-flight Check)
        Opus skickar preliminärplan med prompt:
        ─────────────────────────────────────────
        "Modul: [X]. Målgrupp: [ålder]. Enhet: [skärm].
        Förkunskaper: [vad barnet kan sedan innan].
        Plan: [Steg 1–X, kort beskrivning av interaktion]

        Analysera mot kognitionsforskningen:
        1. Vilka naïve theories har barn om detta, och hur ska
           visualiseringen korrigera snarare än förstärka dem?
        2. Finns steg som bryter mot Mayers multimediaprinciper
           (Spatial Contiguity, Coherence, Temporal Contiguity)?
        3. Hur kan stealth assessment byggas in?
        4. Saknas något developmental progression-steg?"
        ─────────────────────────────────────────
        Output: Granskning mot corpus (Mayer, Sweller, Kapur,
        Clements/Sarama, Outhwaite)

Steg 4  KOMPLETTERANDE RESEARCH        [Perplexity, vid behov]
        Om NotebookLM identifierar frågor utanför corpus.

Steg 5  FULLSTÄNDIGT DESIGNDOKUMENT    [Opus]
        Sammanväger Perplexity + NotebookLM.
        Inkluderar obligatorisk tabell: Visuella variabler.

Steg 6  IMPLEMENTERING                 [Sonnet]
        Bygger från validerat designdokument.

Steg 7  TEST + BUGGRAPPORT             [Människa]
        Rapport → Opus för beslut om justering.
```

### Rollfördelning

| Agent | Ansvarar för |
|---|---|
| Opus | Orchestrator: arbetsflöde, prompts, designdokument |
| Perplexity | Vad som är vetenskapligt sant (domänfakta, forskning) |
| NotebookLM | Hur faktan paketeras för lärande (kognition, pedagogik) |
| Sonnet | Kod och UI |
| Människa | Test, godkännande, vision |

---

## Del 5 – Öppna frågor

### Till Sonnet
- [ ] **Pilsemantik (F4):** Alternativ A eller C för fysik-1-gravitation? Motivera utifrån RCA.
- [ ] **Problem 1+2:** Kan fix implementeras utan omdesign av steg 4–5, eller krävs omstrukturering?
- [ ] **Problem 3:** Vilka andra ställen i modulen har samma state-feedback-desync?
- [ ] **Multimodal avlastning (F6):** Hur implementeras Web Audio API för att ge massekvationen en auditiv representation synkad med animation?

### Till Opus
- [ ] **Pre-flight Check (Del 4):** Implementeras från nästa modul eller retroaktivt?
- [ ] **Misconceptions-register (F5):** Skapas nu och fylls retroaktivt, eller startas från nästa modul?
- [ ] **Visuella variabler (F1):** Ska obligatorisk variabeldeklaration läggas till design-prompt.md?
- [ ] **Predict-and-Explain (F2):** Obligatoriskt i alla framtida moduler, eller case-by-case?

### Till användaren
- [ ] Nästa modul — ämne?
- [ ] Prioritet: fixa fysik-1-gravitation först, eller starta ny modul med nytt arbetsflöde?

---

*v1.0: Användaren + Perplexity (struktur) + NotebookLM (pedagogisk analys)*
*v1.1: Sonnet (RCA Del 2, NLM-justeringar F3/F4, ny F6, strök Alt. B)*
*Nästa steg: Opus tar beslut om arbetsflöde och pilsemantik*
