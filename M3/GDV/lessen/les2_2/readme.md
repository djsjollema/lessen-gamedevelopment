# Les 2.2 - Game Design Document (Deel 1)

## Leerdoelen

Na deze les kun je:

- Het doel van een Game Design Document (GDD) uitleggen
- De structuur van een GDD toepassen
- Je concept vertalen naar concrete specificaties
- Visuele referenties verzamelen en verwerken

---

## Deel 1: Wat is een GDD? (15 min)

### Definitie

Een **Game Design Document** is een levend document dat alle aspecten van je game beschrijft. Het dient als:

- **Communicatiemiddel** tussen teamleden
- **Referentie** tijdens development
- **Planning tool** voor scope en features
- **Historisch document** van design beslissingen

### GDD Mythes

| Mythe                                 | Realiteit                         |
| ------------------------------------- | --------------------------------- |
| "GDD moet af voor je begint"          | GDD evolueert mee met development |
| "GDD moet 100+ pagina's zijn"         | Kort en relevant is beter         |
| "Eenmaal geschreven, nooit aanpassen" | Update regelmatig!                |
| "Alleen designers schrijven GDD"      | Heel het team draagt bij          |

### Wat hoort er NIET in een GDD?

- Technische implementatie details (dat is Technical Design)
- Code voorbeelden
- Marketing plannen
- Business model

---

## Deel 2: GDD Structuur (20 min)

### Basis Secties

```markdown
1. Overzicht
   - Titel
   - Elevator Pitch
   - Genre
   - Platform
   - Doelgroep

2. Gameplay
   - Core Loop
   - Mechanics
   - Win/Lose Condities
   - Controls

3. Game Elementen
   - Speler
   - Vijanden
   - Items/Power-ups
   - Level Design

4. Visuele Stijl
   - Art Direction
   - Referentie Afbeeldingen
   - UI Stijl

5. Audio
   - Muziek Stijl
   - Sound Effects
   - Referenties

6. Scope & Planning
   - Must Have Features
   - Nice to Have Features
   - Out of Scope
```

### MoSCoW Methode

Prioriteer features met MoSCoW:

| Categorie       | Betekenis                          | Voorbeeld                  |
| --------------- | ---------------------------------- | -------------------------- |
| **M**ust Have   | Essentieel, game werkt niet zonder | Player movement, collision |
| **S**hould Have | Belangrijk, maar game werkt zonder | Score systeem, lives       |
| **C**ould Have  | Nice to have als tijd over is      | Power-ups, animaties       |
| **W**on't Have  | Expliciet out of scope             | Multiplayer, level editor  |

---

## Deel 3: Jouw GDD Starten (25 min)

### Template voor Pac-Man Project

Gebruik dit template als basis. Vul zoveel mogelijk in tijdens de les.

```markdown
# [GAME TITEL]

## Game Design Document v0.1

---

## 1. Overzicht

### 1.1 Concept Statement

[1-2 zinnen die je game beschrijven]

### 1.2 Elevator Pitch

[30 seconden beschrijving - wat maakt je game uniek?]

### 1.3 Genre

- Primair: Arcade / Maze
- Subgenre: [jouw twist, bijv. Horror, Puzzle, etc.]

### 1.4 Platform

- Unity 2D
- PC (Windows)

### 1.5 Doelgroep

- Leeftijd: [bijv. 10+]
- Speelervaring: [casual/hardcore]
- Waarom spreekt dit hen aan: [...]

---

## 2. Gameplay

### 2.1 Core Gameplay Loop
```

[Beschrijf de cyclus: wat doet speler steeds opnieuw?]
Actie 1 → Actie 2 → Beloning → Herhaal

```

### 2.2 Belangrijkste Mechanics

#### Mechanic 1: [Naam]
- **Beschrijving**: [Wat is het?]
- **Input**: [Hoe activeert speler dit?]
- **Feedback**: [Wat ziet/hoort speler?]

#### Mechanic 2: [Naam]
[Herhaal voor elke mechanic]

### 2.3 Controls

| Actie | Input |
|-------|-------|
| Bewegen | WASD / Pijltjestoetsen |
| [Actie] | [Toets] |

### 2.4 Win Conditie
[Wanneer wint de speler?]

### 2.5 Lose Conditie
[Wanneer verliest de speler?]

---

## 3. Game Elementen

### 3.1 De Speler

| Eigenschap | Waarde |
|------------|--------|
| Naam/Uiterlijk | [Beschrijving] |
| Snelheid | [relatief: langzaam/gemiddeld/snel] |
| Levens | [aantal] |
| Speciale abilities | [indien van toepassing] |

### 3.2 Vijanden

#### Vijand 1: [Naam]
- **Uiterlijk**: [Beschrijving]
- **Gedrag**: [Hoe beweegt/reageert deze?]
- **Bedreiging**: [Wat doet deze met speler?]

### 3.3 Collectibles

| Item | Functie | Punten |
|------|---------|--------|
| [Dot equivalent] | [Wat doet het?] | [Score] |
| [Power-up] | [Effect] | [Score] |

### 3.4 Level Design

- **Grid grootte**: [bijv. 15x15]
- **Elementen**:
  - Muren
  - Paden
  - [Speciale gebieden]

[Schets van level layout]

---

## 4. Visuele Stijl

### 4.1 Art Direction
[Beschrijf de gewenste look & feel]
- Kleurenpalet: [kleuren]
- Stijl: [pixel art / vector / etc.]

### 4.2 Referentie Afbeeldingen
[Plak hier afbeeldingen of links naar inspiratie]

### 4.3 UI Stijl
- Font stijl: [...]
- Kleuren voor UI: [...]
- HUD elementen: [wat zie je tijdens gameplay?]

---

## 5. Audio

### 5.1 Muziek
- Stijl: [genre]
- Referenties: [vergelijkbare games/tracks]

### 5.2 Sound Effects
| Actie | Geluid Beschrijving |
|-------|---------------------|
| Dot pakken | [korte "pop"] |
| Game over | [...] |

---

## 6. Scope

### 6.1 Must Have (zonder dit is het geen game)
- [ ] Player kan bewegen
- [ ] [...]

### 6.2 Should Have (belangrijk)
- [ ] Score systeem
- [ ] [...]

### 6.3 Could Have (als we tijd over hebben)
- [ ] [...]

### 6.4 Won't Have (out of scope)
- [ ] Multiplayer
- [ ] [...]

---

## Changelog

| Datum | Versie | Wijzigingen |
|-------|--------|-------------|
| [datum] | 0.1 | Eerste opzet |
```

---

## Oefeningen (60 min)

### Oefening 1: GDD Opstarten (30 min)

1. Maak een nieuw Markdown bestand: `GDD_[GameNaam].md`
2. Kopieer het template
3. Vul in wat je al weet uit Les 1.2:
   - Overzicht (sectie 1)
   - Core Loop (sectie 2.1)
   - Win/Lose condities (sectie 2.4, 2.5)

### Oefening 2: MoSCoW Prioritering (15 min)

1. Brainstorm alle features die je wilt
2. Sorteer ze in Must/Should/Could/Won't
3. Vul sectie 6 in

**Let op:** Wees realistisch! Je hebt ~6 weken.

### Oefening 3: Visuele Referenties (15 min)

1. Zoek 3-5 afbeeldingen die je stijl representeren
2. Dit kunnen zijn:
   - Screenshots van andere games
   - Kunst/illustraties
   - Kleurenpaletten
3. Voeg toe aan je GDD met uitleg waarom

**Tip:** Gebruik [coolors.co](https://coolors.co) voor kleurenpaletten.

---

## Tips voor een Goed GDD

✅ **Doe dit:**

- Houd het kort en scanbaar
- Gebruik bullets en tabellen
- Update regelmatig
- Voeg afbeeldingen/schetsen toe
- Laat teamgenoot reviewen

❌ **Vermijd dit:**

- Lange lappen tekst
- Vage beschrijvingen ("het moet cool zijn")
- Te veel detail voor onbelangrijke features
- Nooit meer updaten na eerste versie

---

## Deliverables

Aan het einde van deze les heb je:

- [ ] GDD bestand aangemaakt
- [ ] Sectie 1 (Overzicht) ingevuld
- [ ] Sectie 2.1, 2.4, 2.5 ingevuld
- [ ] Sectie 6 (Scope) ingevuld met MoSCoW
- [ ] Minstens 3 visuele referenties verzameld

---

## Volgende Les

In **Les 3.1** gaan we player movement, input handling en collision detection implementeren!
