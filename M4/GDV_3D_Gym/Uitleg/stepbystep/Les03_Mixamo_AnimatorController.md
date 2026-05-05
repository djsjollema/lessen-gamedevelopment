# Les 3 — Mixamo: Modellen, Animaties & Animator Controller
**Zelfstandige stap-voor-stap instructie**

---

## Leerdoelen
- Je kunt een karakter en animaties downloaden van Mixamo en correct importeren in Unity
- Je begrijpt de belangrijkste import settings (Rig, Avatar, Loop Time)
- Je kunt een Animator Controller opzetten met states, parameters en transitions

---

## Stap 1 — Karakter downloaden van Mixamo

1. Ga naar [mixamo.com](https://www.mixamo.com) en log in (gratis Adobe-account vereist).
2. Klik bovenaan op **Characters** en kies een karakter (bijv. "Xbot" of "Ybot").
3. Klik op **Use this character**.
4. Klik op **Download**.
5. Stel het formaat in:
   - **Format:** FBX for Unity
   - **Skin:** With Skin (voor het model inclusief texturen)
   - **Pose:** T-pose
6. Klik **Download** en sla het bestand op.

---

## Stap 2 — Animaties downloaden van Mixamo

Herhaal dit voor elke animatie die je nodig hebt (Idle, Walk, Run, Jump).

1. Klik bovenaan op **Animations**.
2. Zoek een animatie, bijv. `Idle`.
3. Klik de animatie aan — je karakter toont hem direct.
4. Klik **Download**:
   - **Format:** FBX for Unity
   - **Skin:** Without Skin (want je hebt het model al)
   - **Frames per Second:** 30
   - **Keyframe Reduction:** None
5. Sla elke animatie op met een duidelijke naam: `Worker_Idle.fbx`, `Worker_Walk.fbx`, etc.

Download minimaal:
- `Idle` (rustig staan)
- `Walking` (lopen)
- `Running` (rennen)
- `Jump` (sprong omhoog)
- `Falling Idle` (in de lucht)
- `Hard Landing` (landen)

---

## Stap 3 — FBX-bestanden importeren in Unity

1. Sleep alle gedownloade `.fbx`-bestanden vanuit Windows Verkenner naar de **Project** view in Unity (bijv. naar de map `Assets/3d/`).
2. Unity importeert ze automatisch.

---

## Stap 4 — Rig instellen op Humanoid

Dit is de **belangrijkste stap** — zonder dit werken animaties niet correct op het karakter.

1. Selecteer het **karakter**-FBX in de Project view (het model mét skin, bijv. `Worker_Idle_SKIN.fbx`).
2. Ga in de Inspector naar het tabblad **Rig**.
3. Stel **Animation Type** in op **Humanoid**.
4. Klik **Apply**.
5. Klik daarna op **Configure...** om de Avatar te controleren.
6. In het Avatar-venster: controleer of alle lichaamsdelen groen zijn. Rood betekent dat een bone niet is herkend.
7. Als alles groen is: klik **Done**.

### Animaties instellen op Humanoid
Herhaal stap 4 voor **elke animatie-FBX** (zonder skin):
1. Selecteer de animatie-FBX.
2. Rig → Animation Type → **Humanoid**.
3. Stel **Avatar Definition** in op **Copy From Other Avatar**.
4. Sleep het Avatar van je karakter-FBX naar het **Source** veld.
5. Klik **Apply**.

---

## Stap 5 — Animatie-clips instellen (Loop Time, Root Motion)

1. Selecteer een animatie-FBX, bijv. `Worker_Walk.fbx`.
2. Ga naar het tabblad **Animation** in de Inspector.
3. Selecteer de animatie-clip (in de lijst onderaan).
4. Stel in:
   - ✅ **Loop Time** — vink aan voor lopen, rennen, idle (herhalende animaties)
   - ✅ **Loop Pose** — vink aan voor een naadloze loop
   - **Root Transform Rotation** → Bake Into Pose: ✅
   - **Root Transform Position (Y)** → Bake Into Pose: ✅ (voor jump/landing: uitvinken)
   - **Root Transform Position (XZ)** → Bake Into Pose: ✅ (voor in-place animaties)
5. Klik **Apply**.

> **Loop Time aan vs uit:**
> - ✅ Loop Time aan: Idle, Walk, Run (herhalen eindeloos)
> - ❌ Loop Time uit: Jump, Landing (eenmalig afspelen)

---

## Stap 6 — Animator Controller aanmaken

1. In de Project view: **rechtermuisknop > Create > Animator Controller**.
2. Noem het `WorkerController`.
3. Dubbelklik om de **Animator** editor te openen.

---

## Stap 7 — States toevoegen aan de Animator Controller

1. In de Animator editor: **rechtermuisknop > Create State > Empty**.
2. Herhaal dit voor elke animatie. Noem de states:
   - `Idle`
   - `Walk`
   - `Run`
   - `Jump`
   - `Fall`
   - `Land`
3. Koppel een animatieclip aan elke state:
   - Selecteer de state.
   - Sleep in de Inspector de bijbehorende `.fbx`-animatieclip naar het veld **Motion**.

> **Entry:** De oranje state is de beginstate. Sleep een pijl van **Entry** naar `Idle` om de game te beginnen in de Idle-staat.

---

## Stap 8 — Parameters aanmaken

Parameters zijn variabelen waarmee scripts de Animator aansturen.

1. Klik links op het tabblad **Parameters** in de Animator editor.
2. Klik op **+** en voeg toe:
   - `InputVertical` — **Float** (0 = stil, 1 = lopen, 2 = rennen)
   - `Grounded` — **Bool** (true = op de grond)
   - `JumpTrigger` — **Trigger** (éénmalig schot)

---

## Stap 9 — Transitions aanmaken

Transitions bepalen wanneer de Animator van de ene naar de andere state gaat.

### Idle → Walk
1. Klik met de rechtermuisknop op de `Idle` state → **Make Transition** → klik op `Walk`.
2. Selecteer de transition (de pijl). In de Inspector:
   - ❌ **Has Exit Time** — uitvinken (we willen directe overgang)
   - **Transition Duration:** 0.1
3. Klik **+ (Add Condition)**:
   - `InputVertical` → **Greater** → `0.1`

### Walk → Idle
1. Rechtermuisknop op `Walk` → **Make Transition** → `Idle`.
2. Condition: `InputVertical` → **Less** → `0.1`

### Walk → Run
1. `Walk` → `Run`. Condition: `InputVertical` → **Greater** → `0.9`

### Run → Walk
1. `Run` → `Walk`. Condition: `InputVertical` → **Less** → `0.9`

### Idle/Walk/Run → Jump (via Any State)
1. Rechtermuisknop op **Any State** → **Make Transition** → `Jump`.
2. Condition: `JumpTrigger`

### Jump → Fall
1. `Jump` → `Fall`. **Has Exit Time**: ✅, Exit Time: `0.8` (na 80% van de sprong-animatie)

### Fall → Land
1. `Fall` → `Land`. Condition: `Grounded` → **true**

### Land → Idle
1. `Land` → `Idle`. **Has Exit Time**: ✅, Exit Time: `1.0`

---

## Stap 10 — Animator Controller koppelen aan karakter

1. Sleep het karakter-FBX (`Worker_Idle_SKIN.fbx`) vanuit de Project view naar de **Hierarchy** om hem in de scene te plaatsen.
2. Selecteer het karakter in de Hierarchy.
3. In de Inspector: zoek het **Animator**-component.
4. Sleep je `WorkerController` naar het veld **Controller**.
5. Zorg dat **Avatar** ingesteld is op het Avatar van je karakter.

---

## Stap 11 — Animator aansturen vanuit script

Voeg dit toe aan je movement-script (of maak een los testscript):

```csharp
private Animator animator;

void Awake()
{
    animator = GetComponentInChildren<Animator>();
}

void Update()
{
    Vector2 input = moveAction.ReadValue<Vector2>();

    // InputVertical aansturen op basis van beweging
    float speed = input.magnitude; // 0 = stil, 1 = beweegt
    if (sprintAction.IsPressed()) speed = 2f; // sprint = waarde 2
    animator.SetFloat("InputVertical", speed);

    // Grounded doorgeven
    animator.SetBool("Grounded", characterController.isGrounded);

    // Springen
    if (jumpAction.WasPressedThisFrame() && characterController.isGrounded)
    {
        animator.SetTrigger("JumpTrigger");
    }
}
```

---

## Stap 12 — Testen

1. Druk op **Play**.
2. Controleer:
   - Staat het karakter stil in Idle?
   - Speelt Walk af als je beweegt?
   - Schakelt hij over naar Run bij sprinten?
   - Springt de animatie correct en landt hij terug?
3. Open het **Animator**-venster in Play mode om live te zien welke state actief is.

---

## Veelgemaakte fouten & oplossingen

| Probleem | Oorzaak | Oplossing |
|---|---|---|
| Avatar is rood | Bones niet herkend | Configure Avatar → wijs bones handmatig toe |
| Animatie speelt niet in loop | Loop Time staat uit | Animation tab → Loop Time ✅ |
| Karakter "glijdt" weg tijdens animatie | Root Motion staat aan | Bake XZ into Pose ✅ in animatie-tab |
| Transition werkt niet | Condition klopt niet | Controleer parameter-naam en operator |
| Animator Controller niet gekoppeld | Controller-veld leeg | Sleep controller naar Animator component |
| Animatie knippert abrupt | Transition Duration = 0 | Stel Transition Duration in op 0.1–0.2 |

---

## Controlelijst voor afronding

- [ ] Karakter en animaties gedownload van Mixamo (FBX for Unity)
- [ ] Rig → Humanoid ingesteld op karakter én animaties
- [ ] Avatar is groen (geen rode bones)
- [ ] Loop Time aan voor Idle/Walk/Run
- [ ] Animator Controller aangemaakt met alle states
- [ ] Parameters aangemaakt: `InputVertical`, `Grounded`, `JumpTrigger`
- [ ] Alle transitions correct met conditions
- [ ] Script stuurt animator correct aan
- [ ] Alle animaties testen correct in Play mode
