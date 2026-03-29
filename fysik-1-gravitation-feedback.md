# Feedback & Förbättringsförslag: fysik-1-gravitation
**Version:** 1.0  
**Datum:** 2026-03-29  
**Testat av:** Vuxen (utvecklare)  
**Enheter:** Mobil ca 8" + Desktop (desktop: visuellt utan anmärkning)  
**Syfte med dokument:** Skickas till Sonnet för RCA + förfining → sedan till Opus för beslut om arbetsflöde

---

## Del 1 – Buggrapport

```
App: fysik-1-gravitation
Enhet: Mobil ca 8" / [webbläsare] + Desktop / [webbläsare]
Testad av: Vuxen
```

### Problem 1
- **Steg:** 4 – Bollar med olika storlek, reglaget för massa
- **Vad hände:** När massan ökades på en boll växte båda pilarna
  lika mycket. Det implicita budskapet blev att bollarna drar i
  varandra med lika stor kraft oavsett massaskillnad.
- **Förväntat:** Pilen mot den tyngre bollen borde vara större,
  pilen mot den lättare bollen borde vara mindre – för att spegla
  att mer massa ger starkare dragning mot det tunga objektet.
- **Skärmbild:** –

### Problem 2
- **Steg:** 5 – "Äpplet drar också i Jorden"
- **Vad hände:** Pilen mot äpplet är större, pilen mot Jorden är
  mindre.
- **Förväntat:** Pilen mot Jorden borde vara större eftersom Jordens
  massa är mycket större – visualiseringen kommunicerar omvänt
  förhållande jämfört med lärandemålet "mer massa = starkare dragning".
- **Skärmbild:** –

### Problem 3
- **Steg:** 8 – Feedbacktext vid fel svar B) "Äpplet är tungt"
- **Vad hände:** Texten "Titta på pilarna igen — de pekar åt båda
  håll!" visades men i bilden syntes bara en stor pil mot Jorden,
  ingen pil tillbaka från äpplet.
- **Förväntat:** Feedbacktexten måste synkroniseras med state –
  om texten refererar till ett visuellt element måste det elementet
  vara renderat och synligt.
- **Skärmbild:** –

### Fungerade bra
- Steg 3: Tydligt och snyggt hur bollar dras mot varandra och
  konceptet namnges som gravitation
- Steg 7: Testboll som dras åt olika håll – pedagogiskt stark
  övning, polish kan förbättras men strukturen är bra
- Steg 8: "Vad lärde du dig?" är ett bra pedagogiskt avslut
- Inga problem med klick, drag eller visuell layout på stor
  mobil (ca 8") eller desktop

---

## Del 2 – RCA (Root Cause Analysis)

> **INSTRUKTION TILL SONNET:** Gör en RCA av de tre problemen ovan.
> Identifiera om de har gemensamma rotorsaker. Formulera varje
> rotorsak som en generaliserbar designregel för framtida moduler
> där kraft, rörelse eller abstrakta värden visualiseras med pilar
> eller andra skalningsbara element.
>
> Förslag på struktur per rotorsak:
> - Vad är grundproblemet (tekniskt / pedagogiskt / designmässigt)?
> - Vilka problem i Del 1 delar denna rotorsak?
> - Hur generaliseras det till en designregel?

### [Sonnet fyller i här]

---

## Del 3 – Förslag till åtgärder och designregler

> Nedan är förslag från tre källor: användaren (U), NotebookLM (NLM)
> och Perplexity/extern research (P). Alla är FÖRSLAG – inget är
> beslutat. Sonnet uppmanas att utvärdera, förfina och eventuellt
> lägga till egna förslag baserat på sin RCA i Del 2.

---

### F1 – Pilstorlekens semantik måste definieras explicit [U + NLM]

**Källa:** Användaren (observerade förvirringen) + NotebookLM  
**Förslag:** Om pilar representerar abstrakta värden (kraft, energi,
hastighet) måste skalningsregeln kommuniceras till barnet och vara
konsekvent i hela modulen. Definiera explicit vad den visuella
variabeln betyder:

> *Exempel: "Pillängd = Kraft, Animationshastighet = Acceleration"*

**Designregel (förslag):** Innan en pilannotation används för första
gången i en modul – visa en legend eller förklaring som kopplar
pillängd/storlek till det abstrakta värdet den representerar.

---

### F2 – Predict-and-Explain vid kontraintuitiva moment [NLM + P]

**Källa:** NotebookLM (Kapur: Productive Failure) + Perplexity
(forskning om naïve theories hos 8–9-åringar)  
**Förslag:** När appen visualiserar ett fenomen som bryter mot barnets
vardagsintuition (gravitation, friktion, bråk) ska den inte bara
visa det korrekta utfallet. Bygg in ett Predict-and-Explain-moment:

1. Låt barnet gissa resultatet innan det visas
2. Visa utfallet
3. Om utfallet är kontraintuitivt – förklara explicit varför med
   text som adresserar just diskrepansen

> *Exempel för steg 4: "Vilken pil tror du blir störst?" →
> visar lika stora pilar → "Krafterna är alltid lika stora åt
> båda håll! Men den lättare bollen rör sig mer."*

**Designregel (förslag):** Kontraintuitiva koncept kräver alltid
ett prediction-steg. Listan på kontraintuitiva koncept ska växa
för varje ny modul och dokumenteras i ett gemensamt register.

---

### F3 – State-Feedback Sync [U + NLM]

**Källa:** Användaren (observerade desync) + NotebookLM
(Mayers Spatial Contiguity-princip)  
**Förslag:** Förklarande feedback (explanatory feedback) måste vara
villkorad av vad som faktiskt är synligt i appens state. Ingen
feedbacktext får referera till ett visuellt element om inte det
elementet är aktivt och synligt.

**Designregel (förslag):** Kodarkitekturen bör ha en explicit
koppling: `if (feedbackText references component X) → assert(X is
in active state)`. Detta bör vara ett obligatoriskt QA-steg
innan en modul levereras.

---

### F4 – Visuell representation: kraft vs. acceleration [U]

**Källa:** Användaren  
**Bakgrund:** Problem 1 och 2 rymmer en fysikalisk paradox:
Newtons tredje lag säger att kraft är exakt lika stor åt båda
håll oavsett massaskillnad. Lika stora pilar är alltså *fysikaliskt
korrekt* om pilarna representerar kraft. Men om de representerar
rörelseeffekt/acceleration borde de vara olika stora.

**Förslag (öppen fråga till Sonnet och Opus):** Detta är ett
fundamentalt designbeslut som påverkar hela modulens konceptuella
ram. Alternativen:

| Alternativ | Pilar representerar | Korrekt enligt | Intuitivt för 8–9 år? |
|---|---|---|---|
| A | Kraft (Newton 3) | Fysik | Nej – skapar förvirring |
| B | Acceleration/rörelse | Pedagogisk förenkling | Ja – stämmer med intuition |
| C | Båda visas (två lager) | Fysik + pedagogik | Kräver tydlig legend |

**Rekommendation (förslag):** Välj ett alternativ explicit och
dokumentera det i modulens designdokument. Oavsett val – kommunicera
det till barnet.

---

### F5 – Generaliserbart register för kontraintuitiva koncept [P + U]

**Källa:** Perplexity (forskning om vanliga misconceptions hos barn)
+ Användaren  
**Förslag:** Skapa ett levande dokument (`misconceptions-register.md`)
som samlar kända naïve theories per ämnesområde. Fylls på för varje
ny modul. Används som obligatorisk input i pre-flight check
(se Del 4).

---

## Del 4 – Förslag: Utökat arbetsflöde med Pre-flight Check

> Detta är ett förslag på ett nytt generaliserat arbetsflöde för
> framtida moduler. Sonnet uppmanas att utvärdera och förfina.
> Opus tar det slutliga beslutet om implementering.

### Nuvarande arbetsflöde
```
Opus (plan + designdokument) → Sonnet (bygger) → [Test]
```

### Föreslaget arbetsflöde

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
           visualiseringen korrigera dem?
        2. Finns steg som bryter mot Mayers multimediaprinciper
           (Spatial Contiguity, Coherence, Temporal Contiguity)?
        3. Hur kan stealth assessment byggas in för att mäta
           om förståelse uppnåtts?
        4. Saknas något developmental progression-steg enligt
           Learning Trajectory-forskning?"
        ─────────────────────────────────────────
        Output: Granskning mot corpus (Mayer, Sweller, Kapur,
        Clements/Sarama, Outhwaite)

Steg 4  KOMPLETTERANDE RESEARCH        [Perplexity, vid behov]
        Om NotebookLM identifierar frågor utanför corpus
        (ny forskning, domänspecifika fakta) skickar Opus
        en andra researcrunda till Perplexity.

Steg 5  FULLSTÄNDIGT DESIGNDOKUMENT    [Opus]
        Sammanväger Perplexity-research + NotebookLM-granskning.
        Producerar färdigt design + specifikationsdokument.

Steg 6  IMPLEMENTERING                 [Sonnet]
        Bygger modulen från validerat designdokument.

Steg 7  TEST + BUGGRAPPORT             [Människa]
        Testar mot mall (se Del 1).
        Rapport → Opus för justering.
```

### Rollfördelning

| Agent | Roll | Ansvarar för |
|---|---|---|
| Opus | Orchestrator / planerare | Arbetsflöde, designdokument, prompts |
| Perplexity | Extern faktaresearch | Vad som är vetenskapligt / tekniskt sant |
| NotebookLM | Kognitiv/pedagogisk granskning | Hur fakta paketeras för lärande |
| Sonnet | Implementering | Kod och UI |
| Människa | Test, beslut, kvalitetsgranskning | Godkännande och buggrapport |

**Arbetsfördelning Perplexity vs. NotebookLM:**
- **Perplexity:** Domänfakta, aktuell forskning, syntax, versioner,
  externa källor med citeringar. Ansvarar för *vad* som är sant.
- **NotebookLM:** Kognitionspsykologi och pedagogisk arkitektur
  utifrån uppladdad corpus. Ansvarar för *hur* faktan paketeras
  för en specifik målgrupp.

---

## Del 5 – Öppna frågor och beslutspunkter

> Dessa frågor behöver besvaras – av Sonnet (tekniska/design),
> Opus (arbetsflöde) eller användaren (vision/prioritet).

### Till Sonnet (tekniska / designfrågor)
- [ ] **Pilsemantik (F4):** Vilket alternativ (kraft / acceleration /
      båda) väljs för fysik-1-gravitation? Motivera utifrån RCA.
- [ ] **Problem 1+2:** Kan en fix implementeras utan att ändra
      modulens grundläggande konceptuella ram, eller krävs
      omdesign av steg 4–5?
- [ ] **Problem 3:** Vad i kodarkitekturen orsakade desynken?
      Finns fler ställen i modulen där samma mönster upprepas?

### Till Opus (arbetsflöde / strategi)
- [ ] **Pre-flight Check (Del 4):** Ska detta arbetsflöde
      implementeras från nästa modul, eller retroaktivt på
      fysik-1-gravitation?
- [ ] **Misconceptions-register (F5):** Ska detta skapas nu
      och fyllas i retroaktivt, eller startas från nästa modul?
- [ ] **Designbeslutsdokumentation:** Ska ett "concept frame"-
      dokument per modul skapas som dokumenterar vad pilar /
      animationer / färger representerar?

### Till användaren (vision)
- [ ] Nästa modul – ämne? (Avgör om vi kan testa arbetsflödet live)
- [ ] Ska Predict-and-Explain (F2) vara obligatoriskt i alla
      framtida moduler, eller case-by-case?

---

*Dokument skapat av: Perplexity (strukturering + extern research)*  
*Input från: Användaren (observation + vision), NotebookLM (pedagogisk analys)*  
*Nästa steg: Sonnet fyller i Del 2 (RCA) och förfinar Del 3 → skickas till Opus*
