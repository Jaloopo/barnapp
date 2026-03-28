# Feedback efter testning

Använd denna struktur när du rapporterar problem efter att ha testat en app.

## Mall

```
App: [id, t.ex. el-1-ledare]
Enhet: [mobil/iPad/laptop + webbläsare]
Testad av: [barn/vuxen + ålder om barn]

### Problem
- Steg: [nummer]
- Vad hände: [beskriv]
- Förväntat: [vad borde hänt]
- Skärmbild: [om möjligt]

### Fungerade bra
- [beskriv vad som fungerade, detta hjälper review.md]
```

## Exempel

```
App: el-1-ledare
Enhet: iPad 10" / Safari
Testad av: barn 8 år

### Problem
- Steg: 3
- Vad hände: Drag-target för liten, barnet missade upprepade gånger
- Förväntat: Ska kunna dra utan precision
- Skärmbild: -

### Fungerade bra
- Guided challenge i steg 1 fångade intresset direkt
- Scaffolding vid fel 2 hjälpte utan att ge bort svaret
```
