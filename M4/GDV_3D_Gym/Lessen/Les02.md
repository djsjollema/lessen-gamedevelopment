# M4 GDV HNR LES 2: Input System & Rigidbody Beweging

Deze les leren jullie het volgende:

- Je snapt het verschil tussen het oude en nieuwe Input System
- Je kunt een `InputActionAsset` aanmaken of aanpassen met Action Maps en Bindings
- Je kunt input uitlezen via een C# script
- Je kunt een Rigidbody-object laten bewegen en springen via het nieuwe Input System
- Je kunt twee spelers aansturen via aparte Action Maps in één `InputActionAsset`

In deze les laat de docent live zien hoe je het nieuwe Input System instelt en een speelbaar blokje maakt. Je kunt meekijken en aantekeningen maken, of direct meedoen.

De uitgebreide stap-voor-stap instructie staat hier: [Les02_StepByStep.md](../Uitleg/stepbystep/Les02_InputSystem_Rigidbody.md)

---

## Oud vs. nieuw Input System

Unity heeft twee manieren om toetsenbord- en controllerinput te verwerken:

| Oud systeem                   | Nieuw systeem                                   |
| ----------------------------- | ----------------------------------------------- |
| `Input.GetKey(KeyCode.Space)` | `jumpAction.WasPressedThisFrame()`              |
| Hardcoded aan toetsenbord     | Configureerbaar: toetsenbord, controller, touch |
| Geen hergebruik mogelijk      | Action Maps per context (gameplay, UI, menu)    |
| Polling per frame             | Event-driven of polling mogelijk                |

Het nieuwe Input System werkt met een **InputActionAsset**: een apart bestand dat alle inputs definieert, los van de code. Zo kun je inputs eenvoudig aanpassen zonder scripts te wijzigen.

---

## Demo 1 — InputActionAsset bekijken (~10 min)

De docent laat zien:

- Hoe je het `InputSystem_Actions.inputactions`-bestand opent
- Wat een **Action Map** is (bijv. "Player")
- Wat een **Action** is (bijv. "Move", "Jump")
- Wat **Bindings** zijn (bijv. WASD, Spatie, Gamepad)

> Open het bestand via de **Project** view → dubbelklik op `InputSystem_Actions.inputactions`

---

## Demo 2 — Twee Action Maps aanmaken (~15 min)

De docent maakt live twee Action Maps aan voor twee spelers:

**Player1** — Actions:

- `Move` (Vector2, WASD)
- `Jump` (Button, Left Ctr)
- `Sprint` (Button, Left Shift)

**Player2** — Actions:

- `Move` (Vector2, Arrows)
- `Jump` (Button, Right Ctr)
- `Sprint` (Button, Right Shift)

> Sla het bestand op na elke wijziging via **Save Asset** (rechtsboven).

---

## Demo 3 — Cubes Toevoegen (~5 min)

De docent voegt 2 **Cubes** toe als spelers (`Player1` en `Player2`), elk met een **Rigidbody**

- Constraints: **Freeze Rotation X en Z**

> Geef de blokjes een ander materiaal zodat je ze kunt onderscheiden.

---

## Demo 4 — Script schrijven: InputPlayer.cs (~20 min)

De docent schrijft live het script `InputPlayer.cs`:

**Belangrijkste onderdelen:**

```csharp
InputActionMap map = input.FindActionMap(mapName);
moveAction  = map.FindAction("Move");
jumpAction  = map.FindAction("Jump");
```

```csharp
Vector2 moveInput = moveAction.ReadValue<Vector2>();
Vector3 movement = new Vector3(moveInput.x, 0f, moveInput.y) * moveSpeed * Time.deltaTime;
transform.Translate(movement, Space.World);
```

```csharp
if (jumpAction.WasPressedThisFrame() && isGrounded)
{
    rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
}
```

Het script krijgt een `[SerializeField] string mapName` zodat je per blokje kunt instellen welke Action Map gebruikt wordt (`Player1` of `Player2`).

---

## Oefening — Koppelen en testen (~10 min)

Koppel het script aan beide blokjes in de Hierarchy:

1. Voeg `InputPlayer` toe aan **Player1**, sleep het `.inputactions`-bestand erin, stel **Map Name** in op `Player1`.
2. Doe hetzelfde voor **Player2**, stel **Map Name** in op `Player2`.
3. Druk op **Play** en test:
   - **Player1**: WASD bewegen, Spatie springen, Left Shift sprinten
   - **Player2**: IJKL bewegen, Enter springen

---

## Huiswerk: Input in je 3D Gym

Voeg de 2 spelerblokjes toe aan je eigen 3D Gym scene uit les 1.

Zorg dat:

- De spelers kunnen bewegen via het nieuwe Input System
- De spelers kunnen springen
- De gronddetectie correct werkt (via tag of layer)
- De scene een uitdagend parcours heeft om doorheen te bewegen

Optioneel (voor snelle werkers):

- Voeg een sprint-functie toe
- Implementeer de robuustere gronddetectie via `Physics.CheckSphere` (zie de stap-voor-stap instructie)

Maak een mooi gifje van je gameview waarbij je laat zien dat je 2 blokjes kunt besturen en presenteer deze op je readme.

Geef met tekst een toelichting op wat je hebt gemaakt.

Commit en push je voortgang naar je GitHub-repository en lever de link in op Simulise: `GD - M4 - GDV - HNR : Input System & Rigidbody`
