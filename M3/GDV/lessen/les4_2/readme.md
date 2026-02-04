# Les 4.2 - Usability & Gameplay Testing

## Leerdoelen

Na deze les kun je:

- Het verschil uitleggen tussen usability en gameplay testing
- Een testplan opstellen
- Een playtest sessie uitvoeren
- Feedback verzamelen en verwerken

---

## Deel 1: Soorten Tests (15 min)

### Usability Testing

Test of spelers de game **kunnen bedienen** en **begrijpen**.

| Vraag | Focus |
|-------|-------|
| Begrijpt de speler de controls? | Input, tutorials |
| Is de UI duidelijk? | Menu's, HUD, feedback |
| Weet de speler wat te doen? | Doelen, instructies |
| Kan de speler navigeren? | Menu flow, level design |

### Gameplay Testing

Test of de game **leuk** en **gebalanceerd** is.

| Vraag | Focus |
|-------|-------|
| Is het te makkelijk/moeilijk? | Difficulty balancing |
| Is het leuk? | Core loop, engagement |
| Wil de speler nog een keer? | Replayability |
| Voelt het eerlijk? | Collision, hit detection |

### Wanneer Welke Test?

```
Development Timeline:

[Prototype] ──► [Alpha] ──► [Beta] ──► [Release]
     │              │           │
     ▼              ▼           ▼
 Usability     Gameplay     Polish
 "Werkt het?"  "Is het leuk?" "Is het af?"
```

---

## Deel 2: Testplan Opstellen (15 min)

### Testplan Template

```markdown
# Playtest Plan - [Game Naam]

## Test Informatie
- **Datum:** [datum]
- **Versie:** [build nummer/versie]
- **Testers:** [aantal en wie]
- **Duur:** [tijd per sessie]

## Test Doelen
Wat willen we leren?
1. [ ] Begrijpen spelers de controls?
2. [ ] Is level 1 te moeilijk?
3. [ ] Werkt de power-up zoals bedoeld?

## Test Scenario's
### Scenario 1: Eerste keer spelen
- Start game zonder uitleg
- Observeer: Hoe lang duurt het voor speler beweegt?
- Observeer: Probeert speler verkeerde toetsen?

### Scenario 2: Level voltooien
- Speler probeert level 1 te halen
- Meet: Tijd tot voltooien
- Meet: Aantal deaths

## Vragen Achteraf
1. Wat vond je leuk?
2. Wat vond je frustrerend?
3. Was iets onduidelijk?
4. Zou je het nog een keer spelen?

## Successcriteria
- [ ] 80% begrijpt controls binnen 30 seconden
- [ ] Level 1 haalbaar in <3 minuten
- [ ] Testers willen nog een keer spelen
```

### Goede Testvragen

✅ **Open vragen:**
- "Wat dacht je toen je dit zag?"
- "Waarom deed je dat?"
- "Wat verwachtte je dat er zou gebeuren?"

❌ **Vermijd sturende vragen:**
- "Vond je de controls intuïtief?" (suggereert antwoord)
- "Was het te moeilijk?" (ja/nee geeft weinig info)

---

## Deel 3: Playtest Uitvoeren (20 min)

### De 5 Regels van Playtesten

#### 1. Leg NIETS uit
```
❌ "Je moet WASD gebruiken om te bewegen en spatie om..."
✅ "Hier is de game, veel plezier!"
```
Als je moet uitleggen, is je game niet duidelijk genoeg.

#### 2. Niet helpen
```
❌ "Je moet naar links, daar is de uitgang"
✅ *stilte en observeren*
```
Laat de speler worstelen. Dat is waardevolle informatie.

#### 3. Niet verdedigen
```
Speler: "Dit is verwarrend"
❌ "Ja maar dat is omdat we nog geen tutorial hebben"
✅ "Interessant, wat maakt het verwarrend?"
```

#### 4. Observeer gedrag
Let op:
- Gezichtsuitdrukkingen (frustratie, blijdschap)
- Wat probeert de speler? (verkeerde toetsen?)
- Waar kijkt de speler? (mist UI elementen?)
- Hoelang duurt iets?

#### 5. Think Aloud Protocol
Vraag testers om hardop te denken:
```
"Hmm, ik zie een geel ding, ik denk dat ik dat moet pakken...
Oh wacht er komt iets aan, ik ga naar links...
Ah! Ik ben dood. Ik snapte niet dat dat een vijand was."
```

### Observatie Template

```markdown
## Observatie Log

### Tester: [naam/nummer]
### Datum: [datum]

| Tijd | Observatie | Type | Ernst |
|------|------------|------|-------|
| 0:15 | Probeert pijltjestoetsen (werkt) | Usability | - |
| 0:45 | Loopt 3x tegen zelfde muur | Usability | Medium |
| 1:20 | Zegt "Oh cool!" bij power-up | Engagement | Positief |
| 2:00 | Snapt niet dat ghost gevaarlijk is | Usability | Hoog |
| 2:30 | Geeft op, te moeilijk | Gameplay | Hoog |

### Key Insights
1. Controls worden snel begrepen
2. Vijanden niet herkenbaar als gevaar
3. Eerste level te moeilijk
```

---

## Deel 4: Feedback Verwerken (10 min)

### Feedback Categoriseren

| Categorie | Actie | Voorbeeld |
|-----------|-------|-----------|
| **Bug** | Fixen | "Game crasht bij level 2" |
| **Usability** | Verbeteren | "Wist niet wat de rode cirkel was" |
| **Balance** | Tweaken | "Ghosts zijn te snel" |
| **Feature Request** | Overwegen | "Zou leuk zijn met multiplayer" |
| **Persoonlijke voorkeur** | Negeren (meestal) | "Ik hou niet van blauw" |

### Prioriteren met Impact/Effort Matrix

```
        Hoge Impact
             │
    ┌────────┼────────┐
    │ QUICK  │  DO    │
    │ WINS   │ FIRST  │
────┼────────┼────────┼──── Effort
    │ MAYBE  │ DO     │
    │ LATER  │ LAST   │
    └────────┼────────┘
             │
        Lage Impact

Voorbeeld:
- "Ghost niet herkenbaar" → Hoge impact, lage effort → QUICK WIN
- "Multiplayer toevoegen" → Hoge impact, hoge effort → DO LAST (of never)
- "Andere font voor score" → Lage impact, lage effort → MAYBE LATER
```

### Actie Items Formuleren

```markdown
## Playtest Resultaten - Actiepunten

### Must Fix (voor volgende test)
1. [ ] Ghosts duidelijker maken als vijand (rode outline?)
2. [ ] Tutorial toevoegen voor power-up
3. [ ] Level 1 makkelijker (minder ghosts)

### Should Fix
4. [ ] Betere audio feedback bij hit
5. [ ] Score zichtbaarder maken

### Nice to Have
6. [ ] Verschillende ghost kleuren
7. [ ] Particle effect bij dot pickup
```

---

## Oefeningen (60 min)

### Oefening 1: Testplan Schrijven (15 min)

1. Kopieer het Testplan Template
2. Vul in voor jouw game:
   - 3 specifieke test doelen
   - 2 test scenario's
   - 5 vragen voor achteraf

**Voorbeeld test doelen:**
```
1. Begrijpen spelers binnen 20 sec hoe ze moeten bewegen?
2. Is de power-up effect duidelijk (weten ze dat ghosts nu eetbaar zijn)?
3. Kunnen spelers level 1 halen binnen 3 levens?
```

### Oefening 2: Playtest Sessie (30 min)

1. Wissel games met een ander duo
2. Speel elkaars game (10 min per game)
3. Observer houdt zich aan de 5 regels
4. Vul het Observatie Log in

**Observatie focus:**
```
□ Hoe lang duurt eerste beweging?
□ Welke toetsen probeert tester eerst?
□ Waar kijkt tester naar (UI, level)?
□ Wanneer toont tester frustratie/plezier?
□ Wat zegt tester hardop?
```

### Oefening 3: Feedback Verwerken (15 min)

1. Bespreek observaties met je duo
2. Categoriseer feedback (Bug/Usability/Balance/Feature)
3. Maak een lijst van top 3 verbeterpunten
4. Voeg toe aan je GDD of backlog

**Output format:**
```
## Playtest #1 - Samenvatting

### Positief
- Controls snel begrepen
- "Cool!" reactie bij power-up

### Te verbeteren
1. [Usability] Ghosts lijken niet gevaarlijk
   → Actie: Rode kleur/ogen toevoegen
   
2. [Balance] Level 1 te moeilijk (0/3 haalde het)
   → Actie: Start met 2 ghosts ipv 4
   
3. [Usability] Score niet opgemerkt
   → Actie: Score groter maken, animatie bij punten
```

---

## Playtest Checklist

### Voorbereiding
- [ ] Werkende build (geen crashes!)
- [ ] Testplan klaar
- [ ] Observatie template geprint/klaar
- [ ] Testers geregeld

### Tijdens de test
- [ ] Niet uitleggen
- [ ] Niet helpen
- [ ] Niet verdedigen
- [ ] Observeren en noteren
- [ ] Vragen achteraf stellen

### Na de test
- [ ] Feedback categoriseren
- [ ] Prioriteiten bepalen
- [ ] Actiepunten formuleren
- [ ] GDD/backlog updaten

---

## Tips voor Effectief Testen

### Hoeveel testers?

| Aantal | Vindt | Gebruik voor |
|--------|-------|--------------|
| 3-5 | ~80% van usability issues | Snelle feedback |
| 5-10 | ~90% van issues | Grondige test |
| 10+ | Statistisch relevante data | Balance testing |

### Wie als tester?

✅ **Goede testers:**
- Mensen die je game nog nooit gezien hebben
- Mensen uit je doelgroep
- Klasgenoten van andere projecten

❌ **Vermijd:**
- Jezelf (je kent de game te goed)
- Je duo partner (zelfde probleem)
- Familie die "niet wil kwetsen"

---

## Volgende Les

In **Les 5.1** gaan we animaties aanroepen in Unity!
