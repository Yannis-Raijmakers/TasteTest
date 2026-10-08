# Smaaktraining

Een dagelijkse oefening om je oog voor interface-design te trainen. Eén challenge, vier rondes, samen een uur:

1. **Ontwerp** (20 min): een leeg canvas en een opdracht. Geen voorbeelden, geen AI.
2. **Bestudeer** (10 min): vier geschetste voorbeeldschermen. Schrijf 3 patronen, 3 do's en 3 don'ts op.
3. **Vergelijk** (10 min): leg je notities naast een analyse van acht observaties en vink aan wat je zelf zag.
4. **Herontwerp** (20 min): hetzelfde scherm opnieuw, met wat je net leerde. Daarna staan beide versies naast elkaar.

## Ontwerpen

In de ontwerprondes kies je zelf waar je werkt:

- **Schets hier**: een ingebouwd tekenvlak met pen, vormen, tekst, vullen, verplaatsen en gum.
- **Ontwerp in Figma**: werk in Figma en haal je frame op door het als PNG te plakken (⇧⌘C in Figma, ⌘V op de pagina), een afbeelding te kiezen, of met een link naar het frame via de Figma-connector van Claude.

## Draaien

`smaaktraining.html` is de hele app: één bestand, zonder build-stap.

- Gepubliceerd als Claude-artifact: https://claude.ai/artifact/PhNidMHv92hvM3YDW5Cgig (privé). Daar bewaart de app je logboek in je Claude-account en kan Claude feedback geven, nieuwe challenges bedenken en frames uit Figma ophalen.
- Lokaal openen in een browser werkt ook. Dan blijft alles in de browser bewaard en zijn de Claude- en Figma-linkfuncties verborgen. Plakken en uploaden werken wel.

Het bestand is geschreven als artifact-pagina, dus zonder eigen `<html>`- en `<body>`-tags. Die voegt Claude toe bij het publiceren.

## Opbouw

Alles staat in `smaaktraining.html`:

- `BUILTIN`: de vijf ingebouwde challenges met voorbeeldschermen en observaties.
- `BLOCK` en `phone()`: de bouwstenen waarmee voorbeeldschermen uit een korte lijst worden getekend.
- `mountBoard()`: het tekenvlak. `mountSource()`: de Figma-modus.
- `initStore()`, `initAI()`, `initDL()`, `initFig()`: de koppelingen met Claude, elk optioneel.
