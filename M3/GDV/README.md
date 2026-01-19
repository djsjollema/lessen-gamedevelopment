# Lessen Gamedevelopment (GDV)

## Inleiding

Welkom in deze module Gamedevelopment! In deze module gaan we minimaal **2 kleine arcade-style games** bouwen. Hierbij leren we de fundamentele programmeerconcepten die je in elk game nodig hebt.

### Aanpak

Deze module behandelt **basisconcepten (technieken)** die je moet begrijpen én toepassen:

- Per les leggen we **één specifieke techniek** uit (bv. Rigidbody2D, Collisions, etc.)
- We laten **niet zien hoe je de complete games bouwt**, maar wel hoe je iedere techniek toepast
- Je maakt zelf de **vertaling naar je eigen game**

### Leren door Oefenen

Elke les volgt hetzelfde patroon:

1. **Theorie** - Uitleg van het concept
2. **Voorbeeld** - Hoe het in een echte game werkt
3. **Oefening** - Een kleine praktijk-opdracht (niet aan games gekoppeld)
4. **Toepassing** - Je past het toe in je eigen game

De oefeningen kunnen snel in één les gemaakt worden. Dit helpt je de techniek te begrijpen voordat je het in je game toepast.

### Leervolgorde

Iedereen **start met Flappy Bird** (warming up met basis-concepten)

Daarna kies je:

- **Asteroids** of **Joust** (afhankelijk van voorkeur)
  - Technieken van Flappy Bird komen ook terug in deze games
  - Asteroids en Joust delen bepaalde concepten met elkaar

**Advies:** Doe alle lessen en oefeningen - alles is relevant!

### Werkschema

| Lessen          | Activiteit                                       |
| --------------- | ------------------------------------------------ |
| **HNR-lessen**  | Werk aan theorie-lessen en bijhorende oefeningen |
| **VERI-lessen** | Pas de technieken toe in je eigen game           |

### Verwachtingen en Doelen

Eind van deze module moet je:

- Alle oefeningen hebben gemaakt en ingeleverd (via GitHub README presentatie)
- Minimaal 2 games hebben afgerond
- Alle basis-concepten begrijpen en kunnen toepassen

### Tijd en Ondersteuning

**Inzet:**

- 4 uur les per week (GDV)
- 2 uur huiswerk per week (oefeningen en game-development)

**Support:**

- Docenten beschikbaar tijdens lessen
- Hulp via Teams ook buiten lestijd
- Vraag snel hulp als je ergens niet uitkomt!

### Aanbevolen Snelheid

Werk elke week aan **minimaal 2 lessen/oefeningen** om goed op schema te blijven.

## Game 1. Flappy Bird :smiley_cat: (Zeer goed te doen)

### Overzicht

Flappy Bird is een casual mobiel spel waarbij de speler een vogel bestuurt die door verticale buizen vliegt. De speler raakt de scherm aan om de vogel omhoog te doen vliegen. Zonder input valt de vogel naar beneden door de zwaartekracht. Het doel is om zoveel mogelijk buizen voorbij te gaan zonder ze aan te raken.

<img height=200 src=https://media3.giphy.com/media/v1.Y2lkPTc5MGI3NjExOXVkbmhjcXA5M3NlYXMxcnpub24yM2xsd3FxYzR3djV5bzNtdXYxOSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/euuaA2cwLEUuI/giphy.gif />

### Core Mechanics

#### 1. **Bird Control**

<details>

- **Invoer:**
  - Muis-klik of SPATIE voor flap (sprongetje omhoog)
  - Geen input = vallen door zwaartekracht
- **Beweging:**
  - Vogel stijgt snel omhoog bij flap
  - Lineaire snelheid naar beneden (zwaartekracht)
  - Horizontale beweging constant naar rechts
- **Animatie:** Vogel roteert op basis van verticale snelheid

</details>

#### 2. **Pipe Generation**

<details>

- **Obstakels:** Paren van verticale buizen (boven en onder)
- **Gat:** Variabele opening tussen boven- en onderbuis
- **Spawning:** Buizen verschijnen aan rechterkant met regelmatige intervallen
- **Beweging:** Buizen schuiven naar links (of vogel beweegt relatief naar rechts)
- **Verwijdering:** Buizen verdwijnen aan linkerkant na passeren

</details>

#### 3. **Collision Detection**

<details>

- **Pipe Collision:** Vogel raakt buis = Game Over
- **Ground/Ceiling Collision:** Vogel raakt grond of bovenkant = Game Over
- **Pipe Passing:** Vogel passeert veilig door gat = +1 score

</details>

#### 4. **Scoring System**

<details>

- **Per Buis:** +1 punt voor elke succesvolle passage
- **High Score:** Weergeven van beste prestatie
- **Game Over Score:** Tonen huidige en best behaalde score

</details>

#### 5. **Physics**

<details>

- **Zwaartekracht:** Constante neerwaartse versnelling
- **Flap Force:** Instant snelheidswijziging omhoog
- **Terminal Velocity:** Maximale valsnelheid
- **No Acceleration:** Vogel versnelt niet horizontaal

</details>

#### 6. **Game States**

<details>

- **Start:** Vogel wachten op eerste flap
- **Playing:** Actieve gameplay
- **Game Over:** Vogelbotsing, optie om opnieuw te starten

</details>

### Noodzakelijke Code Concepten

- `Rigidbody2D` voor gravity en physica
- `AddForce()` of directe velocity-aanpassing voor flap
- `OnTriggerEnter2D()` voor collision detection buizen
- Instantiate/pooling voor pipe generation
- Random gat-positie per buis
- UI-update voor score en high score

---

## Game 2. Asteroids :construction_worker: (Hard werken)

### Overzicht

Asteroids is een arcade shoot-em-up waar de speler een driehoekig ruimteschip bestuurt. Het doel is om alle asteroïden te vernietigen zonder geraakt te worden. Vernietigde asteroïden splitsen in kleinere stukken.

<img height=200 src=https://media3.giphy.com/media/v1.Y2lkPTc5MGI3NjExcHdsbDRrZmFnMjZzM2Jrc2FvbWtxcXducjl2Znl0ZTdwYWZkYXdhOCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/l2QDNEIwuqlSFjWYo/giphy.gif />

### Core Mechanics

#### 1. **Spaceship Control**

<details>

- **Invoer:**
  - Pijltoetsen LINKS/RECHTS voor rotatie
  - Pijltoets OMHOOG voor acceleratie voorwaarts
  - SPATIE voor schieten
- **Beweging:**
  - Rotatie rond eigen as (Z-as in 2D)
  - Lineaire versnelling in neus-richting
  - Inertia: schip blijft bewegen als je geen input geeft
- **Scherm Wrapping:** Schip verdwijnt aan één kant en verschijnt aan andere kant

</details>

#### 2. **Wapen System**

<details>

- **Projectielen:** Kogels die van het schip schieten
- **Snelheid:** Vaste snelheid + snelheid van het schip
- **Richting:** Dezelfde richting als het schip neus
- **Lifespan:** Projectielen verdwijnen na bepaalde tijd of buiten scherm
- **Fire Rate:** Cooldown tussen shots (geen spammen)

</details>

#### 3. **Asteroid Mechanics**

<details>

- **Soorten:**
  - Grote asteroïden (slow, veel punten)
  - Middelgrote asteroïden (faster, medium punten)
  - Kleine asteroïden (fastest, weinig punten)
- **Beweging:**
  - Lineaire beweging in willekeurige richting
  - Rotatie/tumble effect
- **Spawning:**
  - Grote asteroïden spawnen bij level start
  - Middelgrote + kleine asteroïden spawnen als grote wordt vernietigd
  - Maximum aantal asteroïden op scherm
- **Collision:**
  - Asteroïden botsen niet met elkaar (passeren door)
  - Asteroïden botsen met schip = schade/leven verlies

</details>

#### 4. **Collision Detection**

<details>

- **Projectiel + Asteroid:** Asteroïde vernietigd, splits in kleinere stukken
- **Asteroid + Spaceship:** Schip geraakt, verliest leven
- **Screen Wrapping:** Objecten verdwijnen en verschijnen aan andere kant

</details>

#### 5. **Scoring System**

<details>

- **Per Asteroïde:**
  - Grote: 20 punten
  - Middelgrote: 50 punten
  - Kleine: 100 punten
- **Level Complete:** Als alle asteroïden vernietigd → level complete
- **Score Multiplier:** Optioneel bonus per niveau

</details>

#### 6. **Lives & Game Over**

<details>

- **Start Lives:** 3-5 levens
- **Lose Life:** When schip geraakt door asteroïde
- **Invulnerability:** Korte periode onschadelijk na hit
- **Game Over:** Geen levens meer over

</details>

#### 7. **Wave/Level System**

<details>

- **Difficulty Scaling:**
  - Meer asteroïden per level
  - Snellere asteroïden
  - Minder spawntijd tussen asteroïden

</details>

### Noodzakelijke Code Concepten

- `transform.Rotate()` voor schip-rotatie
- `Physics2D.OverlapCircle()` of raycasts voor collision
- `Vector2.Lerp()` voor smooth acceleration/deceleration
- Object pooling voor asteroïden en projectielen
- Randomness voor asteroïden-spawning
- Screen boundary wrapping met modulo-berekeningen

---

## Game 3. Joust :scream_cat: (Pittig!)

### Overzicht

Joust is een arcade-actie spel waarbij twee ridders boven op elkaar moeten botsen. Spelers besturen hun ridders op vliegende struisvogels en proberen elkaar aan te vallen van bovenaf op de tegenstander te landen. Dit gebeurt boven een lava-achtige ondergrond met een aantal platforms erboven. Het doel is om alle tegenstanders uit te schakelen zonder zelf in het magma te vallen of getrokken te worden (door een hand). Ook is er een buizerd die iedereen aanvalt in het veld als het te lang duurt voordat alle tegenstanders zijn verslagen.

<img height=200 src=./src/Joust.gif />

### Core Mechanics

#### 1. **Player Control**

<details>

- **Invoer:**
  - Pijltoetsen LINKS/RECHTS voor beweging
  - PIJLTJE OMHOOG of SPATIE voor vleugels slaan (vliegen/opstijgen)
- **Beweging:**
  - Horizontale beweging links/rechts
  - Verticale beweging door vleugelslagen (flappen)
  - Zwaartekracht trekt ridder omlaag
- **Hoogte Management:** Speler moet hoogte behouden door te flappen

</details>

#### 2. **Combat System**

<details>

- **Attack:** Ridder aanvallen van hoger vliegende positie (boven tegenstander)
- **Hoogte Voordeel:** Alleen bovenste speler kan schade uitdelen bij botsing
- **Vijand Transformatie:** Verslagen vijand transformeert tot ander type , ridder en vogel apart
- **Wave Escalation:** Meer vijanden per ronde, sneller en agressiever

</details>

#### 3. **Enemy AI**

<details>

- **Tegenstanders:** Andere ridders/vogels met AI
- **Behavior:** Jagen op speler, proberen hoger te vliegen
- **Wave System:** Meerdere tegenstanders tegelijk
- **Respawning:** Verslagen vijanden komen terug als volgende ronde

</details>

#### 4. **Collision Detection**

<details>

- **Ridder-Ridder:** Botsing resulteert in schade (hoogte bepaalt uitkomst)
- **Lava Collision:** Raken van ondergrond/magma = verlies van leven
- **Screen Wrapping:** Ridders verdwijnen links/rechts en verschijnen aan andere kant

</details>

#### 5. **Scoring System**

<details>

- **Per Tegenstander:** Punten voor verslaan van vijand
- **Wave Bonus:** Bonus voor alle tegenstanders verslaan
- **Survival:** Extra punten voor niet in lava vallen
- **High Score:** Meest behaalde punten

</details>

#### 6. **Physics**

<details>

- **Zwaartekracht:** Constante neerwaartse kracht
- **Flap Mechanics:** Korte opwaarts-impuls per vleugelslag
- **Terminal Velocity:** Maximale valsnelheid
- **Momentum:** Behoud van horizontale snelheid

</details>

#### 7. **Game Progression**

<details>

- **Waves/Levels:** Oplopende moeilijkheid
- **Lives System:** Aantal pogingen voordat Game Over
- **Level Complete:** Alle tegenstanders verslaan → volgende wave
- **Game Over:** Geen levens meer

</details>

### Noodzakelijke Code Concepten

- `Rigidbody2D` met zwaartekracht voor vlieg-mechanica
- `AddForce()` voor flap/vleugelslagen
- `OnCollisionEnter2D()` voor ridder-ridder en lava-botsingen
- Hoogte-berekening voor combat outcome
- AI-pathfinding voor tegenstanders (simpel volgen van speler)
- Wave-management en enemy-spawning
- Screen wrapping voor horizontale beweging

---
