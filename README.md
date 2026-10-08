# Smaaktraining

Een dagelijkse oefening om je oog voor interface-design te trainen. Eén challenge, vier rondes, samen een uur:

1. **Ontwerp** (20 min): een leeg canvas en een opdracht. Geen voorbeelden, geen AI.
2. **Bestudeer** (10 min): vier geschetste voorbeeldschermen. Schrijf 3 patronen, 3 do's en 3 don'ts op.
3. **Vergelijk** (10 min): leg je notities naast een analyse van acht observaties en vink aan wat je zelf zag.
4. **Herontwerp** (20 min): hetzelfde scherm opnieuw, met wat je net leerde. Daarna staan beide versies naast elkaar.

## Ontwerpen

In de ontwerprondes kies je zelf waar je werkt:

- **Schets hier**: een ingebouwd tekenvlak met pen, vormen, tekst, vullen, verplaatsen en gum.
- **Ontwerp in Figma**: werk in Figma en haal je frame op door het als PNG te plakken (⇧⌘C in Figma, ⌘V op de pagina), of kies of sleep een afbeelding.

## Draaien en hosten

De site is één statisch bestand, `index.html`, zonder build-stap of backend. Open het in een browser, of zet de map op een statische host zoals GitHub Pages, Netlify, Vercel of Cloudflare Pages.

Lokaal met een server:

```bash
python3 -m http.server 4174
```

Sessies, notities en het logboek worden bewaard in `localStorage` van de browser.

## Opbouw

Alles staat in `index.html`:

- `BUILTIN`: de vijf ingebouwde challenges met voorbeeldschermen en observaties.
- `BLOCK` en `phone()`: de bouwstenen waarmee voorbeeldschermen uit een korte lijst worden getekend.
- `mountBoard()`: het tekenvlak. `mountSource()`: de Figma-modus.
