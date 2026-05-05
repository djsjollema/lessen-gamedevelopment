# Lessenpakket: 3d_Gym — Game Development voor Beginners

---

## Analyse van de 3d_Gym Scene

### Aanwezige assets & scripts

| Categorie | Inhoud |
|---|---|
| **Scenes** | `3d_Gym.unity`, `character_controller.unity`, `input_manager.unity` |
| **Scripts** | `MoveCharacterController.cs` (CharacterController + animator + sprong), `InputPlayer.cs` (Rigidbody + charged jump, oefeningen) |
| **Mixamo character** | `Worker_Idle_SKIN.fbx`, `Worker_walk.fbx`, `Worker_run.fbx`, `Worker_jump_up/down.fbx`, Animator Controller |
| **Props** | `double_open_end_wrench.FBX` met rotatie-animatie, Barrels, Boxes, Containers (prefabs) |
| **Materials** | URP-materialen, HDRI Skybox (`CasualDay`), gras, vloer, character |
| **Textures** | Diffuse, Normal Map, Specular, Glossiness, Occlusion van character & wrench |
| **Settings** | URP (PC + Mobile), Render Pipeline, Volume Profiles |
| **Packages** | Unity.AI.Navigation, Cinemachine 3, Input System, Timeline, Splines, Visual Scripting |
| **Explanations** | `SprongFormule.md` |

---

## Overzicht van technieken: bestaand + aanvullend

### ✅ Al verwerkt (of gepland) in de scene

1. Asset pack importeren, Package Manager, URP Render Pipeline Converter, Skybox
2. Input System (nieuw) — lopen, rennen, springen met Rigidbody
3. Mixamo modellen & animaties importeren, import settings, Animator Controller
4. Bewegen met `CharacterController.Move()`
5. Springen met de formule `verticalVelocity = Mathf.Sqrt(2f * Mathf.Abs(gravity) * jumpHeight)`
6. Items oppakken (wrench) + UI-update + particle effect + sound *(nog toe te voegen)*
7. Raycast — schieten of obstakels detecteren *(nog toe te voegen)*
8. Cinemachine 3 — pan & tilt camera

### 💡 Aanvullende technieken die goed aansluiten

| # | Techniek | Aansluiting op scene |
|---|---|---|
| 9 | **Physics verdieping** — drag, mass, PhysicsMaterial (friction/bounciness), AddForce, constraints | Barrels & Boxes die je opzij kunt duwen |
| 10 | **Tags & Layers + Physics Collision Matrix** | Speler botst niet met eigen bullets, collision filtering |
| 11 | **Particle System** | Pickup-effect wrench, stofwolkje bij landing, explosie barrel |
| 12 | **AudioSource & AudioMixer** — 3D spatial audio | Voetstappen, spronggeluid, wrench-pickup, achtergrondmuziek |
| 13 | **UI (uGUI)** — Canvas, TextMeshPro, health bar, score, inventory | Wrench-teller, health balk, sprint-indicator |
| 14 | **ScriptableObjects** — item-definities, speler-statistieken | Wrench-item data, enemy data |
| 15 | **NavMesh & AI Navigation** *(package al aanwezig!)* | NPC-collega die door de gym loopt en je volgt |
| 16 | **Coroutines** — timed events, invincibility frames | Knipperend effect na schade, respawn delay |
| 17 | **Scene Management** — scènewisseling, laadscherm, main menu | Start-menu, game-over scherm |
| 18 | **Post Processing / URP Volume** — bloom, vignette, color grading | Atmosferisch gymgevoel, hurt-effect |
| 19 | **Splines** *(package al aanwezig!)* — camera- of NPC-pad | NPC loopt via een spline-pad door de gym |
| 20 | **Timeline & Cutscenes** *(package al aanwezig!)* — intro-animatie | Openingsscène waarbij de camera inzoomt op het personage |
| 21 | **Texture Maps begrijpen** — Diffuse, Normal, Specular, Occlusion, Metallic | Character & wrench textures al aanwezig als voorbeeld |
| 22 | **ProBuilder / Level Prototyping** | Gym uitbreiden met eigen ruimtes en obstakels |

---
---

# Lesplannen

> **Structuur per les (2 uur)**
> - 🎓 **Instructie**: max 20 minuten
> - 🔨 **Mini-opdrachten**: 2–3 × max 10 minuten
> - 💬 **Peer feedback**: 5 minuten per mini-opdracht
> - ✅ **Feedback verwerken**: 5 minuten
> - 🏠 **Huiswerkopdracht**: 1 uur (in de klas)

---

## Les 1 — Project Setup: URP, Package Manager & Skybox

### Leerdoelen
- Je kunt een nieuw Unity URP-project aanmaken en een asset pack importeren
- Je kunt de Render Pipeline Converter gebruiken om materialen te converteren
- Je kunt een HDRI Skybox instellen via Lighting instellingen

### Instructie (20 min)
1. Nieuw project aanmaken: 3D (URP) template
2. Asset pack importeren via Asset Store / Package Manager (`.unitypackage`)
3. Render Pipeline Converter: `Window > Rendering > Render Pipeline Converter` — Built-in naar URP
4. Skybox instellen: `Window > Rendering > Lighting` → Environment → Skybox Material
5. HDRI Skybox met `CasualDay`-materiaal demonstreren
6. URP Renderer Assets tonen (PC vs. Mobile)

### 🔨 Mini-opdracht 1 (10 min)
Maak een nieuw project aan, importeer de meegeleverde asset pack en zorg dat alle materialen correct zijn (geen roze materialen). Plaats een lichtbron in de scene.

**💬 Peer feedback:** Controleer elkaars scene: zijn er nog roze materialen? Staat het licht goed?

**✅ Verwerken:** Ontbrekende conversies alsnog doorvoeren.

### 🔨 Mini-opdracht 2 (10 min)
Stel de HDRI Skybox in. Pas de `Exposure` en `Rotation` aan zodat de belichting past bij een sporthal-gevoel. Maak een screenshot van je resultaat.

**💬 Peer feedback:** Vergelijk de sfeer van elkaars scene. Geef één concreet verbeterpunt.

**✅ Verwerken:** Pas de belichting aan op basis van de feedback.

### 🏠 Huiswerkopdracht (1 uur)
Zoek een gratis asset pack op de Unity Asset Store (thema: sporthal, magazijn of buitenruimte). Importeer deze in het 3d_Gym project en bouw een kleine, eigen ruimte (minimaal 4 muren, een vloer, verlichting en decoratie). Zorg dat er geen materiaal-fouten zijn. Leg uit in een kort tekstje (5 zinnen) welke keuzes je hebt gemaakt.

---

## Les 2 — Input System (Nieuw): Rigidbody Beweging

### Leerdoelen
- Je snapt het verschil tussen het oude en nieuwe Input System
- Je kunt een `InputActionAsset` aanmaken met Action Maps en Bindings
- Je kunt input uitlezen met `ReadValue<Vector2>()`, `WasPressedThisFrame()` en `IsPressed()`
- Je kunt een Rigidbody bewegen en laten springen via scripts

### Instructie (20 min)
1. Verschil oud (`Input.GetKey`) vs. nieuw Input System
2. `InputActionAsset` aanmaken: `Action Map`, `Action`, `Binding`
3. In script: `FindActionMap()`, `FindAction()`, `Enable()` in `OnEnable`
4. `ReadValue<Vector2>()` voor assen, `WasPressedThisFrame()` voor knoppen
5. `Rigidbody.AddForce()` vs. `transform.Translate()`
6. Korte toelichting `InputPlayer.cs` in de scene

### 🔨 Mini-opdracht 1 (10 min)
Voeg de `"J"`-knop toe als extra binding voor de `Jump`-actie. Maak de actie werken zodat een blokje (met Rigidbody) omhoog springt.

**💬 Peer feedback:** Test elkaars project: werkt de J-toets? Geef aan of de sprong te krachtig of te zwak aanvoelt.

**✅ Verwerken:** Pas `jumpForce` aan op basis van de feedback.

### 🔨 Mini-opdracht 2 (10 min)
Zorg dat het blokje pas opnieuw kan springen nadat het de grond heeft geraakt (geen dubbele sprongen). Gebruik een `bool isGrounded` die je bijhoudt via `OnCollisionEnter` en `OnCollisionExit`.

**💬 Peer feedback:** Test of de double jump echt geblokkeerd is. Bespreek hoe jullie het detecteren van de grond hebben opgelost.

**✅ Verwerken:** Verbeter de gronddetectie als hij niet betrouwbaar is.

### 🔨 Mini-opdracht 3 (10 min)
Zorg dat het blokje in meerdere richtingen beweegt (links/rechts/voor/achter) met de `moveAction`. Voeg ook `"i"`, `"j"`, `"k"`, `"l"` toe als alternatieve bindings.

**💬 Peer feedback:** Speelt de beweging lekker? Is er verschil merkbaar in de controller-feel?

**✅ Verwerken:** Pas snelheid of bewegingsrichting aan.

### 🏠 Huiswerkopdracht (1 uur)
Bouw een **twee-speler mini-game**: twee blokjes op één scherm, elk met een eigen Action Map (Player1 / Player2). Beiden kunnen lopen en springen. Maak een simpele arena met obstakels (primitieven). Bonuspunt: de speler die van het platform valt verliest.

---

## Les 3 — Mixamo: Modellen, Animaties & Animator Controller

### Leerdoelen
- Je kunt een karakter en animaties downloaden van Mixamo en correct importeren in Unity
- Je begrijpt de belangrijkste import settings (Rig, Avatar, Loop Time)
- Je kunt een Animator Controller opzetten met states, parameters en transitions

### Instructie (20 min)
1. Mixamo.com: karakter kiezen, FBX for Unity exporteren
2. Import settings in Unity: `Rig` tab → Humanoid, `Avatar Definition`
3. `Animation` tab: animaties extracten, `Loop Time` aan/uit, `Root Motion` vs. in-place
4. Animator Controller aanmaken: states toevoegen, transitions, `Exit Time` uitleggen
5. Parameters: `Float`, `Bool`, `Trigger` — koppeling aan script
6. Bestaande `Worker_Idle.controller` tonen als voorbeeld

### 🔨 Mini-opdracht 1 (10 min)
Download een eigen karakter van Mixamo (niet de Worker). Importeer het correct in het project. Controleer of het Avatar groen is en geen errors geeft.

**💬 Peer feedback:** Controleer elkaars Avatar: is hij correct geconfigureerd? Zijn de bones goed gemapped?

**✅ Verwerken:** Corrigeer eventuele mapping-fouten.

### 🔨 Mini-opdracht 2 (10 min)
Maak een Animator Controller voor je karakter met minimaal drie states: Idle, Walk, Run. Stel een `Float`-parameter `Speed` in en maak transitions op basis van deze waarde.

**💬 Peer feedback:** Bekijk elkaars Animator graph. Zijn de transition-condities logisch? Zijn er blend-problemen?

**✅ Verwerken:** Pas transition thresholds aan waar nodig.

### 🔨 Mini-opdracht 3 (10 min)
Voeg een `Jump`-animatie toe met een `Trigger`-parameter. Zorg dat de transitie vanuit elke state kan springen (gebruik `Any State`).

**💬 Peer feedback:** Test de spronganimatie in Play mode. Gaat hij soepel over of zit er een harde knip?

**✅ Verwerken:** Pas `Transition Duration` en `Exit Time` aan voor een vloeiende overgang.

### 🏠 Huiswerkopdracht (1 uur)
Bouw een volledig Animator Controller met: Idle, Walk, Run, Jump (up + down), Land. Gebruik Blend Trees voor Walk/Run zodat de snelheid de animatie bepaalt. Voeg het toe aan het Worker-prefab en zorg dat `MoveCharacterController.cs` de animator correct aanstuurt. Test alle transitions in Play mode en leg in een korte notitie (5 zinnen) uit welke animator-instellingen je hebt gebruikt en waarom.

---

## Les 4 — CharacterController: Bewegen & Springen

### Leerdoelen
- Je begrijpt het verschil tussen `CharacterController` en `Rigidbody` beweging
- Je kunt `CharacterController.Move()` correct gebruiken
- Je kunt de sprong-formule uitleggen en toepassen

### Instructie (20 min)
1. Waarom CharacterController? Vergelijk met Rigidbody (controle vs. physics)
2. `CharacterController.Move(Vector3)` — werkt met deltabewegingen, niet op positie
3. `isGrounded` gebruiken voor gronddetectie
4. Zwaartekracht handmatig implementeren: `verticalVelocity += gravity * Time.deltaTime`
5. De sprong-formule: `v = √(2 × |g| × h)` — afgeleid van kinematische vergelijking
6. `MoveCharacterController.cs` doorlopen: sprint, rotatie, animator-koppeling

### 🔨 Mini-opdracht 1 (10 min)
Pas `gravity` en `jumpHeight` aan zodat het springen voelt als een **langzame maansprong** (lage gravity, hoge jump). Noteer de waarden. Daarna: maak het zwaar en snel als **aardse sprong**.

**💬 Peer feedback:** Speel elkaars versie. Welke feel is het best? Welke waarden werken het beste voor een game?

**✅ Verwerken:** Stel de waarden in die jullie als best voelden.

### 🔨 Mini-opdracht 2 (10 min)
Voeg een **sprint-indicator** toe: als de speler sprint, kleur dan een `Image` in de UI rood. Stop de sprint als de speler een `staminaTimer` heeft opgebruikt (bijv. 3 seconden).

**💬 Peer feedback:** Is de stamina-mechaniek begrijpelijk zonder uitleg? Is de timer logisch?

**✅ Verwerken:** Pas de timer-duur of het visuele feedback-element aan.

### 🔨 Mini-opdracht 3 (10 min)
Voeg een **coyote time** toe: de speler mag nog 0.15 seconden na het aflopen van een platform springen (zonder te vliegen). Gebruik een `float coyoteTimer`.

**💬 Peer feedback:** Merk je het verschil met en zonder coyote time? Voelt het eerlijker?

**✅ Verwerken:** Pas de coyote-tijd aan tot het goed voelt.

### 🏠 Huiswerkopdracht (1 uur)
Bouw een **obstacle course** in de 3d_Gym scene: minimaal 5 platforms op verschillende hoogtes, een platform dat beweegt (met een script of via een Animator), en een smal pad. De speler moet van start naar finish kunnen lopen en springen. Zorg voor duidelijk visuele feedback (start- en eindzone). Documenteer welke `gravity`- en `jumpHeight`-waarden je hebt gekozen en waarom.

---

## Les 5 — Raycast: Items Oppakken & Interactie

### Leerdoelen
- Je begrijpt hoe een `Raycast` werkt (richting, afstand, `RaycastHit`)
- Je kunt een item detecteren met Raycast en oppakken
- Je kunt een UI-element updaten als reactie op een game-event
- Je kunt een `ParticleSystem` en `AudioSource` activeren via script

### Instructie (20 min)
1. Raycast basis: `Physics.Raycast(origin, direction, out hit, distance)`
2. `Debug.DrawRay()` voor visuele debugging
3. Vergelijking met trigger/collider: wanneer gebruik je wat?
4. Tags gebruiken om objecten te herkennen (`hit.collider.CompareTag("Pickup")`)
5. UI updaten: `TextMeshProUGUI`, `Image.fillAmount`
6. `ParticleSystem.Play()` en `AudioSource.PlayOneShot()` aanroepen

### 🔨 Mini-opdracht 1 (10 min)
Voeg een Raycast toe aan de speler die recht naar voren schiet. Gebruik `Debug.DrawRay()` om hem zichtbaar te maken in de Scene view. Zorg dat in de Console wordt geprint welk object geraakt wordt.

**💬 Peer feedback:** Is de ray goed gepositioneerd? Raakt hij objecten die hij niet zou moeten raken?

**✅ Verwerken:** Pas de origin (oogpositie) of richting aan.

### 🔨 Mini-opdracht 2 (10 min)
Voeg een Tag `"Pickup"` toe aan de wrench. Als de Raycast de wrench raakt EN de speler op interactie-knop drukt (bijv. `"E"`), verdwijnt de wrench en wordt een UI-teller met `+1` bijgewerkt.

**💬 Peer feedback:** Werkt de interactie soepel? Is de pickup-afstand logisch (niet te groot, niet te klein)?

**✅ Verwerken:** Pas de max-afstand van de Raycast aan.

### 🔨 Mini-opdracht 3 (10 min)
Koppel een `ParticleSystem` (gebruik een bestaand Unity effect of maak een simpele burst) aan de pickup. Laat het effect afspelen op de positie van de wrench bij oppakken.

**💬 Peer feedback:** Ziet het effect er bevredigend uit? Is het op de juiste positie?

**✅ Verwerken:** Pas de grootte, kleur of duur van het effect aan.

### 🏠 Huiswerkopdracht (1 uur)
Bouw een **collectibles-systeem**: plaats 5 wrenches in de gym op verschillende locaties. Maak een UI-balk die bijhoudt hoeveel je hebt verzameld (bijv. "3/5"). Als alle 5 zijn opgepakt, speelt een geluid en verschijnt een "Completed!"-tekst in beeld. Bonus: voeg een timer toe die aftelt — als de tijd op is, verlies je.

---

## Les 6 — Raycast: Schieten & Obstakels Detecteren

### Leerdoelen
- Je kunt een raycast-gebaseerd shoot-systeem bouwen
- Je begrijpt Layer Masks voor gefilterde raycasts
- Je kunt visuele feedback geven via `LineRenderer` of `TrailRenderer`

### Instructie (20 min)
1. Raycast voor schieten: richting vanuit camera of speler
2. `LayerMask` gebruiken: `Physics.Raycast(origin, dir, out hit, dist, layerMask)`
3. Schade toepassen op geraakt object via een interface (`IDamageable`)
4. `LineRenderer` voor laserstraal of `Instantiate()` voor bullet
5. Object kapot laten gaan: `Destroy(hit.collider.gameObject)`
6. Raycast voor obstakels: "kan ik de deur zien?" → NPC line-of-sight preview

### 🔨 Mini-opdracht 1 (10 min)
Voeg een schiet-actie toe aan de Input Asset. Bij het drukken op de schiet-knop wordt een Raycast geschoten vanuit de camera-richting. Toon een `Debug.DrawRay()` en print het geraakt object.

**💬 Peer feedback:** Schiet de ray in de juiste richting? Test met meerdere objecten.

**✅ Verwerken:** Corrigeer eventuele richting- of originfouten.

### 🔨 Mini-opdracht 2 (10 min)
Voeg een `LineRenderer` toe die gedurende 0.1 seconde de kogelbaan toont (gebruik een `Coroutine` voor de fade). Kleur de lijn rood.

**💬 Peer feedback:** Is de lijn zichtbaar en duidelijk? Verdwijnt hij snel genoeg?

**✅ Verwerken:** Pas de fade-tijd of kleur aan.

### 🔨 Mini-opdracht 3 (10 min)
Maak een `Barrel` prefab met een `int health = 3`. Elke Raycast-hit trekt 1 health af. Bij 0 health: `Destroy()` de barrel en spawn een particle effect op die positie.

**💬 Peer feedback:** Is het duidelijk dat de barrel schade ontvangt? Mis je visuele feedback bij elke hit?

**✅ Verwerken:** Voeg een kleur-flash toe bij schade (verander `Material.color` kort).

### 🏠 Huiswerkopdracht (1 uur)
Bouw een **shooting range**: een rij van 5 targets (planken of cylinders) op afstand. De speler schiet met Raycast. Elk target heeft HP. Bij dood: spawn confetti-particles en update een score-UI. Na 30 seconden reset alles en toon de score. Gebruik Layer Masks zodat de speler zichzelf niet kan raken.

---

## Les 7 — Cinemachine 3: Camera Systemen (Pan & Tilt)

### Leerdoelen
- Je kunt een Cinemachine Virtual Camera instellen met een Follow-target
- Je begrijpt het verschil tussen pan (horizontaal) en tilt (verticaal) camerabesturing
- Je kunt de Cinemachine Input Handler koppelen aan het nieuwe Input System

### Instructie (20 min)
1. Cinemachine installeren via Package Manager, `CinemachineCamera` component
2. `Follow` en `LookAt` target instellen (CameraFollowTarget op de speler)
3. `CinemachineOrbitalFollow` vs. `CinemachinePositionComposer`
4. Input System koppelen: `CinemachineInputAxisController`
5. `Recentering` inschakelen: camera keert terug als speler niet beweegt
6. Camera collision met `CinemachineCameraOffset` en `CinemachineDeoccluder`

### 🔨 Mini-opdracht 1 (10 min)
Maak een Virtual Camera die de Worker-speler volgt. Stel `Follow` en `LookAt` in op de Worker. Pas de `Camera Distance` en `Field of View` aan.

**💬 Peer feedback:** Volgt de camera soepel? Is de afstand aangenaam?

**✅ Verwerken:** Pas `Damping` waarden aan voor soepelere beweging.

### 🔨 Mini-opdracht 2 (10 min)
Voeg pan & tilt-input toe via de muis (of joystick). Zorg dat de speler kan rondkijken en dat de camera vertica beperkt is (tilt max ±60 graden).

**💬 Peer feedback:** Voelt de camerarotatie prettig aan? Is de muisgevoeligheid goed?

**✅ Verwerken:** Pas de `Axis Value Range` en `Input Gain` aan.

### 🔨 Mini-opdracht 3 (10 min)
Maak een tweede Virtual Camera: een `Overview Camera` die boven de scene hangt (bovenaanzicht). Gebruik een `CinemachineBrain` priority-switch zodat je met een knop kunt wisselen tussen de twee camera's.

**💬 Peer feedback:** Gaat de overgang soepel? Is het duidelijk wanneer je van camera wisselt?

**✅ Verwerken:** Voeg een `Blend Time` toe voor een vloeiende overgang.

### 🏠 Huiswerkopdracht (1 uur)
Ontwerp een **cutscene-intro** met Cinemachine: als de scene start, beweegt een camera langs minimaal 3 waypoints door de gym (gebruik `CinemachinePath` of `Spline`). Na 5 seconden schakelt de camera over naar de speler-followcam. Gebruik `Timeline` of `Coroutines` voor de timing. Zorg voor een smooth blend.

---

## Les 8 — NavMesh & NPC Navigatie

### Leerdoelen
- Je kunt een NavMesh bakken voor een scene
- Je kunt een NPC laten navigeren met `NavMeshAgent`
- Je kunt een simpele patrol- en follow-AI bouwen

### Instructie (20 min)
1. `AI Navigation`-package (al aanwezig): `NavMeshSurface` bakken
2. `NavMeshAgent` component: `speed`, `angularSpeed`, `stoppingDistance`
3. `agent.SetDestination(Vector3)` gebruiken in script
4. Patrol-loop: array van waypoints, automatisch naar volgend punt
5. Follow-AI: `agent.SetDestination(player.position)` in `Update`
6. NavMesh Obstacle voor dynamische obstakels (barrel die je wegschopt)

### 🔨 Mini-opdracht 1 (10 min)
Bak een NavMesh over de 3d_Gym scene. Voeg een `NavMeshAgent` toe aan een NPC (gebruik een simpele capsule of het Worker-model). Laat de NPC naar een vaste positie navigeren.

**💬 Peer feedback:** Navigeert de NPC correct? Loopt hij niet door muren of objecten?

**✅ Verwerken:** Voeg `NavMeshObstacle` toe aan grote meubels die niet in de mesh zijn opgenomen.

### 🔨 Mini-opdracht 2 (10 min)
Bouw een patrol-systeem: de NPC loopt langs 3–4 waypoints in een lus. Gebruik een `Transform[]`-array en een index die bijhoudt waar de NPC naartoe gaat.

**💬 Peer feedback:** Is de patrol logisch gepositioneerd? Stopt de NPC correct bij elk waypoint?

**✅ Verwerken:** Pas `stoppingDistance` aan en voeg een wachttijd toe bij elk punt (Coroutine).

### 🔨 Mini-opdracht 3 (10 min)
Voeg line-of-sight toe: als de NPC de speler *ziet* (Raycast raakt speler, geen obstakel ertussen), wisselt hij van patrol naar follow-modus.

**💬 Peer feedback:** Is de overgang van patrol naar follow duidelijk? Reageert de NPC te snel of te langzaam?

**✅ Verwerken:** Voeg een detectie-range toe (`Vector3.Distance`) als extra conditie.

### 🏠 Huiswerkopdracht (1 uur)
Bouw een **bewaker-systeem**: een NPC patrouilleert door de gym. Als de speler te dichtbij komt (en de NPC heeft line-of-sight), gaat de NPC naar de speler. Als de speler wegrent en buiten de detectie-range is voor 3 seconden, keert de NPC terug naar de patrol. Gebruik een state machine met minimaal 3 states: `Patrol`, `Chase`, `Return`. Toon de huidige state in een UI-label boven de NPC.

---

## Les 9 — Particle Systems & Audio

### Leerdoelen
- Je kunt een Particle System aanmaken en instellen (emission, shape, lifetime, color over lifetime)
- Je kunt een `AudioSource` gebruiken voor 3D ruimtelijk geluid
- Je kunt particles en audio koppelen aan game-events via script

### Instructie (20 min)
1. Particle System aanmaken: `Emission`, `Shape`, `Start Lifetime/Speed/Size`
2. `Color over Lifetime`, `Size over Lifetime` voor visuele polish
3. `Sub Emitters` voor complexere effecten (bijv. vonken bij explosie)
4. `AudioSource`: `PlayOneShot()` vs. `Play()`, `spatialBlend` voor 3D-geluid
5. `AudioMixer`: volume-groepen, master/music/SFX-kanalen
6. Koppeling: `OnCollisionEnter` → particles + audio tegelijk starten

### 🔨 Mini-opdracht 1 (10 min)
Maak een stofwolkje particle effect voor wanneer de speler landt na een sprong. Activeer het via `animator`-events of via de `isGrounded`-check in het movement-script.

**💬 Peer feedback:** Is het effect op de juiste positie (voeten, niet hoofd)? Is de grootte passend?

**✅ Verwerken:** Pas de `Start Size` en `Simulation Space` aan.

### 🔨 Mini-opdracht 2 (10 min)
Voeg een 3D `AudioSource` toe aan een barrel. Als de speler er tegenaan botst (`OnCollisionEnter`, alleen als de kracht groot genoeg is), speelt een klap-geluid. Pas `spatialBlend` in op 1 (volledig 3D).

**💬 Peer feedback:** Hoor je het verschil in volume als je dichterbij of verder weg staat? Is de drempelwaarde voor het geluid goed?

**✅ Verwerken:** Pas `Rolloff` curve aan voor realistischer afstandsgeluid.

### 🔨 Mini-opdracht 3 (10 min)
Maak een `AudioMixer` met drie groepen: `Master`, `Music`, `SFX`. Koppel de achtergrondmuziek aan `Music` en het landing-effect aan `SFX`. Voeg twee sliders toe aan de UI om het volume per kanaal te regelen.

**💬 Peer feedback:** Werken de volume-sliders correct? Is de standaardbalans tussen muziek en SFX goed?

**✅ Verwerken:** Pas de standaard dB-waarden aan.

### 🏠 Huiswerkopdracht (1 uur)
Bouw een **interactieve geluidsruimte** in de gym: minimaal 4 objecten met elk een eigen Particle System en AudioSource. Voorbeelden: een barrel die ontploft bij schieten, een ventilator die ronddraait met lopend geluid, een neon-lamp die flikkert met knetter-geluid. Gebruik de `AudioMixer` voor volume-balans. Elke interactie geeft zowel visuele als auditieve feedback.

---

## Les 10 — UI Systeem: Canvas, Health Bar & Inventory

### Leerdoelen
- Je kunt een Canvas opzetten met de juiste Render Mode
- Je kunt een `TextMeshProUGUI` aanpassen via script
- Je kunt een health bar bouwen met `Image.fillAmount`
- Je kunt een inventory-grid bouwen met een simpele `List<>`

### Instructie (20 min)
1. Canvas: `Screen Space — Overlay` vs. `World Space` vs. `Camera`
2. `TextMeshProUGUI`: tekst updaten, kleur wisselen
3. `Image.fillAmount` voor een health/stamina-balk (0.0 – 1.0)
4. `RectTransform.anchoredPosition` voor UI-layout
5. Inventory basis: `List<string>` of `List<ScriptableObject>` bijhouden
6. `Instantiate()` voor inventory-slots in een Grid Layout Group

### 🔨 Mini-opdracht 1 (10 min)
Maak een health bar die afneemt als je op `"H"` drukt (simuleer schade). Gebruik `Image.fillAmount`. De balk kleurt van groen → geel → rood naarmate de health afneemt.

**💬 Peer feedback:** Is de kleurovergang duidelijk? Is de balk goed leesbaar op de achtergrond?

**✅ Verwerken:** Pas de kleurdrempels of balk-grootte aan.

### 🔨 Mini-opdracht 2 (10 min)
Toon de naam van het laatste opgepakte item in de UI. Als je 3 wrenches hebt opgepakt, toon dan "Wrench ×3". Update de tekst bij elke pickup.

**💬 Peer feedback:** Is de tekst altijd correct gesynchroniseerd met de game-state?

**✅ Verwerken:** Zorg dat de teller nooit negatief kan worden of te groot kan groeien.

### 🔨 Mini-opdracht 3 (10 min)
Bouw een inventory-grid van 4 vakjes (gebruik `Grid Layout Group`). Als je een item oppakt, verschijnt het icoontje in het eerste lege vakje. Gebruik een `List<Image>` om de slots bij te houden.

**💬 Peer feedback:** Is de grid-layout duidelijk? Zijn de icoontjes leesbaar?

**✅ Verwerken:** Voeg een hover-tooltip toe die de item-naam toont.

### 🏠 Huiswerkopdracht (1 uur)
Bouw een volledig **HUD**: health bar, stamina bar, item-teller (wrenches), mini-timer en een `"Press E to pick up"`-prompt die alleen zichtbaar is als de speler dicht bij een item staat (Raycast-gebaseerd). Alle UI-elementen moeten correct schalen op verschillende resoluties (gebruik `Canvas Scaler` met `Scale With Screen Size`).

---

## Les 11 — ScriptableObjects: Data-gedreven Design

### Leerdoelen
- Je begrijpt waarom ScriptableObjects handig zijn voor game data
- Je kunt een ScriptableObject aanmaken voor item-definities
- Je kunt een ScriptableObject gebruiken als data-bron in andere scripts

### Instructie (20 min)
1. Probleem zonder SO: hardcoded waarden in prefabs vs. data-driven
2. `[CreateAssetMenu]` attribute, aanmaken via Project window
3. SO als item-definitie: naam, icoontje, waarde, geluid, effect
4. Referentie in MonoBehaviour: `[SerializeField] private ItemData itemData;`
5. SO als event-systeem: `UnityEvent` in een SO (optioneel)
6. Voorbeeld: `ItemData.cs` voor de wrench

### 🔨 Mini-opdracht 1 (10 min)
Maak een `ItemData` ScriptableObject met: `itemName`, `itemIcon (Sprite)`, `pickupSound (AudioClip)` en `pointValue (int)`. Maak een SO-asset voor de wrench.

**💬 Peer feedback:** Zijn de velden logisch gekozen? Ontbreken er eigenschappen?

**✅ Verwerken:** Voeg een ontbrekend veld toe op basis van de feedback.

### 🔨 Mini-opdracht 2 (10 min)
Pas het pickup-script aan zodat het de `ItemData` uitleest voor de naam in de UI en het geluid bij oppakken. Verwijder alle hardcoded waarden.

**💬 Peer feedback:** Werkt de koppeling correct? Kan je eenvoudig een nieuw item toevoegen zonder code te wijzigen?

**✅ Verwerken:** Voeg een tweede item-type toe (bijv. een helm) alleen via een nieuwe SO-asset.

### 🔨 Mini-opdracht 3 (10 min)
Maak een `PlayerStatsSO` met: `maxHealth`, `moveSpeed`, `jumpHeight`. Laat `MoveCharacterController.cs` de waarden uitlezen uit dit SO in plaats van via `SerializeField`.

**💬 Peer feedback:** Is het makkelijker om speler-stats aan te passen nu ze in een SO staan?

**✅ Verwerken:** Bespreek: wanneer gebruik je een SO en wanneer niet?

### 🏠 Huiswerkopdracht (1 uur)
Ontwerp een **loot-systeem**: maak 5 verschillende `ItemData` SOs (gereedschap, veiligheidsuitrusting, enz.). Bouw een `LootTable` SO die een weighted lijst van items bijhoudt. Bij het raken van een barrel spawnt er een random item op basis van de loot table (gebruik `Random.value`). Toon het gevonden item 2 seconden in de UI en voeg het toe aan de inventory.

---

## Les 12 — Scene Management & Coroutines

### Leerdoelen
- Je kunt van scene wisselen met `SceneManager.LoadScene()`
- Je kunt een laadscherm bouwen met een `AsyncOperation`
- Je kunt `Coroutines` gebruiken voor tijdgebonden logica

### Instructie (20 min)
1. `using UnityEngine.SceneManagement;`
2. `SceneManager.LoadScene()` — direct vs. `LoadSceneAsync()`
3. `AsyncOperation.progress` voor een laadbalkie
4. `DontDestroyOnLoad()` voor persistente objecten (GameManager, AudioManager)
5. Coroutine basis: `IEnumerator`, `yield return new WaitForSeconds()`, `StartCoroutine()`
6. Gebruik: invincibility frames, respawn-delay, knipperende UI

### 🔨 Mini-opdracht 1 (10 min)
Maak een `MainMenu`-scene met een Start-knop. Bij klikken laadt de 3d_Gym scene. Voeg een `Quit`-knop toe. Zorg dat de knop-sounds correct spelen (gebruik `AudioSource.PlayOneShot()`).

**💬 Peer feedback:** Werkt de knoppenlogica? Is het menu visueel duidelijk?

**✅ Verwerken:** Voeg een hover-animatie toe aan de knoppen (via `Animator` of `EventTrigger`).

### 🔨 Mini-opdracht 2 (10 min)
Maak een `Coroutine` die de speler 2 seconden onkwetsbaar maakt na het ontvangen van schade (invincibility frames). Zorg dat de speler knippert (enable/disable `MeshRenderer` elke 0.1 seconden) tijdens de invincibility.

**💬 Peer feedback:** Is het visueel duidelijk wanneer de speler onkwetsbaar is?

**✅ Verwerken:** Pas de duur of knippersnelheid aan.

### 🔨 Mini-opdracht 3 (10 min)
Bouw een `GameOver`-scherm: als de health 0 bereikt, wacht 2 seconden (Coroutine), laad dan de GameOver-scene. De GameOver-scene toont de score en een restart-knop.

**💬 Peer feedback:** Is de 2-seconden delay logisch? Gaat de score correct mee naar de GameOver-scene?

**✅ Verwerken:** Gebruik `DontDestroyOnLoad()` of `static` variabelen voor de score.

### 🏠 Huiswerkopdracht (1 uur)
Bouw een complete **game-loop**: MainMenu → 3d_Gym → GameOver → terug naar MainMenu. Gebruik een `GameManager` singleton (met `DontDestroyOnLoad`) die score, timer en levens bijhoudt. Voeg een afteltimer toe in de gym: als de tijd op is, trigger de GameOver. Toon op het GameOver-scherm: eindscore, verstreken tijd en een highscore (bewaard via `PlayerPrefs`).

---

## Les 13 — Post Processing & Verlichting

### Leerdoelen
- Je kunt een URP Volume instellen met post-processing effecten
- Je begrijpt het verschil tussen baked en realtime verlichting
- Je kunt een `Global Volume` en `Local Volume` gebruiken

### Instructie (20 min)
1. `Volume` component: `Global Volume` vs. `Local Volume` (trigger)
2. Effecten: `Bloom`, `Vignette`, `Color Grading`, `Depth of Field`
3. `Override` activeren per effect, profielen aanmaken
4. Baked vs. Realtime verlichting: performance uitleg
5. `Light Probes` voor dynamische objecten in gebakken licht
6. Hurt-effect met Local Volume: rood vignette bij schade via script

### 🔨 Mini-opdracht 1 (10 min)
Voeg een `Global Volume` toe aan de 3d_Gym scene. Activeer `Bloom` en `Color Grading`. Geef de scene een koele, industriële sfeer (lage saturatie, blauw-grijs tint).

**💬 Peer feedback:** Past de sfeer bij een sporthal/werkplaats? Is het effect te sterk of te subtiel?

**✅ Verwerken:** Pas `Intensity` en `Threshold` aan.

### 🔨 Mini-opdracht 2 (10 min)
Maak een `Local Volume` (Box Collider) in een hoek van de gym. Als de speler in die zone loopt, wordt het beeld waziger (`Depth of Field`) als mysterieus effect. Pas de trigger aan via de Volume's blending.

**💬 Peer feedback:** Werkt de overgang soepel? Is het duidelijk dat je in een speciale zone bent?

**✅ Verwerken:** Voeg een particle effect toe als hint dat er iets bijzonders is.

### 🔨 Mini-opdracht 3 (10 min)
Maak een hurt-effect: als de speler schade ontvangt, wordt het `Vignette`-effect in een Global Volume kort versterkt (rood, intense vignette). Gebruik een `Coroutine` om het effect na 0.5 seconden te laten vervagen.

**💬 Peer feedback:** Is het hurt-effect duidelijk zonder vervelend te zijn?

**✅ Verwerken:** Pas de kleur, intensity en fade-tijd aan.

### 🏠 Huiswerkopdracht (1 uur)
Optimaliseer de verlichting van de 3d_Gym scene: bak de statische verlichting met `Baked Global Illumination`. Voeg `Light Probes` toe voor de bewegende Worker. Maak dag/nacht-zones met Local Volumes. Documenteer het verschil in framerate (FPS) voor en na baking. Stel de `Directional Light` in op dynamisch voor schaduwkwaliteit.

---

## Les 14 — Physics Verdieping: Rigidbody, Forces & Materials

### Leerdoelen
- Je begrijpt `AddForce`, `AddTorque` en force modes
- Je kunt een `PhysicsMaterial` instellen voor stuiteren en wrijving
- Je kunt Rigidbody constraints gebruiken voor gecontroleerde beweging

### Instructie (20 min)
1. `AddForce(Vector3, ForceMode)`: `Force`, `Impulse`, `VelocityChange`, `Acceleration`
2. `AddTorque()` voor roterende objecten
3. `drag` en `angularDrag`: luchtweerstand simuleren
4. `PhysicsMaterial`: `staticFriction`, `dynamicFriction`, `bounciness`
5. `Rigidbody.constraints`: `FreezePositionY`, `FreezeRotation`
6. Voorbeeld: barrel die je wegschopt vs. een zware kist die nauwelijks beweegt

### 🔨 Mini-opdracht 1 (10 min)
Maak twee barrels: één licht (mass = 1) en één zwaar (mass = 20). Geef ze dezelfde `AddForce` via een script als de speler erop botst. Observeer het verschil.

**💬 Peer feedback:** Is het gewichtsverschil goed voelbaar? Klopt het met je gevoel voor realisme?

**✅ Verwerken:** Pas de masses aan voor een bevredigende feel.

### 🔨 Mini-opdracht 2 (10 min)
Maak een stuiterend object: een bal met een `PhysicsMaterial` met `bounciness = 0.8`. Gooi hem omhoog via `AddForce(Vector3.up, ForceMode.Impulse)`. Pas het materiaal aan zodat hij hoog stuiteert maar tot stilstand komt.

**💬 Peer feedback:** Stuitert de bal realistisch? Hoe lang duurt het voor hij stopt?

**✅ Verwerken:** Pas `drag` aan naast het materiaal.

### 🔨 Mini-opdracht 3 (10 min)
Maak een **kanon** dat een bal afvuurt richting de speler (of een doelobject) via `AddForce`. Gebruik `ForceMode.VelocityChange` voor een direct schot. De kracht is instelbaar via een `SerializeField`.

**💬 Peer feedback:** Raakt het kanon zijn doel? Is de kracht goed ingesteld?

**✅ Verwerken:** Voeg een `launch angle` toe zodat de baan boogvormig is.

### 🏠 Huiswerkopdracht (1 uur)
Bouw een **physics-puzzelkamer**: de speler moet minimaal 3 objecten (kist, barrel, platform) op de juiste manier manipuleren om een deur te openen of een pad te creëren. Gebruik `AddForce`, `PhysicsMaterial` en `Rigidbody.constraints` bewust. Elke physics-keuze (massa, wrijving, bounciness) moet onderbouwd zijn in een korte technische notitie (5 zinnen).

---

## Les 15 — Splines & Timeline: Geprogrammeerde Camera & Cutscenes

### Leerdoelen
- Je kunt een Spline-pad aanmaken en een NPC of camera erlangs laten bewegen
- Je kunt een basis Timeline-cutscene opzetten
- Je begrijpt hoe je Timeline koppelt aan Cinemachine voor camera-overgangen

### Instructie (20 min)
1. `Unity.Splines`: `SplineContainer`, `SplineAnimate` component
2. Knots aanpassen in de Scene view
3. `SplineAnimate.Duration` en `Loop Mode` instellen
4. `Timeline` window: tracks toevoegen, clips plaatsen
5. `Cinemachine Track` in Timeline voor camera-switch
6. `Activation Track` om objecten in/uit te schakelen per moment

### 🔨 Mini-opdracht 1 (10 min)
Maak een spline-pad langs de gym en laat een lege `GameObject` (als placeholder NPC) dit pad volgen met `SplineAnimate`. Pas de snelheid aan.

**💬 Peer feedback:** Volgt het object het pad soepel? Zijn er scherpe hoeken?

**✅ Verwerken:** Pas de Spline Tangent-modus aan (Bezier) voor vloeiende curves.

### 🔨 Mini-opdracht 2 (10 min)
Maak een Timeline-cutscene: Camera vliegt vanuit een startpositie naar de Worker-speler toe (gebruik twee Virtual Cameras en een `Cinemachine Track`). De cutscene duurt 4 seconden.

**💬 Peer feedback:** Gaat de camera-overgang soepel? Voelt de snelheid goed?

**✅ Verwerken:** Pas de blend curve aan in de Timeline.

### 🔨 Mini-opdracht 3 (10 min)
Koppel de `SplineAnimate`-NPC aan de Timeline: de NPC begint pas te lopen na 2 seconden (gebruik een `Animation Track` of `Activation Track`). De cutscene eindigt met de speler-camera.

**💬 Peer feedback:** Is de timing logisch? Voelt het als een echte intro-cutscene?

**✅ Verwerken:** Voeg een fade-in effect toe aan het begin van de Timeline.

### 🏠 Huiswerkopdracht (1 uur)
Bouw een **volledige intro-cutscene** (min. 8 seconden) voor de 3d_Gym: de camera vliegt via een Spline de gym in, een NPC loopt via een eigen Spline-pad naar een werkplek, en na de cutscene neemt de speler de controle over. Gebruik Timeline met minimaal: een Cinemachine Track, een Animation Track voor de NPC, en een Activation Track voor de UI (UI wordt pas zichtbaar na de cutscene). Exporteer een screen-recording van de cutscene.

---

*Document gegenereerd als onderdeel van het 3d_Gym lessenpakket voor startende game development studenten.*
