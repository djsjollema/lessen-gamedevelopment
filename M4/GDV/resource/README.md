# Overzicht GDV — Module 1, 2 & 3

## Inhoudsopgave

- [Inleiding](#inleiding)
- [M1 — Fundamenten van Unity en C#](#m1--fundamenten-van-unity-en-c)
- [M2 — Peggle: Physics-based Game Development](#m2--peggle-physics-based-game-development)
- [M3 — PAC-MAN: Arcade Game Development](#m3--pac-man-arcade-game-development)
- [Overzicht opgebouwde kennis en vaardigheden](#overzicht-opgebouwde-kennis-en-vaardigheden)
- [Aanbevolen vervolgonderwerpen voor M4](#aanbevolen-vervolgonderwerpen-voor-m4)

---

## Inleiding

Dit document geeft een overzicht van alle behandelde stof in de GDV-lessen (Game Development) van **Module 1**, **Module 2** en **Module 3**. Per module wordt samengevat welke onderwerpen aan bod zijn gekomen en welke kennis en vaardigheden studenten hebben opgedaan. Aansluitend volgt een overzicht van passende vervolgonderwerpen voor Module 4.

---

## M1 — Fundamenten van Unity en C\#

> **Duur:** 8 weken (16 lessen) · **Focus:** Eerste kennismaking met Unity en C#

### Behandelde stof

| Week | Les | Onderwerp                                                                                                                        |
| :--: | :-: | -------------------------------------------------------------------------------------------------------------------------------- |
|  1   | 1.1 | Introductie Unity: interface, projectstructuur, GameObjects, Scenes, Componenten, Transform                                      |
|  1   | 1.2 | Introductie C# scripting: scriptstructuur, `MonoBehaviour`, `Start()` / `Update()`, `Debug.Log()`, comments                      |
|  2   | 2.1 | Scenes, GameObjects via code aansturen, `Vector3`, `Time.deltaTime`, bewegingspatronen (lineair, circulair, bobbing)             |
|  2   | 2.2 | Datatypes (`int`, `float`, `string`, `bool`), variabelen, operatoren, `Input.GetKey()`, `Input.GetAxis()`, if-statements (intro) |
|  3   | 3.1 | Physics: `Rigidbody`, Colliders, `AddForce()`, `ForceMode`, Physics Materials, `FixedUpdate()`                                   |
|  3   | 3.2 | Functies, parameters & argumenten, return types, DRY-principe, variable scope                                                    |
|  4   | 4.1 | Colliders vs. Triggers, Tags, Layers, Physics Layer Matrix                                                                       |
|  4   | 4.2 | Collision-events in code: `OnTriggerEnter`, `OnCollisionEnter`, `CompareTag`, `Destroy()`                                        |
|  5   | 5.1 | If / else / else-if, switch, vergelijkingsoperatoren, logische operatoren (`&&`, `\|\|`, `!`)                                    |
|  5   | 5.2 | Combineren van logica met input en botsingen, `GetComponent<T>()`, inter-script communicatie                                     |
|  6   | 6.1 | `List<T>`: toevoegen, verwijderen, itereren; lijsten in Inspector; Arrays vs. Lists; `Instantiate()`, `Random.Range()`           |
|  6   | 6.2 | For-, foreach-, while-loops, nested loops, `break` / `continue`, Coroutines (`IEnumerator`, `yield return`)                      |
| 7–8  |  —  | Toets, inhaalwerk, mini-project                                                                                                  |

### Verworven kennis & vaardigheden

- Unity-editor navigeren en projecten opzetten
- C#-basisscripts schrijven en aan GameObjects koppelen
- GameObjects besturen via Transform en Rigidbody
- Physics-systeem begrijpen en toepassen (krachten, botsingen, materialen)
- Input afhandelen (toetsenbord)
- Triggers en tags inzetten voor interactie
- Voorwaardelijke logica programmeren (if/switch)
- Scripts laten communiceren via `GetComponent<T>()`
- Dynamische collecties beheren met `List<T>`
- Loops gebruiken voor herhalende operaties
- Coroutines inzetten voor tijdgestuurde acties

---

## M2 — Peggle: Physics-based Game Development

> **Duur:** 6 weken (11 lessen) · **Focus:** Bouwen van een volledig Peggle-achtig spel

### Behandelde stof

| Week | Les | Onderwerp                                                                                                     |
| :--: | :-: | ------------------------------------------------------------------------------------------------------------- |
|  1   | 1.1 | Game concept schrijven, projectopzet, Git/GitHub repository                                                   |
|  1   | 1.2 | Herhaling C# basics + Arrays en Lists, `[SerializeField]`, inventory-systeem                                  |
|  2   | 2.1 | 2D Physics: `Rigidbody2D`, `AddForce`, `CircleCollider2D`, `Physics Material 2D`, bounciness                  |
|  2   | 2.2 | Mouse-aiming (`Mathf.Atan2`, `Quaternion.AngleAxis`), Prefabs, `Instantiate`, charge-mechanic, `LineRenderer` |
|  3   | 3.1 | Singleton pattern (`ScoreManager.Instance`), hit-registratie, score per peg, `Destroy()`                      |
|  3   | 3.2 | C# Action Events (`event Action<T>`), publisher/subscriber, Tags, combo- & multiplier-systeem                 |
|  4   | 4.1 | Unity UI Canvas, RectTransform, Anchors, Canvas Scaler, 9-slice sprites, TextMesh Pro, custom fonts           |
|  4   | 4.2 | UI koppelen aan game-logica via events, `TMP_Text`, ball-counting systeem                                     |
|  5   | 5.2 | Juice/polish: Particle System, AudioSource/AudioClip, Coroutine-based screenshake                             |
|  6   | 6.1 | Feature-checklist, peer testing, Unity Build Profiles, GitHub Releases                                        |
|  6   | 6.2 | 2D sprite-sheet animaties, Sprite Editor, Animator component                                                  |

### Verworven kennis & vaardigheden

- Een game-concept opstellen en documenteren
- 2D physics toepassen (krachten, botsing, bounciness)
- Mik- en schietmechaniek bouwen met muis-input
- Prefab-workflow beheersen (aanmaken, instantiëren, configureren)
- Singleton pattern toepassen voor centrale managers
- Event-driven architectuur opzetten met `Action<T>` (pub/sub)
- Responsive UI bouwen met Canvas, Anchors en TextMesh Pro
- UI updaten vanuit game-logica via events
- Game juice toevoegen: particles, geluid, screenshake
- Sprite-sheet animaties importeren en instellen
- Een standalone build maken en releasen via GitHub

---

## M3 — PAC-MAN: Arcade Game Development

> **Duur:** 7 weken (14 lessen) · **Focus:** PAC-MAN-achtig spel met design, testing & presentatie

### Behandelde stof

| Week | Les | Onderwerp                                                                                            |
| :--: | :-: | ---------------------------------------------------------------------------------------------------- |
|  1   | 1.1 | Herhaling programmeer-basics: variabelen, functies, conditionals, access modifiers                   |
|  1   | 1.2 | Game-analyse (Core Loop, Goal, Challenge, Feedback, Progression), brainstormen, elevator pitch       |
|  2   | 2.1 | Grid genereren met modulo-operator: level als string-array → tile-spawning met `switch`              |
|  2   | 2.2 | Tutorial-leveldesign: woordloze communicatie van mechanics via ruimtelijk ontwerp (64×36 grid)       |
|  3   | 3.1 | Input (Legacy vs. New Input System), `Rigidbody2D`-beweging, `Collider2D`, triggers, `CompareTag`    |
|  3   | 3.2 | Sprite-sheet animaties maken: slicing, Animation Clips, Animator Controller, transitions, parameters |
|  4   | 4.1 | Waypoint-navigatie: patrol-loops, `MoveTowards`, chase/flee-gedrag, ghost-AI archetypen              |
|  4   | 4.2 | Usertesting: testprotocol, observatiesheet, feedback prioriteren (High/Medium/Low)                   |
|  5   | 5.1 | AnimatorController via code: `SetFloat/Bool/Integer/Trigger`, Blend Trees, transition-instellingen   |
|  5   | 5.2 | UI: Canvas, TextMeshPro score-display, Image-based levens, Singleton `ScoreManager`                  |
|  6   | 6.1 | Game State Manager: enum-states, `DontDestroyOnLoad`, `Time.timeScale`, `PlayerPrefs`, C# events     |
|  6   | 6.2 | Polishen: Particle System, `AudioSource.PlayOneShot`, Coroutine screenshake, feedback-loop           |
|  7   | 7.1 | Code reviews: checklist (naamgeving, performance, DRY, `SerializeField`), peer feedback              |
|  7   | 7.2 | STARR-reflectie, eindpresentatie voorbereiden                                                        |

### Verworven kennis & vaardigheden

- Procedurele level-generatie vanuit data (grid met modulo)
- AI-vijandgedrag implementeren (patrol, chase, flee)
- Animator Controllers aansturen vanuit code (parameters, Blend Trees)
- Game Design Documents en tutorial-levels ontwerpen
- Usertests plannen, uitvoeren en feedback verwerken
- Game State Management opzetten met enums en events
- Data persisteren met `PlayerPrefs`
- Code reviews geven en ontvangen
- Reflecteren op eigen leerproces (STARR-methode)
- Een game presenteren met demo-GIF

---

## Overzicht opgebouwde kennis en vaardigheden

### C\# Programmeren

| Onderwerp                           | M1  | M2  | M3  |
| ----------------------------------- | :-: | :-: | :-: |
| Variabelen & datatypes              | ✅  | ✅  | ✅  |
| Functies (void, return, parameters) | ✅  | ✅  | ✅  |
| If / else / switch                  | ✅  |  —  | ✅  |
| For / foreach / while loops         | ✅  |  —  | ✅  |
| Arrays & Lists                      | ✅  | ✅  | ✅  |
| Coroutines (`IEnumerator`, `yield`) | ✅  | ✅  | ✅  |
| Enums                               |  —  |  —  | ✅  |
| Action Events (pub/sub)             |  —  | ✅  | ✅  |
| Singleton pattern                   |  —  | ✅  | ✅  |
| `GetComponent<T>()`                 | ✅  | ✅  | ✅  |
| `[SerializeField]` vs public        |  —  | ✅  | ✅  |

### Unity Engine

| Onderwerp                                 | M1  | M2  | M3  |
| ----------------------------------------- | :-: | :-: | :-: |
| Editor-navigatie & projectopzet           | ✅  | ✅  | ✅  |
| GameObjects, Componenten, Transform       | ✅  | ✅  | ✅  |
| Physics (Rigidbody, Colliders, Materials) | ✅  | ✅  | ✅  |
| Triggers & Tags                           | ✅  | ✅  | ✅  |
| Prefabs & Instantiate                     | ✅  | ✅  | ✅  |
| Input-afhandeling                         | ✅  | ✅  | ✅  |
| UI (Canvas, TextMeshPro, Anchors)         |  —  | ✅  | ✅  |
| Animator & Animation Clips                |  —  | ✅  | ✅  |
| Particle System                           |  —  | ✅  | ✅  |
| AudioSource / AudioClip                   |  —  | ✅  | ✅  |
| LineRenderer                              |  —  | ✅  |  —  |
| Camera-shake (Coroutine)                  |  —  | ✅  | ✅  |
| Build & Release                           |  —  | ✅  |  —  |
| PlayerPrefs (data opslaan)                |  —  |  —  | ✅  |
| Grid-generatie (modulo)                   |  —  |  —  | ✅  |
| Waypoint AI / navigatie                   |  —  |  —  | ✅  |
| Game State Management                     |  —  |  —  | ✅  |
| Blend Trees                               |  —  |  —  | ✅  |

### Game Design & Soft Skills

| Onderwerp              | M1  | M2  | M3  |
| ---------------------- | :-: | :-: | :-: |
| Game concept schrijven |  —  | ✅  | ✅  |
| Game Design Document   |  —  |  —  | ✅  |
| Level-/tutorial-design |  —  | ✅  | ✅  |
| Usertesting & QA       |  —  |  —  | ✅  |
| Code reviews           |  —  |  —  | ✅  |
| Reflecteren (STARR)    |  —  |  —  | ✅  |
| Presenteren            |  —  |  —  | ✅  |
| Git & GitHub           | ✅  | ✅  | ✅  |

---

## Aanbevolen vervolgonderwerpen voor M4

Op basis van de opgebouwde kennis en vaardigheden in M1–M3 zijn de volgende onderwerpen passende vervolgstappen. Ze bouwen voort op de bestaande basis en introduceren nieuwe concepten die de studenten naar een hoger niveau tillen.

---

### 1. Object-Oriented Programming (OOP) — Verdieping

> _Bouwt voort op: functies, `GetComponent`, Singleton, enums_

| Onderwerp                    | Omschrijving                                                                          |
| ---------------------------- | ------------------------------------------------------------------------------------- |
| **Inheritance (overerving)** | Baseclasses maken (bijv. `Enemy`) met afgeleide klassen (`PatrolEnemy`, `ChaseEnemy`) |
| **Interfaces**               | `IDamageable`, `ICollectible` — losse contracten definiëren voor gedrag               |
| **Abstract classes**         | Gemeenschappelijke logica in een abstracte baseclass plaatsen                         |
| **Polymorfisme**             | Verschillende objecten via dezelfde referentie aanspreken                             |
| **Encapsulation**            | Properties (`get`/`set`), `private` backing fields, data beschermen                   |

---

### 2. Design Patterns voor Games

> _Bouwt voort op: Singleton, Action Events (pub/sub), Game State Manager_

| Onderwerp                         | Omschrijving                                                                |
| --------------------------------- | --------------------------------------------------------------------------- |
| **Observer pattern (verdieping)** | Events met meerdere listeners, `UnityEvent` vs. C# `event`                  |
| **Object Pooling**                | Hergebruik van objecten in plaats van `Instantiate`/`Destroy` (performance) |
| **State pattern**                 | Game state management als formeel pattern (i.p.v. alleen enums)             |
| **Command pattern**               | Input-abstrahering, undo/redo-systemen                                      |
| **Factory pattern**               | Object-creatie abstraheren voor vijanden, power-ups, etc.                   |
| **ScriptableObjects**             | Data-driven design: configuratie losgekoppeld van code                      |

---

### 3. Geavanceerde AI & Pathfinding

> _Bouwt voort op: waypoint-navigatie, chase/flee-gedrag, grid-generatie_

| Onderwerp                      | Omschrijving                                                             |
| ------------------------------ | ------------------------------------------------------------------------ |
| **Finite State Machine (FSM)** | Formele state machine voor AI-gedrag (Idle → Patrol → Chase → Attack)    |
| **NavMesh / A\* Pathfinding**  | Unity NavMesh voor 3D of A\*-algoritme voor 2D grid-navigatie            |
| **Line of Sight**              | Raycasting voor zichtdetectie                                            |
| **Behaviour Trees**            | Complexere AI-logica via boom-structuren (sequence, selector, decorator) |

---

### 4. Tilemap & Procedurele Level-generatie

> _Bouwt voort op: grid met modulo, prefab-spawning, level-design_

| Onderwerp                 | Omschrijving                                            |
| ------------------------- | ------------------------------------------------------- |
| **Unity Tilemap**         | Tile Palette, Rule Tiles, Animated Tiles                |
| **Procedural Generation** | Random level-generatie, Perlin Noise, cellular automata |
| **Tilemap Collider 2D**   | Botsingen direct vanuit tilemaps                        |
| **Level-editor tools**    | Eigen editor-scripts voor sneller level-bouwen          |

---

### 5. Geavanceerd Animatiesysteem

> _Bouwt voort op: Animator, Blend Trees, sprite-sheet animaties_

| Onderwerp                   | Omschrijving                                                    |
| --------------------------- | --------------------------------------------------------------- |
| **Sub-state machines**      | Complexere Animator-structuren met geneste states               |
| **Animation Events**        | Functies aanroepen op specifieke animation frames               |
| **Animation Layers**        | Meerdere animatie-lagen combineren (bijv. lopen + schieten)     |
| **IK (Inverse Kinematics)** | Characters dynamisch laten reiken/kijken                        |
| **DOTween / Tweening**      | Vloeiende animaties via code (UI-animaties, easing, sequencing) |

---

### 6. Geavanceerde UI & Menu-systemen

> _Bouwt voort op: Canvas, TextMeshPro, Anchors, scoredisplay_

| Onderwerp            | Omschrijving                                                               |
| -------------------- | -------------------------------------------------------------------------- |
| **Menu-flow**        | Main menu → Settings → Gameplay → Pause → Game Over (met scene-management) |
| **UI-animaties**     | Tween-gebaseerde transities, fade-in/out, slide-effecten                   |
| **Settings-systeem** | Volume-slider, resolutie-dropdown, keybinding                              |
| **Dialogue-systeem** | NPC-dialogen met keuzes en vertakking                                      |
| **Localization**     | Meertalige UI-teksten                                                      |

---

### 7. Save/Load & Data Persistence

> _Bouwt voort op: PlayerPrefs, game state management_

| Onderwerp                      | Omschrijving                                           |
| ------------------------------ | ------------------------------------------------------ |
| **JSON serialisatie**          | `JsonUtility` of `Newtonsoft.Json` voor save-bestanden |
| **File I/O**                   | Opslaan naar en laden van bestanden (`System.IO`)      |
| **ScriptableObjects als data** | Runtime-data opslaan in assets                         |
| **Encryptie basics**           | Simpele bescherming van save-bestanden                 |
| **Cloud saves**                | Intro tot opslaan in de cloud (Steam, PlayFab)         |

---

### 8. Netwerk & Multiplayer (Introductie)

> _Bouwt voort op: events, game state management, data-structuren_

| Onderwerp                         | Omschrijving                     |
| --------------------------------- | -------------------------------- |
| **Unity Netcode for GameObjects** | Basis lobby, client-server model |
| **Network-synchronisatie**        | NetworkVariables, RPCs           |
| **Lokale multiplayer**            | Split-screen, gedeelde input     |

---

### 9. Versiebeheer & Samenwerking (Verdieping)

> _Bouwt voort op: Git/GitHub basics, code reviews_

| Onderwerp                     | Omschrijving                                            |
| ----------------------------- | ------------------------------------------------------- |
| **Git branching-strategieën** | Feature branches, Git Flow                              |
| **Pull Requests & reviews**   | Gestructureerd code-review proces via GitHub            |
| **Merge conflicts oplossen**  | Praktische oefeningen met conflicten in Unity-projecten |
| **CI/CD basics**              | Automatische builds via GitHub Actions                  |

---

### 10. Performance & Optimalisatie

> _Bouwt voort op: physics, loops, Instantiate/Destroy, Coroutines_

| Onderwerp             | Omschrijving                                      |
| --------------------- | ------------------------------------------------- |
| **Profiler**          | Unity Profiler gebruiken om bottlenecks te vinden |
| **Object Pooling**    | Hergebruik i.p.v. Instantiate/Destroy             |
| **Sprite Atlassen**   | Draw calls verminderen met atlassen               |
| **Async/Await**       | Moderne alternative voor Coroutines               |
| **Memory management** | Garbage collection begrijpen en voorkomen         |

---

### 11. 3D Game Development (Introductie)

> _Bouwt voort op: alle 2D-kennis uit M1–M3_

| Onderwerp                         | Omschrijving                                      |
| --------------------------------- | ------------------------------------------------- |
| **3D-omgeving opzetten**          | 3D project, camera, belichting                    |
| **3D physics**                    | Rigidbody (3D), MeshCollider, CharacterController |
| **First/Third Person Controller** | Basisbesturing in 3D                              |
| **ProBuilder**                    | Level-prototyping direct in Unity                 |
| **Materialen & Shaders (intro)**  | Basis van rendering en visuele effecten           |

---

### 12. Testing & Debugging (Verdieping)

> _Bouwt voort op: usertesting, code reviews, Debug.Log_

| Onderwerp                        | Omschrijving                                 |
| -------------------------------- | -------------------------------------------- |
| **Unity Test Framework**         | Unit tests schrijven voor game-logica        |
| **Assertions & Debugging tools** | `Debug.Assert`, Breakpoints in Visual Studio |
| **Playtesting-methoden**         | A/B testing, analytics, heatmaps             |
| **Bug tracking**                 | GitHub Issues als bugtracker gebruiken       |

---

### Aanbevolen selectie voor M4 GDV

Onderstaande onderwerpen vormen samen een gebalanceerd M4-programma en sluiten direct aan bij het niveau na M3:

|  Prioriteit  | Onderwerp                                                              | Reden                                                                       |
| :----------: | ---------------------------------------------------------------------- | --------------------------------------------------------------------------- |
|   🔴 Hoog    | **OOP — Inheritance & Interfaces**                                     | Essentieel volgende stap in C#; maakt code herbruikbaar en schaalbaar       |
|   🔴 Hoog    | **Design Patterns (ScriptableObjects, Object Pooling, State Pattern)** | Professionelere code-architectuur; direct toepasbaar in elk project         |
|   🔴 Hoog    | **Geavanceerde AI (FSM, Pathfinding)**                                 | Logisch vervolg op waypoint-navigatie uit M3                                |
| 🟡 Gemiddeld | **Tilemap & procedurele generatie**                                    | Verdieping van de grid-kennis uit M3 met Unity's Tilemap-systeem            |
| 🟡 Gemiddeld | **Save/Load systemen**                                                 | Verdieping van PlayerPrefs naar echte data-persistentie                     |
| 🟡 Gemiddeld | **Geavanceerde Animatie & UI**                                         | Polijsten van bestaande kennis met Animation Events, DOTween, menu-systemen |
| 🟢 Optioneel | **3D introductie / Multiplayer / Performance**                         | Verbreding voor gevorderde studenten                                        |

---

> **Gegenereerd op:** 19 februari 2026 · **Bron:** Analyse van lesmateriaal M1/GDV, M2/GDV en M3/GDV
