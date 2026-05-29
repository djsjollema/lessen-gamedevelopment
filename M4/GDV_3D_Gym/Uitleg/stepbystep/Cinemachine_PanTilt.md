# Step By Step — Cinemachine 3: Camera Systemen (Pan & Tilt)
**Zelfstandige stap-voor-stap instructie**

---

## Leerdoelen
- Je kunt een Cinemachine Virtual Camera instellen met een Follow-target
- Je begrijpt het verschil tussen pan (horizontaal) en tilt (verticaal) camerabesturing
- Je kunt de Cinemachine Input Handler koppelen aan het nieuwe Input System

---

## Achtergrond: Hoe werkt Cinemachine?

Cinemachine werkt met twee onderdelen:
- **CinemachineBrain**: zit op de Main Camera. Luistert naar alle Virtual Cameras en beslist welke actief is.
- **CinemachineCamera** (Virtual Camera): definieert hoe de camera beweegt en kijkt.

Je kunt meerdere Virtual Cameras maken (follow-cam, overview, cutscene-cam) en ze wisselen via prioriteit of vanuit code.

---

## Stap 1 — Cinemachine installeren

1. Ga naar **Window > Package Manager**.
2. Klik op het dropdown linksboven → **Unity Registry**.
3. Zoek naar **Cinemachine**.
4. Selecteer versie **3.x** en klik **Install**.

---

## Stap 2 — CinemachineBrain instellen op de Main Camera

Na installatie:

1. Selecteer de **Main Camera** in de Hierarchy.
2. Controleer of er automatisch een `CinemachineBrain`-component is toegevoegd. Zo niet: **Add Component > Cinemachine > CinemachineBrain**.
3. Laat de standaardinstellingen staan.

---

## Stap 3 — Follow-target aanmaken op de speler

Cinemachine volgt een specifiek punt op de speler, niet het hele object.

1. Selecteer het karakter in de Hierarchy.
2. Maak een leeg child-object: **rechtermuisknop > Create Empty**. Noem het `CameraTarget`.
3. Positioneer `CameraTarget` op borsthoogte: Y = 1.5.

---

## Stap 4 — Virtual Camera aanmaken (Follow-cam)

1. Ga naar **GameObject > Cinemachine > CinemachineCamera**.
2. Noem hem `VC_Follow`.
3. In de Inspector: stel in:
   - **Follow:** sleep `CameraTarget` hierheen
   - **Look At:** sleep `CameraTarget` hierheen

---

## Stap 5 — OrbitalFollow instellen

De `CinemachineOrbitalFollow`-component zorgt voor de pan & tilt beweging rondom de speler.

1. Selecteer `VC_Follow`.
2. Klik **Add Extension > CinemachineOrbitalFollow** (of het staat al als component).
3. Stel in:
   - **Radius / Camera Distance:** 5 (hoe ver de camera achter de speler is)
   - **Vertical Axis → Value:** 20 (standaard kijkhoek naar beneden, in graden)
   - **Vertical Axis → Range:** Min = -30, Max = 60 (tilt-beperking)
   - **Horizontal Axis:** dit is de pan-as

---

## Stap 6 — Input System koppelen aan Cinemachine

Cinemachine 3 gebruikt de `CinemachineInputAxisController` om input te ontvangen.

1. Selecteer `VC_Follow`.
2. **Add Component > Cinemachine > CinemachineInputAxisController**.
3. In de Inspector zie je de axes:
   - **Look X** → koppel aan de `Look`-actie (horizontale muis)
   - **Look Y** → koppel aan de `Look`-actie (verticale muis)

### Look-actie toevoegen aan InputActionAsset
4. Open `PlayerInput.inputactions`.
5. Voeg een actie toe: `Look`, **Action Type: Value**, **Control Type: Vector2**.
6. Binding: **Mouse/Delta** (voor muisbeweging).
7. **Save Asset**.

### Terugkoppelen in Cinemachine
8. In `CinemachineInputAxisController`:
   - Klik bij **Controllers** op **+**.
   - Stel **Name** in op `Look`.
   - Koppel de `Look`-action via de InputActionReference.

---

## Stap 7 — Damping instellen voor soepele camerabewegingen

1. Selecteer `VC_Follow`.
2. Zoek het `CinemachinePositionComposer` of `CinemachineOrbitalFollow`-component.
3. Stel in:
   - **Damping:** X = 0.5, Y = 0.5, Z = 0.5 (hoe snel de camera de speler volgt; 0 = instant)
4. Test in Play mode: de camera volgt nu met een kleine vertraging voor een professioneler gevoel.

---

## Stap 8 — Recentering inschakelen

Als de speler stopt met rondkijken, kan de camera automatisch terugkeren naar achter de speler.

1. Selecteer `VC_Follow`.
2. Zoek **Horizontal Axis** in het `CinemachineOrbitalFollow`-component.
3. Activeer **Recentering**:
   - ✅ **Enable Recentering**
   - **Wait Time:** 2 (seconden voor de camera begint te recenteren)
   - **Recentering Time:** 1 (seconden voor de overgang)

---

## Stap 9 — Camera-collision instellen (CinemachineDeoccluder)

Voorkomt dat de camera door muren gaat.

1. Selecteer `VC_Follow`.
2. **Add Extension > CinemachineDeoccluder**.
3. Stel in:
   - **Strategy:** Pull Camera Forward
   - **Camera Radius:** 0.3

---

## Stap 10 — Tweede Virtual Camera: Overview

1. **GameObject > Cinemachine > CinemachineCamera**. Noem hem `VC_Overview`.
2. Positioneer hem hoog boven de scene: Y = 20, kijk omlaag (Rotation X = 90).
3. Stel **Priority** in op `0` (lager dan de follow-cam, die op `10` staat).

### Wisselen via een knop
4. Maak een script `CameraSwitch.cs` en koppel dit aan een leeg GameObject:

```csharp
using UnityEngine;
using UnityEngine.InputSystem;
using Unity.Cinemachine;

public class CameraSwitch : MonoBehaviour
{
    [SerializeField] private CinemachineCamera followCam;
    [SerializeField] private CinemachineCamera overviewCam;
    [SerializeField] private InputActionAsset inputAsset;
    private InputAction switchAction;
    private bool overviewActive = false;

    void Awake()
    {
        // Voeg een "SwitchCamera"-actie toe aan je InputActionAsset (bijv. Tab-toets)
        switchAction = inputAsset.FindActionMap("Player").FindAction("SwitchCamera");
    }

    void OnEnable()  { inputAsset.FindActionMap("Player").Enable(); }
    void OnDisable() { inputAsset.FindActionMap("Player").Disable(); }

    void Update()
    {
        if (switchAction.WasPressedThisFrame())
        {
            overviewActive = !overviewActive;
            followCam.Priority   = overviewActive ? 0  : 10;
            overviewCam.Priority = overviewActive ? 10 : 0;
        }
    }
}
```

5. Voeg `SwitchCamera` toe aan de InputActionAsset met binding **Keyboard/Tab**.
6. Sleep de twee cameras naar de Inspector-velden.

---

## Stap 11 — Blend instellen

De `CinemachineBrain` bepaalt hoe soepel overgangen zijn.

1. Selecteer de **Main Camera**.
2. In het `CinemachineBrain`-component:
   - **Default Blend:** `EaseInOut`
   - **Default Blend Time:** `0.8` seconden

---

## Stap 12 — Testen

1. Druk op **Play**.
2. Beweeg de muis: draait de camera mee (pan links/rechts, tilt omhoog/omlaag)?
3. Loopt de speler weg: volgt de camera hem met damping?
4. Druk op **Tab**: wisselt de camera naar het bovenaanzicht met een vloeiende blend?
5. Loop naar een muur: wijkt de camera naar voren uit (deoccluder)?

---

## Veelgemaakte fouten & oplossingen

| Probleem | Oorzaak | Oplossing |
|---|---|---|
| Camera beweegt niet | CinemachineBrain ontbreekt op Main Camera | Add Component > CinemachineBrain |
| Input werkt niet | Look-actie niet gekoppeld | CinemachineInputAxisController instellen |
| Camera gaat door muren | Deoccluder niet ingesteld | Add Extension > CinemachineDeoccluder |
| Overgang niet soepel | Blend Time = 0 | CinemachineBrain → Default Blend Time |
| Pan werkt, tilt niet | Vertical axis range te klein | Stel Min/Max in op -30 / 60 |

---

## Controlelijst voor afronding

- [ ] Cinemachine 3 geïnstalleerd via Package Manager
- [ ] CinemachineBrain op de Main Camera aanwezig
- [ ] `CameraTarget` GameObject op borsthoogte van speler aangemaakt
- [ ] `VC_Follow` Virtual Camera met Follow en LookAt ingesteld
- [ ] OrbitalFollow: Camera Distance en Vertical Range ingesteld
- [ ] Look-actie aangemaakt in InputActionAsset (Mouse/Delta)
- [ ] CinemachineInputAxisController gekoppeld aan Look-actie
- [ ] Damping ingesteld voor soepele beweging
- [ ] Recentering ingeschakeld
- [ ] CinemachineDeoccluder toegevoegd
- [ ] `VC_Overview` aangemaakt en schakelbaar via Tab-toets
- [ ] Blend time ingesteld op 0.8 seconden
