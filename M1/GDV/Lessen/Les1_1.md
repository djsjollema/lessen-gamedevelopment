# 🎮 Les 1.1: Introductie Unity en Projectstructuur

## 🎯 Wat Ga Je Leren?

In deze les maak je kennis met Unity en leer je:

- 🌟 Wat Unity precies is en waarom het zo populair is
- 💾 Hoe je Unity installeert en je eerste project maakt
- 🗂️ De Unity interface begrijpen (alle vensters en knoppen)
- 📁 Hoe je je project organiseert (mappenstructuur)
- 🎲 Je eerste GameObject maken en manipuleren

---

## 🌟 Wat is Unity?

### 🎮 Unity in Het Kort

Unity is zoals **LEGO voor games**! Het is een programma waarmee je:

- 🎲 2D en 3D games kunt maken
- 📱 Games kunt maken voor telefoon, computer, PlayStation, Xbox en meer
- 🎨 Mooie graphics en animaties kunt toevoegen
- 🎵 Geluid en muziek kunt inbouwen
- 🕹️ Interactieve verhalen kunt vertellen

### 🏆 Waarom is Unity zo Populair?

**Grote games gemaakt met Unity:**

- 🏙️ Cities: Skylines
- 🎮 Cuphead
- 🧙‍♂️ Hearthstone
- 🏃‍♂️ Temple Run
- 🔫 Call of Duty: Mobile

**Voordelen van Unity:**

- ✅ **Gratis** om te gebruiken (voor studenten en kleine bedrijven)
- ✅ **Beginnersvriendelijk** - je hoeft geen expert te zijn
- ✅ **Veel platforms** - één game, overal spelen
- ✅ **Grote community** - veel hulp en tutorials online
- ✅ **Visual scripting** - je kunt ook zonder code beginnen

---

## 💾 Unity Installeren

### Stap 1: Unity Hub Downloaden

1. Ga naar **unity.com**
2. Klik op **"Get Unity"**
3. Kies **"Individual"** → **"Personal"** (gratis!)
4. Download **Unity Hub**

### Stap 2: Unity Hub Installeren

1. **Start de installer** die je hebt gedownload
2. **Volg de installatiestappen**
3. **Maak een Unity account** aan (gratis)
4. **Log in** in Unity Hub

### Stap 3: Unity Editor Installeren

1. Open **Unity Hub**
2. Ga naar **"Installs"** in het linker menu
3. Klik **"Install Editor"**
4. Kies de **nieuwste LTS versie** (Long Term Support)
5. **Selecteer modules:**
   - ✅ Microsoft Visual Studio Community (voor code schrijven)
   - ✅ Windows Build Support (voor PC games)
   - ✅ Android Build Support (als je mobile games wilt maken)

**⏰ Installatie duurt ongeveer 20-30 minuten**

---

## 🚀 Je Eerste Project Maken

### Stap 1: Nieuw Project Starten

1. Open **Unity Hub**
2. Klik **"New Project"**
3. Kies een **template:**
   - **3D** - Voor 3D games (zoals Mario Odyssey)
   - **2D** - Voor 2D games (zoals Mario Bros)
   - **3D Mobile** - Geoptimaliseerd voor telefoons

**🎯 Voor beginners: Kies "3D"**

### Stap 2: Project Configureren

1. **Project Name:** `Mijn Eerste Game`
2. **Location:** Kies een map op je computer (bijvoorbeeld `C:\Unity Projects\`)
3. Klik **"Create Project"**

**⏰ Unity opent nu je nieuwe project (kan 1-2 minuten duren)**

---

## 🖥️ De Unity Interface - Een Rondleiding

Wanneer Unity opent, zie je verschillende vensters. Dit noemen we de **"Interface"** of **"Layout"**.

### 🗂️ De Belangrijkste Vensters

```
┌─────────────────┬─────────────────┐
│   Hierarchy     │   Inspector     │
│   (Objecten)    │   (Details)     │
├─────────────────┼─────────────────┤
│                 │                 │
│   Scene View    │   Game View     │
│   (Bouwen)      │   (Spelen)      │
│                 │                 │
├─────────────────┴─────────────────┤
│          Project Window           │
│          (Bestanden)              │
└───────────────────────────────────┘
```

### 1. 📋 Hierarchy Window (Linksboven)

**Wat is dit?**

- Een **lijst van alle objecten** in je huidige scene
- Zoals een inhoudsopgave van je level
- Hier zie je alles wat in je game zit

**Wat zie je standaard?**

- 📷 **Main Camera** - De camera waarmee spelers je game zien
- ☀️ **Directional Light** - Zonlicht dat alles verlicht

**🏠 Vergelijking:** Dit is zoals een plattegrond van je huis - het toont alle kamers en objecten.

### 2. 🎮 Scene View (Midden-links)

**Wat is dit?**

- Je **werkplek** waar je je game bouwt
- Hier plaats je objecten, beweeg je dingen rond, en ontwerp je levels
- Zoals een 3D versie van Paint, maar dan voor games

**🛠️ Navigatie:**

- **Rechtermuisknop + slepen** = Rondkijken
- **Scrollwiel** = In- en uitzoomen
- **Middelste muisknop + slepen** = Verplaatsen

### 3. 🕹️ Game View (Midden-rechts, vaak verstopt achter Scene View)

**Wat is dit?**

- Hier zie je **precies wat de speler ziet**
- Wanneer je op **Play** drukt, zie je hier je game in actie
- Dit is het eindresultaat

**🎬 Vergelijking:** Scene View is zoals achter de schermen van een film, Game View is wat het publiek ziet.

### 4. 🔍 Inspector Window (Rechtsboven)

**Wat is dit?**

- Toont **alle details** van het geselecteerde object
- Hier verander je eigenschappen zoals kleur, grootte, positie
- Hier voeg je **components** toe (functies aan objecten)

**📝 Vergelijking:** Dit is zoals het eigenschappen-menu van een bestand op je computer.

### 5. 📁 Project Window (Onderaan)

**Wat is dit?**

- Je **bestandenverkenner** binnen Unity
- Hier staan alle assets: afbeeldingen, geluiden, scripts, 3D modellen
- Organiseer hier al je game-materiaal

---

## 🎲 Je Eerste GameObject

### Wat is een GameObject?

Een **GameObject** is alles wat in je game kan bestaan:

- 🏃‍♂️ De speler
- 👾 Vijanden
- 🧱 Muren
- 💎 Verzamelobjecten
- 🌳 Bomen
- ☁️ Wolken

**Alles in Unity is een GameObject!**

### Een Kubus Maken

1. **Rechtsklik** in de Hierarchy
2. Ga naar **3D Object → Cube**
3. **Een kubus verschijnt** in je Scene!

### 🎮 Experimenteren met je Kubus

#### Selecteren en Verplaatsen

1. **Klik** op je kubus in de Scene of Hierarchy
2. Je ziet **gekleurde pijlen** (Gizmos) verschijnen:
   - 🔴 **Rode pijl** = X-as (links/rechts)
   - 🟢 **Groene pijl** = Y-as (omhoog/omlaag)
   - 🔵 **Blauwe pijl** = Z-as (vooruit/achteruit)
3. **Sleep** aan de pijlen om je kubus te verplaatsen

#### Tools Gebruiken

In de linkerbovenhoek zie je **tools** (of druk Q, W, E, R):

- **🖐️ Hand Tool (Q)** - Navigeren door de scene
- **➡️ Move Tool (W)** - Objecten verplaatsen
- **🔄 Rotate Tool (E)** - Objecten draaien
- **📐 Scale Tool (R)** - Objecten groter/kleiner maken

#### Inspector Properties

Met je kubus geselecteerd, kijk naar de **Inspector**:

**🎯 Transform Component:**

- **Position** - Waar staat het object? (X, Y, Z coördinaten)
- **Rotation** - Hoe is het object gedraaid? (in graden)
- **Scale** - Hoe groot is het object? (1 = normaal, 2 = dubbel zo groot)

**🎨 Probeer dit:**

- Zet Position Y op **5** → kubus zweeft in de lucht!
- Zet Rotation Y op **45** → kubus draait scheef!
- Zet Scale X op **3** → kubus wordt breed!

---

## 📁 Project Organisatie

### 🗂️ Waarom Organisatie Belangrijk Is

Stel je voor dat je kamer één grote chaos is - je vindt nooit iets terug! Hetzelfde geldt voor Unity projecten.

**🏠 Een goed georganiseerd project:**

```
Assets/
├── 📁 Scripts/          (Al je code)
├── 📁 Materials/        (Kleuren en textures)
├── 📁 Textures/         (Afbeeldingen)
├── 📁 Audio/            (Geluiden en muziek)
├── 📁 Prefabs/          (Herbruikbare objecten)
├── 📁 Scenes/           (Levels)
└── 📁 Models/           (3D objecten)
```

### 📂 Mappen Maken

1. **Rechtsklik** in het Project window
2. Kies **Create → Folder**
3. Geef je map een **duidelijke naam**
4. **Sleep bestanden** naar de juiste mappen

### 🎯 Naamgeving Tips

✅ **Goede namen:**

- `PlayerScript`
- `EnemyTexture`
- `JumpSound`
- `Level1Scene`

❌ **Slechte namen:**

- `Script1`
- `Untitled`
- `asdf`
- `New Material`

---

## 🎨 Meer GameObjects Uitproberen

### Basis 3D Objecten

Maak verschillende objecten (Hierarchy → 3D Object):

- **🎲 Cube** - Blokken, dozen, gebouwen
- **⚽ Sphere** - Ballen, planeten, kogels
- **🍃 Capsule** - Spelers, pilaren
- **📦 Cylinder** - Zuilen, wielen, bomen
- **📐 Plane** - Grond, water, muren

### 🌟 Licht en Camera

- **💡 Light** - Verschillende soorten verlichting
- **📷 Camera** - Extra camera's voor verschillende perspectieven

### 🎮 Praktische Oefening

**Bouw een simpel landschap:**

1. Maak een **Plane** → Dit is je grond
2. Maak een **Cube** → Dit is een huis
3. Maak een **Cylinder** → Dit is een boom
4. Maak een **Sphere** → Dit is de zon
5. **Verplaats alles** naar leuke posities
6. **Druk op Play** en kijk rond met je muis!

---

## 🎬 Scenes - Je Game Levels

### Wat is een Scene?

Een **Scene** is zoals een **level** of **scherm** in je game:

- 🏠 **Hoofdmenu** = Scene 1
- 🌳 **Level 1** = Scene 2
- 🏰 **Level 2** = Scene 3
- 🏆 **Game Over scherm** = Scene 4

### Scene Opslaan

1. Ga naar **File → Save Scene**
2. Geef je scene een naam: `TestScene`
3. Sla op in je **Scenes** map

### Nieuwe Scene Maken

1. **File → New Scene**
2. Kies **Basic (Built-in)** template
3. Je krijgt een lege scene met camera en licht

---

## 🎓 Wat Heb Je Geleerd?

### ✅ Checklist

- [ ] Je weet wat Unity is en waarom het gebruikt wordt
- [ ] Je hebt Unity Hub en Unity Editor geïnstalleerd
- [ ] Je kunt een nieuw project aanmaken
- [ ] Je kent alle belangrijke vensters (Hierarchy, Scene, Inspector, Project)
- [ ] Je kunt GameObjects maken en manipuleren
- [ ] Je begrijpt het Transform component (Position, Rotation, Scale)
- [ ] Je weet hoe je je project moet organiseren met mappen
- [ ] Je kunt scenes opslaan en nieuwe scenes maken

### 🚀 Volgende Stap

In Les 1.2 gaan we onze eerste code schrijven! Dan leren we hoe we Unity objecten kunnen besturen met C# scripts.

---

## 🤔 Veelgestelde Vragen

### Q: Unity laadt heel langtraag, is dat normaal?

**A:** Ja! Unity heeft veel functionaliteit en moet alles inladen. De eerste keer duurt het langer.

### Q: Ik zie verschillende kleuren in mijn Scene, wat betekent dat?

**A:**

- 🔴 **Rood** = X-as (links/rechts)
- 🟢 **Groen** = Y-as (omhoog/omlaag)
- 🔵 **Blauw** = Z-as (vooruit/achteruit)

### Q: Mijn object is verdwenen, hoe vind ik het terug?

**A:**

1. Selecteer het object in de Hierarchy
2. Druk **F** om erop in te zoomen
3. Of dubbelklik op het object in de Hierarchy

### Q: Kan ik de interface aanpassen?

**A:** Ja! Sleep vensters rond, verander de grootte, of kies een andere layout via **Window → Layouts**.

---

## 🏆 Extra Uitdaging

Voor wie meer wil proberen:

### 🏠 Bouw een Huisje

1. **Plane** voor de grond
2. **Cube** voor de muren (scale omhoog voor hoogte)
3. **Pyramid** voor het dak (3D Object → kan je niet vinden? Gebruik een Cube en draai het)
4. **Cylinder** voor een schoorsteen
5. Plaats alles mooi ten opzichte van elkaar

### 🎨 Experimenteer met Kleuren

1. Selecteer een object
2. Kijk in de Inspector naar **Material**
3. Klik op het kleurvakje naast **Albedo**
4. Kies een nieuwe kleur!

**🎮 Succes met je eerste stappen in Unity!**
