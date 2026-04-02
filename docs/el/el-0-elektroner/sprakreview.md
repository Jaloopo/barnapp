# Språkreview: el-0-elektroner

## Bakgrund

Efter lansering av el-0 identifierades att språket i appen var svårbegripligt — inte bara för målgruppen (8–9 år) utan även för vuxna utan förkunskaper. Modulens sekvenslogik och pedagogiska struktur bedöms vara stark, men skärmtextens formuleringar var otillräckliga. Innehållsöversikten skickades till NotebookLM och Perplexity för extern granskning.

---

## Vad som fungerar

- Steg 1–7 sekvenslogik är pedagogiskt välmotiverad
- Steg 6 prediction-steg hanterar korrekt misconceptionen "en elektron åker hela vägen"
- Steg 3 (dra elektronen) och steg 5 (tryck på knuffen) bedöms åldersadekvata av båda granskarna

---

## Identifierade språkproblem

| Steg | Problematisk text | Problem | Föreslagen ersättning |
|------|-------------------|---------|----------------------|
| Intro | "Idag tittar du in i sladden." | Metaforiskt – man kan inte bokstavligen titta in | "Idag ser du vad som finns inuti en sladd." |
| 1 | "I vilken kedja tror du att en liten knuff sprider sig lättast?" | "Sprider sig" abstrakt fysikmetafor | "I vilken kedja tror du att en liten knuff kan åka vidare lättast?" |
| 1 | "Inuti finns pyttesmå delar i kedjor." | "Kedjor" risk för bokstavlig feltolkning (cykelkedja) | "Inuti finns pyttesmå delar som sitter på rad efter varandra." |
| 2 | "Elektronen är inte kärnan och den är inte hela ljuszonen." | Negation + odefinierat ord "ljuszonen" | "Tryck på den lilla gula pricken. Det är elektronen!" |
| 2 | "ytterzon" (svarsalternativ) | Fackord utan förklaring | "utsidan" |
| 4 | Rubrik: "Samma lilla knuff, olika hårt" | Elliptisk mening, oklart vad "hårt" syftar på | "Lika knuff – men olika lätt att flytta" |
| 4 | "I vilken kedja sitter elektronerna lösare?" | "Sitter lösare" abstrakt fasthållningsmetafor | "I vilken kedja är det lättare att flytta elektronerna?" |
| 6 | Kort: "Alla tar ett steg" | Animism-risk – ger elektroner vilja och ben | "Alla flyttar sig ett steg" |
| 6 | Feedback fel: "Titta på alla prickar. Varje elektron tar bara ett litet steg." | Dubbel quantifier tätt ihop | "Titta – inte bara en prick rör sig. Alla prickar tar ett litet steg var." |
| 7 | Kort: "Vissa material håller hårdare" | Håller vad? Abstrakt | "Vissa material håller fast elektronen hårdare" |
| 7 | Feedback rätt: "Nästa gång testar du vilka riktiga material där små steg är lätta." | Komplex inbäddad bisats | "Nästa gång får du testa i vilka riktiga material elektroner lätt kan ta små steg." |
| 7 | Feedback fel: "Blixten och batteriet är inte elektronen." | Ontologiskt förvirrande | "Blixten och batteriet visar inte elektronen. Titta på den gula pricken vid atomen." |

---

## Spatial contiguity-risk (NotebookLM)

Feedbacktexter som "Titta på den gula pricken" och "Titta på alla prickar" ställer krav på att texten renderas *intill* animationen, inte i en separat panel längst ned. Om texten är statiskt placerad långt från animationen uppstår split-attention-effekt. Detta behöver verifieras i koden vid nästa implementation.

---

## Generella mönster att undvika

- **Elliptiska rubriker utan verb** — barn behöver en fullständig sats ("Samma lilla knuff, olika hårt" → oklar)
- **"Sitter" som metafor** — "elektroner sitter lösare" blandar konkret och abstrakt; byt mot "är" eller "håller fast"
- **Komplexa bisatser i feedback** — feedback ska vara omedelbart begriplig, ett påstående i taget
- **Animistiska formuleringar** — "tar steg", "åker" ger elektroner vilja; byt mot "flyttar sig", "knuffas"
- **Negativa instruktioner** — "inte kärnan, inte ljuszonen" är kognitiv belastning; säg vad det är, inte vad det inte är

---

## RCA: varför uppstod detta?

**Rot-orsak:** Texten i design.md var riktmärken, inte slutgiltig kopia.

Fältet "Text på skärmen (skriv ut exakt…)" tolkades av implementationsagenten som en skiss att parafrasera. Inga språkliga constraints hindrade improvisation vid implementation. Resultatet optimerades för teknisk korrekthet och koncishet — inte för 8-åringens ordförråd och kognitiva belastning.

**Bidragande orsak:** Inget språkgranskningssteg existerade i flödet mellan design.md och implementation. Textinnehållet har inte granskats av Perplexity eller NotebookLM innan bygget startade.

---

## Förslag på åtgärder (för Opus att besluta)

### 1. Uppdatera design-prompt.md
Ändra beskrivningen av fältet "Text på skärmen" så att det framgår att texten är *slutgiltig kopia*:
> "Skriv ut exakt vad som ska stå på skärmen. Detta är den färdiga kopian — ingen parafrasering eller förenkling är tillåten vid implementation. Använd barnets ordförråd direkt."

### 2. Lägg till språkgranskningssteg i Flöde 1 steg 5
Innan design.md committats: skicka all skärmtext (rubriker, instruktionstexttexten, feedback-texter) till Perplexity och NotebookLM för språkgranskning. Granskning ska ske *innan* /bygg triggas, inte i efterhand.

Förslag på Perplexity-prompt:
> "Vilka av dessa formuleringar är sannolikt svåra för ett barn på 8–9 år att förstå? Föreslå enklare alternativ. Orden 'elektron', 'atom' och 'kärna' används konsekvent och ska behållas."

Förslag på NotebookLM-prompt:
> "Bryter någon av dessa texter mot Mayers Coherence-, Spatial Contiguity- eller Temporal Contiguity-princip? Finns formuleringar som riskerar att förstärka naïva teorier om elektroner?"

### 3. Uppdatera /bygg-skillen
Lägg till en explicit notering: implementationen ska kopiera text från design.md *ordagrant*. Ingen omformulering vid bygge.

---

## Nästa steg

- [ ] Opus beslutar om åtgärderna ovan och uppdaterar design-prompt.md + /bygg-skill
- [ ] Texterna i el-0 revideras enligt tabellen ovan
- [ ] Spatial contiguity verifieras i koden
- [ ] De interaktiva delarna granskas i ett separat pass *efter* att texten är fixad
