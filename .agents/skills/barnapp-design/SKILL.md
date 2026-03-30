# Barnapp-design — visuellt designsystem för läroappar

Detta skill kompletterar `frontend-design`-skillen med regler specifika för interaktiva läroappar riktade till barn 6–12 år. Vid konflikt vinner alltid denna skill.

## Designriktning

**Ton:** Varm, lekfull, tydlig. Tänk "väldesignad leksak" — inte "cool tech-demo".

Välj estetik från detta spektrum (aldrig generisk):
- **Labb/utforskare** — mörka bakgrunder, glödande element, "science kit"-känsla
- **Naturlig/organisk** — jordtoner, mjuka former, papper-textur
- **Färgglad/playful** — starka primärfärger, rundade hörn, studsiga animationer
- **Byggare/craft** — grid-baserat, "klipp-och-klistra", haptisk känsla
- **Storybook** — illustrativ, varm belysning, boksidesmetafor

Variera mellan appar — ingen app ska se ut som den förra.

## Constraints som ÖVERSTYR frontend-design

### Layout
- **Inga grid-breaking element eller asymmetrisk layout** — barn behöver visuell förutsägbarhet
- **Tydlig visuell hierarki** — ett fokusområde per skärm, aldrig konkurrerande element
- **Centrera interaktionsytan** — viktigaste elementen i mitten eller nedre halvan (tumräckvidd)
- **Generöst whitespace** — men strukturerat, inte dramatiskt negativt utrymme

### Typografi
- **Google Fonts tillåtet** (enda externa beroende)
- Välj karaktärsfulla men **mycket läsbara** fonter — barn med läsovana är målgruppen
- Bra val: Nunito, Quicksand, Baloo 2, Patrick Hand, Fredoka One (display), Lexend (body)
- **Aldrig:** Dekorativa fonter som kräver avkodning, skript-fonter, tunna vikter
- Body: minst `font-size: 1.1rem`, gärna `1.25rem` för ålder 6–8

### Färg
- **Hög kontrast** — minst WCAG AA (4.5:1 text, 3:1 stora element)
- CSS-variabler för teman — ja, precis som frontend-design kräver
- Dominant färg + skarp accent fungerar bra — men **undvik neon mot vitt**
- Felstates: varm orange/gul, aldrig aggressivt rött
- Framgång: grön eller blå med animation — aldrig bara färgbyte (färgblindhet)

### Motion och animation
- **`prefers-reduced-motion` obligatoriskt** — all animation bakom media query
- **Inga blinkande element > 3 ggr/sek**
- Animationer får **aldrig blockera input** — barnet ska kunna trycka under animation
- Bra: studsig feedback vid rätt svar, mjuk glow vid hover, staggered reveal vid sidladdning
- Dåligt: roterande touch targets, parallax, scroll-hijacking
- **CSS-only** — inga animationsbibliotek (en HTML-fil, inga beroenden)

### Touch targets
- **Minimum 44×44 CSS px** (WCAG), sikta på **60–80 px** för barn 6–9
- Rörliga targets: ALDRIG rotera/flytta — pulsera eller glöd istället
- Placera inte interaktiva element nära skärmkant (felträffar)
- Variera knappposition mellan steg (holdover-effekt)

### Bakgrunder och detaljer
- Subtila texturer och gradienter — ja, bra för atmosfär
- **Inga grain overlays** (ser trasigt ut på billiga skärmar)
- **Inga custom cursors** (förvirrande för barn)
- Dekorativa element separerade från lärinnehåll (seductive details-principen)

## Auditory icons (Web Audio API)

Korta, mjuka ljud — inte melodier, inte earcons, inte bakgrundsmusik.
- Rätt svar: mjukt "pop" eller "pling" (~100ms)
- Fel svar: dämpad "bonk" eller "blub" (~150ms) — aldrig straffande
- Progression: kort stigande ton (~200ms)
- Alla ljud: wrappa i try/catch, respektera user preference

## Vad som INTE ändras från frontend-design

Dessa principer gäller fullt ut:
- Välj karaktärsfulla fonter (inte Arial/Inter/Roboto)
- CSS-variabler för konsistens
- Dominant färg + skarp accent
- Intentionell design — varje val motiverat
- Variera estetik mellan appar
- Undvik AI-slop (generiska layouts, förutsägbara mönster)
