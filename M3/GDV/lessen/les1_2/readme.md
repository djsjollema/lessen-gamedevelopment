# Les 1.2 - Game Analyse & Concept Development

## Leerdoelen

Na deze les kun je:

- De kernmechanics van Pac-Man analyseren
- Bestaande Pac-Man varianten onderzoeken
- Een eigen concept met twist bedenken
- Je concept pitchen aan de klas

---

## Deel 1: Pac-Man Analyse (20 min)

### Core Gameplay Loop

```
Verzamel dots → Ontwijken ghosts → Power-up pakken → Ghosts eten → Level clearen
      ↑                                                                    |
      └────────────────────────────────────────────────────────────────────┘
```

### Game Elementen

| Element           | Functie                                             |
| ----------------- | --------------------------------------------------- |
| **Pac-Man**       | Speelbaar karakter, beweegt door doolhof            |
| **Dots**          | Verzamelobjecten, level klaar als alle dots op zijn |
| **Power Pellets** | Tijdelijke power-up, maakt ghosts kwetsbaar         |
| **Ghosts**        | Vijanden met elk eigen gedrag/persoonlijkheid       |
| **Doolhof**       | Speelveld met muren en paden                        |
| **Fruit**         | Bonus items voor extra punten                       |

### Ghost AI Gedrag

In de originele Pac-Man heeft elke ghost een unieke persoonlijkheid:

| Ghost     | Naam   | Gedrag                                  |
| --------- | ------ | --------------------------------------- |
| 🔴 Rood   | Blinky | Achtervolgt Pac-Man direct              |
| 🟠 Oranje | Clyde  | Wisselt tussen achtervolgen en vluchten |
| 🔵 Blauw  | Inky   | Onvoorspelbaar, combineert posities     |
| 🟢 Roze   | Pinky  | Probeert Pac-Man te onderscheppen       |

### Game States

```
Title Screen → Playing → (Paused) → Game Over / Win
                  ↑          |
                  └──────────┘
```

### Scoring Systeem

| Actie        | Punten   |
| ------------ | -------- |
| Dot          | 10       |
| Power Pellet | 50       |
| Ghost #1     | 200      |
| Ghost #2     | 400      |
| Ghost #3     | 800      |
| Ghost #4     | 1600     |
| Fruit        | 100-5000 |

---

## Deel 2: Pac-Man Varianten (15 min)

### Bekende Varianten

Onderzoek deze varianten en noteer wat ze anders doen:

| Variant                          | Twist                               |
| -------------------------------- | ----------------------------------- |
| **Ms. Pac-Man**                  | Nieuwe levels, bewegende fruit      |
| **Pac-Man Championship Edition** | Tijd-gebaseerd, procedurele levels  |
| **Pac-Man 256**                  | Endless runner stijl, glitch vijand |
| **Pac-Man Battle Royale**        | 4-speler competitief                |
| **Pac-Man Mega Tunnel Battle**   | 64 spelers, tunnels tussen arenas   |

### Twist Categorieën

Denk na over welke categorie twist je wilt toepassen:

| Categorie           | Voorbeelden                         |
| ------------------- | ----------------------------------- |
| **Perspectief**     | First-person, top-down, isometrisch |
| **Setting/Thema**   | Ruimte, onderwaterwereld, horror    |
| **Mechanic**        | Multiplayer, power-ups, crafting    |
| **Doel**            | Speedrun, high score, survival      |
| **Twist op rollen** | Speel als ghost, bescherm de dots   |

---

## Deel 3: Concept Ontwikkeling (25 min)

### Brainstorm Stappenplan

1. **Wat vinden we leuk aan Pac-Man?**
   - Noteer 3-5 dingen

2. **Wat zou beter/anders kunnen?**
   - Noteer 3-5 dingen

3. **Welke twist past bij ons?**
   - Kies een categorie
   - Brainstorm 5+ ideeën

4. **Selecteer je twist**
   - Welk idee is het meest haalbaar?
   - Welk idee is het meest origineel?

### Concept Template

Vul onderstaand template in voor je concept:

```markdown
## Game Concept: [Naam van je game]

### Elevator Pitch (1-2 zinnen)

[Beschrijf je game in 1-2 zinnen]

### De Twist

[Wat maakt jouw game uniek?]

### Core Mechanic

[Wat is de belangrijkste actie die de speler doet?]

### Win/Lose Conditie

- Win: [Wanneer win je?]
- Lose: [Wanneer verlies je?]

### Belangrijkste Features

1. [Feature 1]
2. [Feature 2]
3. [Feature 3]

### Visuele Stijl

[Beschrijf kort hoe je game eruitziet]

### Doelgroep

[Voor wie is deze game?]
```

---

## Oefeningen (60 min)

### Oefening 1: Pac-Man Spelen & Analyseren (15 min)

1. Speel de originele Pac-Man (of een online versie)
2. Beantwoord deze vragen:
   - Hoe lang duurt een gemiddeld potje?
   - Wanneer voel je spanning?
   - Wanneer voel je frustratie?
   - Wat zorgt voor "nog een keer spelen"?

**Voorbeeld antwoorden:**

```
┌─────────────────────────────────────────────────────────────┐
│ Vraag                    │ Voorbeeld antwoord               │
├─────────────────────────────────────────────────────────────┤
│ Gemiddelde speeltijd     │ 2-5 minuten per leven            │
│ Spanning                 │ Als ghosts dichtbij zijn         │
│                          │ Laatste paar dots zoeken         │
│                          │ Power-up bijna op                │
│ Frustratie               │ Net mis bij power pellet         │
│                          │ Ingesloten in hoek               │
│ Nog een keer spelen      │ "Net niet" gevoel                │
│                          │ Highscore verbeteren             │
│                          │ Verder komen dan vorige keer     │
└─────────────────────────────────────────────────────────────┘
```

### Oefening 2: Variant Onderzoek (15 min)

1. Zoek **2 Pac-Man varianten** op (YouTube gameplay)
2. Noteer per variant:
   - Wat is de twist?
   - Wat werkt goed?
   - Wat werkt minder?

### Oefening 3: Brainstorm & Concept (20 min)

1. Volg het brainstorm stappenplan met je duo
2. Vul het Concept Template in
3. Maak een **snelle schets** van hoe je game eruitziet

### Oefening 4: Pitch (10 min)

Bereid een **30 seconden pitch** voor:

- Naam van je game
- Wat is de twist?
- Waarom is het leuk?

Presenteer aan een ander duo en geef elkaar feedback.

**Voorbeeld pitch:**

```
"Onze game heet 'Ghost Hunter'.

De twist: JIJ speelt als de ghost en moet Pac-Man
vangen voordat hij alle dots opeet. Maar pas op -
Pac-Man wordt steeds sneller naarmate er minder
dots zijn!

Het is leuk omdat je nu de jager bent in plaats
van de prooi, en je moet slim samenwerken met
andere ghosts om Pac-Man in te sluiten."

[Tijd: ~25 seconden]
```

**Feedback vragen:**

- Is de twist duidelijk?
- Klinkt het speelbaar?
- Wat zou je willen weten/zien?

---

## Tips voor een Goede Twist

✅ **Doe dit:**

- Houd het simpel en haalbaar
- Focus op één grote verandering
- Zorg dat de core loop intact blijft
- Denk aan wat JIJ leuk vindt om te maken

❌ **Vermijd dit:**

- Te veel features tegelijk
- Compleet nieuwe game (het moet Pac-Man herkenbaar blijven)
- Ideeën die te moeilijk zijn voor jullie niveau

---

## Deliverables

Aan het einde van deze les heb je:

- [ ] Analyse notities van originele Pac-Man
- [ ] Onderzoek van 2 varianten
- [ ] Ingevuld Concept Template
- [ ] Schets van je game
- [ ] Gepitcht aan klasgenoten

---

## Volgende Les

In **Les 2.1** gaan we een grid-based level genereren met arrays en modulo. Dit is de basis voor jullie doolhof!
