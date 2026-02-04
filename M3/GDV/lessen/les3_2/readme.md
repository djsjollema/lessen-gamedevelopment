# Les 3.2 - Game Design Document (Deel 2)

## Leerdoelen

Na deze les kun je:

- Game mechanics gedetailleerd beschrijven
- Balancing overwegingen documenteren
- Level design specificaties maken
- Je GDD updaten met technische inzichten

---

## Deel 1: GDD Review & Update (15 min)

### Checklist Vorige Les

Controleer of je GDD de volgende secties bevat:

- [ ] Overzicht (titel, pitch, genre, platform)
- [ ] Core gameplay loop
- [ ] Win/Lose condities
- [ ] Scope (MoSCoW)
- [ ] Visuele referenties

### Vragen voor Reflectie

Bespreek met je duo:

1. Is onze twist nog steeds haalbaar na Les 3.1?
2. Hebben we nieuwe ideeën gekregen tijdens het programmeren?
3. Moeten we iets schrappen of toevoegen?

---

## Deel 2: Mechanics Detailleren (20 min)

### Mechanic Beschrijving Template

Voor elke belangrijke mechanic, documenteer:

```markdown
### Mechanic: [Naam]

**Beschrijving**
[Wat doet deze mechanic?]

**Trigger**
[Hoe/wanneer wordt dit geactiveerd?]

**Regels**

1. [Regel 1]
2. [Regel 2]
3. [...]

**Feedback**

- Visueel: [Wat ziet de speler?]
- Audio: [Wat hoort de speler?]
- Gameplay: [Wat verandert er?]

**Edge Cases**

- Wat gebeurt als [situatie]?
- Wat als [situatie]?

**Balancing Variabelen**
| Variabele | Waarde | Notities |
|-----------|--------|----------|
| [var naam] | [waarde] | [waarom] |
```

### Voorbeeld: Movement Mechanic

```markdown
### Mechanic: Grid Movement

**Beschrijving**
De speler beweegt in 4 richtingen over een grid-based level.

**Trigger**

- WASD of pijltjestoetsen
- Continu: speler blijft bewegen in huidige richting

**Regels**

1. Speler kan alleen horizontaal OF verticaal bewegen, niet diagonaal
2. Beweging stopt bij muren
3. Nieuwe input wordt gebufferd en uitgevoerd zodra mogelijk
4. Speler wrapt naar andere kant bij tunnel exits

**Feedback**

- Visueel: Karakter draait in bewegingsrichting
- Audio: Zacht "wakka wakka" geluid tijdens beweging
- Gameplay: Dots worden opgegeten bij overlap

**Edge Cases**

- Wat als speler in hoek zit? → Kan alleen terug
- Wat als 2 richtingen tegelijk? → Laatste input wint

**Balancing Variabelen**
| Variabele | Waarde | Notities |
|-----------|--------|----------|
| moveSpeed | 5 units/sec | Iets sneller dan ghosts |
| gridSize | 1 unit | Match met tile size |
| inputBuffer | 0.3 sec | Tijd om richting te bufferen |
```

---

## Deel 3: Balancing Document (15 min)

### Waarom Balancing Documenteren?

- Makkelijker tweaken tijdens development
- Voorkomt "random" waardes in code
- Basis voor playtesting feedback

### Balancing Sheet Template

```markdown
## Balancing Sheet

### Snelheden

| Entity          | Base Speed | Power-up Speed | Notes                        |
| --------------- | ---------- | -------------- | ---------------------------- |
| Player          | 5.0        | 5.5            | Iets sneller met power-up    |
| Ghost (normaal) | 4.5        | 2.0            | Langzamer tijdens frightened |
| Ghost (jacht)   | 5.5        | -              | Sneller dan player           |

### Timing

| Event            | Duur    | Notes                    |
| ---------------- | ------- | ------------------------ |
| Power-up effect  | 10 sec  | Ghosts blauw             |
| Ghost respawn    | 5 sec   | Na opgegeten             |
| Level time limit | 120 sec | Indien van toepassing    |
| Warning flash    | 3 sec   | Voordat power-up afloopt |

### Scoring

| Actie        | Punten   | Multiplier       |
| ------------ | -------- | ---------------- |
| Dot          | 10       | -                |
| Power Pellet | 50       | -                |
| Ghost #1     | 200      | x1               |
| Ghost #2     | 400      | x2               |
| Ghost #3     | 800      | x4               |
| Ghost #4     | 1600     | x8               |
| Fruit        | 100-1000 | Varies per level |

### Lives & Difficulty

| Waarde                     | Start        | Notes     |
| -------------------------- | ------------ | --------- |
| Starting Lives             | 3            |           |
| Extra life at              | 10000 pts    |           |
| Ghost speed increase       | +0.1/level   | Per level |
| Power-up duration decrease | -1 sec/level | Min 3 sec |
```

---

## Deel 4: Level Design Specs (10 min)

### Level Design Overwegingen

Documenteer voor je levels:

```markdown
## Level Design Specifications

### Grid Specificaties

- Grid size: 28 x 31 tiles
- Tile size: 1 Unity unit
- Origin: Center of grid

### Tile Types

| ID  | Type         | Beschrijving                  |
| --- | ------------ | ----------------------------- |
| 0   | Empty        | Walkable, geen item           |
| 1   | Wall         | Blokkade                      |
| 2   | Dot          | Collectible, 10 pts           |
| 3   | Power Pellet | Collectible, 50 pts, power-up |
| 4   | Player Spawn | Start positie speler          |
| 5   | Ghost Spawn  | Start positie ghosts          |
| 6   | Tunnel       | Wrap naar andere kant         |

### Level Layout Regels

1. Buitenmuren altijd gesloten (geen ontsnapping)
2. Minimaal 2 routes tussen punten (geen dead ends voor speler)
3. Ghost house in het midden
4. 4 Power Pellets in de hoeken
5. Tunnels links en rechts voor wrapping

### Level Schets
```

[Plak hier een schets of ASCII art van je level]

1 1 1 1 1 1 1 1 1
1 2 2 2 2 2 2 2 1
1 2 1 1 2 1 1 2 1
1 3 1 5 2 5 1 3 1
1 2 1 1 2 1 1 2 1
1 2 2 2 4 2 2 2 1
1 1 1 1 1 1 1 1 1

```

```

---

## Oefeningen (60 min)

### Oefening 1: Mechanics Detailleren (25 min)

Kies **3 belangrijke mechanics** uit je game en documenteer ze volledig:

1. **Movement mechanic** (hoe beweegt de speler?)
2. **Je twist mechanic** (wat maakt jouw game uniek?)
3. **Vijand gedrag** (hoe gedragen vijanden zich?)

Gebruik het template uit Deel 2.

### Oefening 2: Balancing Sheet (15 min)

Maak een eerste versie van je Balancing Sheet:

1. Alle snelheden (speler, vijanden)
2. Alle timing (power-ups, respawns)
3. Alle scoring (punten per actie)
4. Lives en difficulty progression

**Tip:** Begin met schattingen, je past dit aan tijdens playtesting.

### Oefening 3: Level Schets (20 min)

1. Maak een schets van je eerste level:
   - Potlood/pen op papier OF
   - Digitaal (Paint, Figma, etc.)
   - ASCII art

2. Markeer:
   - Spawn punten
   - Power pellet locaties
   - Belangrijke kruispunten
   - Je unieke elementen (voor je twist)

3. Vertaal naar een tile grid:
   - Bepaal grid grootte
   - Nummer elk tile type
   - Schrijf uit als array (voor je code)

---

## GDD Checklist

Na deze les moet je GDD bevatten:

### Sectie 1: Overzicht ✓

- [x] Titel, pitch, genre, platform, doelgroep

### Sectie 2: Gameplay ✓

- [x] Core loop
- [x] Gedetailleerde mechanics (minimaal 3)
- [x] Controls
- [x] Win/Lose condities

### Sectie 3: Game Elementen

- [ ] Speler specificaties
- [ ] Vijand specificaties
- [ ] Collectibles
- [x] Level design specs

### Sectie 4: Visuele Stijl ✓

- [x] Art direction
- [x] Referenties

### Sectie 5: Audio

- [ ] Muziek stijl
- [ ] Sound effects (in te vullen later)

### Sectie 6: Scope ✓

- [x] MoSCoW prioritering

### Sectie 7: Balancing (nieuw!)

- [x] Snelheden
- [x] Timing
- [x] Scoring
- [x] Difficulty

---

## Tips

### Voor Goede Mechanics Documentatie

✅ **Wees specifiek**

- Niet: "Speler kan power-up pakken"
- Wel: "Bij collision met Power Pellet (tag: 'PowerPellet') krijgt speler 10 seconden 'Powered' state"

✅ **Denk aan edge cases**

- Wat als speler 2 power-ups snel achter elkaar pakt?
- Wat als alle ghosts al opgegeten zijn?

✅ **Houd balancing variabelen apart**

- Niet hardcoded in beschrijving
- Maakt tweaken makkelijker

### Voor Level Design

✅ **Start simpel**

- Eerste level als tutorial
- Introduceer mechanics geleidelijk

✅ **Playtest je papieren level**

- Loop met je vinger door het level
- Zijn er interessante keuzes?
- Zijn er saaie stukken?

---

## Volgende Les

In **Les 4.1** gaan we een waypoint systeem bouwen voor vijand AI beweging!
