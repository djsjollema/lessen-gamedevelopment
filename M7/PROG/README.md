# Inhaal programma Game Programming

Revisiting basics:

# Overzicht onderwerpen M1–M6 (GDV & PROG)

Dit overzicht verzamelt de onderwerpen die in de mappen `GDV` en `PROG` (of vergelijkbare `prog`/`Prog`) voorkomen voor de modules M1 t/m M6. Het doel is snel te zien welke thema's en lesinhouden behandeld zijn.

**M1 — GDV:**

- **Unity introductie**: Wat is Unity en waarom gebruiken we het.
- **Projectstructuur & scenes**: Projecten opzetten en organiseren.
- **C# basis & scripting**: Debug.Log, comments, basisstructuur van scripts.
- **GameObjects & componenten**: Transform, componenten toevoegen en gebruiken.
- **Beweging**: DeltaTime, eenvoudige bewegingen via scripts.
- **Physics basics**: Rigidbody, colliders, botsingen en triggers.
- **If-statements en logica**: Basis beslissingsstructuren.
- **Collections & loops**: Lists, arrays, for/foreach loops.
- **Oefeningen & inleverformat**: README-format voor opdrachten, demo GIFs en code links.

**M1 — PROG:**

- Geen expliciete `PROG`-map aanwezig in M1 (alle programmeerstof zit in GDV of Skill-mappen).

**M2 — GDV:**

- **Les 1.1 / 1.2**: Concept & project opzetten; herhaling basis C# (arrays, lists).
- **Forces & collision**: Physics, friction, bounce en Rigidbody-instellingen.
- **Peggle / Aim & Line Renderer**: LineRenderer gebruiken voor aiming, materialen en dikte instellen.
- **Prefabs & importeren sprites**: Prefab maken, prefab mode, importeren van sprites.
- **Score & Triggers**: Score systemen en trigger-detectie.
- **Combos & Multiplier systems**: Combo-detectie en multipliers.
- **Leveldesign & UI**: Anchors, textfields, scoreboards en UI-opmaak.
- **Scores versturen**: Mechanieken en voorbeeld assets (beelden/gifs aanwezig in `src`).

**M2 — PROG:**

- Geen expliciete `PROG`-map gevonden in M2; programmeerpraktijk geïntegreerd in GDV-lessen.

**M3 — prog (canvas)**

- **Canvas & UI in Unity**: Wat is een Canvas, render modes (Overlay/Camera/WorldSpace).
- **Canvas Scaler**: Constant Pixel Size / Scale With Screen Size / Constant Physical Size.
- **UI-elementen**: Text, Image, Button, Panel, Slider, ScrollView.
- **RectTransform & anchors**: Positionering, pivot en sizeDelta.
- **Event System & interaction**: Button.onClick, Event Triggers.
- **Dynamische UI via scripts**: Voorbeelden met `Text`/`TMP_Text` en score updates.

**M3 — GDV:**

- Geen aparte `GDV`-map in M3; hoofdzakelijk `prog` en `BO` aanwezig.

**M4 — PROG:**

- **C# basis herhaling**: Variabelen (int, float, string, bool), if-statements, loops, functies.
- **Collections**: Arrays, Lists, Dictionaries.
- **Unity-specifiek**: MonoBehaviour, Start/Update, GetComponent, public variabelen en Inspector.
- **Game mechanics**: Beweging, collisions, score systemen, timers.
- **Prefabs & Scenes**: Instantiatie, SceneManager voor scene wissel.
- **Debugging & fouten**: NullReferenceException uitleg, Debug.Log gebruiken.
- **Vector3 verdieping**: Lerp, Distance, Magnitude, normalizen.
- **TextMeshPro & UI**: Score UI updaten via `TMP_Text`.
- **Coroutines**: Gebruik van coroutines voor timed behavior.

**M4 — GDV:**

- In M4 staan ook `BO` en `Skill` mappen, maar de belangrijkste programmeerinhoud is samengevat in `PROG`.

**M5 — Prog:**

- **Herhaling en verdieping**: Functions, Classes, Arrays, Lists.
- **Action & Events**: Events pattern en Unity event-driven voorbeelden.
- **Debugging**: Breakpoints, fouten opsporen en voorbeelden in `src`.
- **Design principes**: DRY, SRP, modulariteit, hergebruik van code.
- **OOP topics**: Inheritance, Encapsulation, Abstraction, Polymorphism.
- **Class diagrams & code conventions**: Visuele modellen (mermaid, diagrams) en style-guides.
- **Delegates & Interfaces**: Gebruik van delegates, events en interface patronen.
- **Memory & performance**: Stack vs Heap, garbage collection, read/write performance.
- **Design Patterns**: Factory Method en andere patroonvoorbeelden toegepast in voorbeelden.

**M5 — GDV / Tower Defense**

- Project-specifieke oefeningen voor Tower Defense (plaatsing torens, prefab gebruik, gameplay mechanics) aanwezig onder `Tower_defense_2D` en `Prog` voorbeelden.

**M6 — PROG:**

- **Code Conventions**: Best practices en style.
- **Class Diagrams**: Diagrammen voor ontwerp en planning.
- **Data structures**: Class, Struct & Enum; scriptable objects; wanneer welk type gebruiken.
- **Delegates**: Gebruik en voorbeelden.
- **OOP - Abstraction & Polymorphism**: Verdere verdieping in ontwerpprinicipes.
- **Performance**: Profiler gebruik, heavy workloads, I/O en effecten op `Debug.Log`, memory management en GC.

---

**Aanbevolen aanvullingen:**

- **Persistentie & opslag**: `PlayerPrefs`, file I/O, serialisatie (JSON/binary) en save-systeemontwerp.
- **Input Systemen**: verschil tussen legacy `Input` en de nieuwe `Input System`; toetsen, muis, touch en controllers.
- **Animatie**: Animator / Mecanim basics, animatieparameters, blend trees en transitions.
- **Audio**: `AudioSource`, `AudioMixer`, SFX vs. muziek, spatial audio basics en volume management.
- **AI & gedrag**: State machines, eenvoudige gedragslogica en pathfinding (NavMesh of A\*).
- **Gameplay Architectuur & Design Patterns**: Event-driven architectures, Singleton, Observer, Command toegepast in games.
- **Asset Management & optimalisatie**: texture compression, sprite atlases, draw calls, batching en memory footprints.
- **Performance & Profiling (praktijk)**: object pooling, reduce allocations, profiler workflows en concrete optimalisaties.
- **Builds & platforms**: player settings, platform-specifieke aandachtspunten (mobile vs. desktop) en build pipelines.

- **Editor scripting & tools**: custom inspectors, editor windows en utilities voor workflowverbetering.

- **Versiebeheer / Git**: branches, pull requests, code reviews en `.gitignore` — essentieel voor samenwerking.

- **CI/CD & automatisering**: automatische builds en korte intro tot pipelines (bijv. GitHub Actions).

- **Netwerken & multiplayer basics**: client/server-concepten, latency en opties zoals Unity Netcode (kort overzicht).

- **Testing & QA**: playtesting, unit tests voor C#, en test-driven mindset.

- **Security & netwerkveiligheid (hoog niveau)**: basistips voor online games (input validation, anti-cheat awareness).

- **Localization & accessibility**: string management, fonts en toegankelijkheidsoverwegingen.
