# M4 GDV HNR LES 3: Mixamo, Animaties & Animator Controller

Deze les leren jullie het volgende:

- Je kunt een karakter en animaties downloaden van Mixamo en importeren in Unity
- Je begrijpt de belangrijkste import settings (Rig, Avatar, Loop Time)
- Je kunt een Animator Controller opzetten met states, parameters en transitions
- Je kunt de Animator aansturen vanuit een script

In deze les laat ik zien hoe je een geanimeerd karakter in Unity zet. Je kunt direct meedoen of kijken en aantekeningen maken.

De uitgebreide stap-voor-stap instructie staat hier: [Les03_StepByStep.md](../Uitleg/stepbystep/Les03_Mixamo_AnimatorController.md)

---

## Wat is een Animator Controller?

Een **Animator Controller** bepaalt wanneer welke animatie wordt afgespeeld. Het werkt als een stroomdiagram:

- **States** — animaties zoals Idle, Walk, Run, Jump
- **Transitions** — de pijlen die bepalen wanneer je van de ene naar de andere state gaat
- **Parameters** — variabelen die vanuit scripts worden ingesteld om de transitions te triggeren

---

## Oefening 1 — Karakter en animaties downloaden van Mixamo (~10 min)

Ik laat live zien hoe je van [mixamo.com](https://www.mixamo.com) downloadt.

**Karakter downloaden:**

- Kies een karakter → **Download**
- Format: `FBX for Unity`, Skin: `With Skin`, Pose: `T-pose`

**Animaties downloaden** (zonder skin, want je hebt het model al):

- Format: `FBX for Unity`, Skin: `Without Skin`, FPS: `30`

Download de volgende animaties:

- Idle
- Walk
- Run
- Jump

Sla elke animatie op met een duidelijke naam, bijv. `Player_Walk.fbx`.

---

## Oefening 2 — FBX importeren & Rig instellen op Humanoid (~10 min)

Dit is de **belangrijkste stap** — zonder Humanoid rig werken animaties niet op het karakter.

Ik laat zien:

1. Sleep alle `.fbx`-bestanden naar de **Project** view in Unity.
2. Selecteer het **karakter-FBX** → Inspector → tabblad **Rig** → `Animation Type: Humanoid` → **Apply**.
3. Klik **Configure...** en controleer of alle lichaamsdelen **groen** zijn.
4. Herhaal voor elke **animatie-FBX**:
   - Rig → Humanoid
   - `Avatar Definition: Copy From Other Avatar`
   - Sleep het Avatar van je karakter naar **Source** → **Apply**

> Als een lichaamsdeel rood is, kun je de bone handmatig toewijzen in het Avatar-venster.

---

## Oefening 3 — Materials en textures uitpakken (~5 min)

FBX-bestanden bevatten materialen en textures ingebakken in het bestand. Zolang ze daarin zitten kun je ze niet aanpassen en kunnen ze paars of verkleurd verschijnen in URP. Je pakt ze los uit naar aparte bestanden.

Ik laat zien:

1. Selecteer het **karakter-FBX** (mét skin) in de Project view.
2. Ga in de Inspector naar het tabblad **Materials**.
3. Klik **Extract Textures...** → kies een map, bijv. `Assets/3d/Textures` → **Choose**.
4. Klik **Extract Materials...** → kies een map, bijv. `Assets/3d/Materials` → **Choose**.
5. Klik **Apply**.

Na het uitpakken toont het karakter zijn kleuren en texturen correct in de scene.

> Als het karakter roze blijft, converteer dan via **Edit → Rendering → Render Pipeline Converter**.

---

## Oefening 4 — Loop Time & Root Motion instellen (~5 min)

Voor de animatie-clip (FBX) stel je in of hij herhaalt en of hij het karakter zelf verplaatst.

Moet de animatie loopen? of maar 1x afgespeeld worden?

- Idle?
- Walk?
- Run?
- JumpUp?

> **Root Motion** (Bake into Pose) zorgt dat de animatie het karakter niet zelf verplaatst — dat doen we vanuit de code.

---

## Oefening 5 — Animator Controller opzetten (~15 min)

Ik maak live een `PlayerController` aan en laat zien hoe je states, parameters en transitions instelt.

**States:**

- `Idle`, `Walk`, `Run`, `jump`
- Sleep per state de bijbehorende animatieclip naar het veld **Motion**

**Parameters:**

- `Speed` — Float (0 = stil, 1-5 = lopen, 6-10 = rennen)
- `Grounded` — Bool
- `JumpTrigger` — Trigger

**Transitions (voorbeelden):**

| Van       | Naar | Conditie            |
| --------- | ---- | ------------------- |
| Idle      | Walk | `InputVertical > 2` |
| Walk      | Idle | `InputVertical < 2` |
| Walk      | Run  | `InputVertical > 7` |
| Run       | Walk | `InputVertical < 7` |
| Any State | Jump | `JumpTrigger`       |
| Jump      | Idle | HasExitTime         |

> Zet **Has Exit Time uit** en **Transition Duration op 0.1** voor soepele overgangen (behalve bij Jump).

---

## Oefening 6 — Animator aansturen vanuit script (~10 min)

Ik voeg aan het bestaande InputPlayer-script code toe om de Animator aan te sturen:

```csharp
//voeg toe aan bestaande code
private Animator animator;

void Awake()
{
    //voeg toe aan bestaande code
    animator = GetComponentInChildren<Animator>();
}

void Update()
{

    //Verwerk in de bestaande code
    if (jumpAction.WasPressedThisFrame() && isGrounded){

        rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
        isGrounded = false;

        //nieuwe regel om sprong animatie te triggeren
        animator.SetTrigger("JumpTrigger");

    }
    //Loop en sprint animaties triggeren
    animator.SetFloat("Speed", speed);
    animator.SetBool("Grounded", isGrounded);
}
```

> Open het **Animator**-venster tijdens Play mode om live te zien welke state actief is.

---

## Huiswerk: Geanimeerd karakter in je 3D Gym

Voeg het geanimeerde karakter toe aan je eigen 3D Gym scene uit les 1 en 2.

Zorg dat:

- Het karakter Idle staat als hij stilstaat
- Het karakter loopt en rent op basis van input
- Het karakter springt
- De gronddetectie correct werkt

Optioneel (voor snelle werkers):

- Probeer de sprong op te breken in 3 delen: Springen, Vallen en landen en zorg dat deze op het juiste moment afspelen.
- Experimenteer met **Blend Trees** voor vloeiende overgangen tussen Idle, Walk en Run

Commit en push je voortgang naar je GitHub-repository en lever de link in op Simulise: `GD - M4 - GDV - HNR : Mixamo & Animator Controller`
