---
name: bygg
description: Bygg en barnlärapp från design.md. Triggas med "/bygg [mapp]" eller "bygg [mapp]". Läser design, kontrollerar principer, bygger inkrementellt, kör self-check, uppdaterar index och committar.
user_invocable: true
---

# /bygg — Bygg lärapp från design.md

## Trigger
Användaren säger `/bygg docs/[ämne]/[ämne]-[nr]-[slug]` eller `bygg docs/[ämne]/[ämne]-[nr]-[slug]`.

## Förutsättningar
- En `design.md` finns i angiven mapp
- `docs/principer.md` finns
- `docs/index.yaml` har en entry för appen

## Steg-för-steg

### 1. Läs och validera
1. Läs `design.md` i angiven mapp — detta är **bindande beslut** som inte får ändras
2. Läs `docs/principer.md` för pedagogiska riktlinjer
3. Läs `barnapp-design`-skillen för visuella riktlinjer
4. **Om design.md strider mot principer.md → STOPPA och flagga till användaren**
5. Bekräfta kort för användaren: "Bygger [titel], [antal steg] steg, [ålder], [vanilla/React]"

### 2. Bygg inkrementellt (ALDRIG hela filen i ett Write)

> Filer över ~200 rader riskerar timeout. Bygg i Edit-pass:

**Pass 1 — Write skeleton** (~100–150 rader):
- `<!DOCTYPE html>`, `<meta viewport>`, Google Font-länk
- CSS-variabler enligt barnapp-design (dominant färg + accent)
- Grundläggande layout + steg-navigation
- Tomma steg-containers med id:n
- Minimal JS-struktur: event listeners, steg-navigation, tomma funktioner
- `prefers-reduced-motion` media query (tom men redo)

**Pass 2 — Edit: Interaktionslogik steg 1–3**
- Guided challenge (steg 1) med vardagsförankring
- Do-komponenter per steg
- CRA-progression enligt design.md

**Pass 3 — Edit: Interaktionslogik steg 4+**
- Resterande steg
- Gate-keeping där design.md kräver det
- Konsolidering i sista steget

**Pass 4 — Edit: Visuell feedback + CSS**
- Feedback vid rätt/fel (< 300ms)
- Animationer (CSS-only, bakom prefers-reduced-motion)
- Touch target-storlekar enligt design.md

**Pass 5 — Edit: Scaffolding**
- Fel 1 → visuell markering
- Fel 2 → delvis ledtråd
- Fel 3 → fullständig scaffold
- Expertise reversal: minska scaffolding vid framgång

**Pass 6 — Edit: Ljud (Web Audio API)**
- Auditory icons: pop/pling/blub
- Wrappa i try/catch
- Korta ljud, inga melodier

### 3. Self-check

Verifiera mot **design.md**:
- [ ] Touch targets matchar beslutet?
- [ ] CRA-nivåer implementerade som specificerat?
- [ ] Scaffolding-djup stämmer?
- [ ] Gate-keeping på rätt ställen?
- [ ] Har varje skärm en do-komponent (minst Constructive)?
- [ ] Börjar appen med guided challenge, inte förklaring?
- [ ] Vardagsförankring i steg 1?

Verifiera mot **principer.md**:
- [ ] Språknivå och max ord/skärm stämmer med åldersgruppen?
- [ ] `prefers-reduced-motion` hanteras?
- [ ] Inga tidsgränser?
- [ ] Fail states är uppmuntrande, inte straffande?
- [ ] Touch: Pointer Events, inte mouse events?

Verifiera mot **barnapp-design**:
- [ ] Karaktärsfull font (inte Arial/Inter/Roboto)?
- [ ] CSS-variabler för färgtema?
- [ ] Hög kontrast (WCAG AA)?
- [ ] Animationer bakom prefers-reduced-motion?
- [ ] Ingen AI-slop (generisk layout)?

Om något misslyckas: åtgärda innan du går vidare.

### 4. Kör /simplify

Kör `/simplify` på den byggda `index.html` för att rensa upp kodkvalitet innan commit.

### 5. Uppdatera index.yaml

Ändra appens status till `byggd` i `docs/index.yaml`.

### 6. Commit och push

```bash
git add docs/[ämne]/[ämne]-[nr]-[slug]/index.html docs/index.yaml
git commit -m "bygg: [ämne]-[nr]-[slug] — [kort beskrivning]"
git push origin main
```

Om push misslyckas: `git pull --rebase origin main && git push origin main`

### 7. Rapportera klart

Avsluta med:
```
✅ Byggd: [titel]
📁 docs/[ämne]/[ämne]-[nr]-[slug]/index.html
🔗 https://jaloopo.github.io/barnapp/[ämne]/[ämne]-[nr]-[slug]/
📝 Testa och ge feedback med: docs/feedback-mall.md
```

## Vanliga misstag att fånga

- Rörliga touch targets (pulsera/glöd istället för rotera)
- Poetiska metaforer (test: kan en 7-åring rita det?)
- Facktermer utan trestegsbrygga: upplevelse → vardag → etikett
- Fler än ett lärandemål
- Text som inte sitter intill det den beskriver
- Auto-progression (eleven styr takten, alltid)
- Textfält för barns reflektion (använd flerval/visuellt val)
- Poängsystem/stjärnor som primär motivator
