# Les 4 — CharacterController: Bewegen & Springen
**Zelfstandige stap-voor-stap instructie**

---

## Leerdoelen
- Je begrijpt het verschil tussen `CharacterController` en `Rigidbody` beweging
- Je kunt `CharacterController.Move()` correct gebruiken
- Je kunt de sprong-formule uitleggen en toepassen

---

## Achtergrond: CharacterController vs. Rigidbody

| Eigenschap | CharacterController | Rigidbody |
|---|---|---|
| Bewegingscontrole | Direct, volledig in jouw code | Indirect via krachten |
| Botsingen | Ingebouwd (schuift langs muren) | Via PhysX engine |
| Zwaartekracht | Zelf implementeren | Automatisch |
| Gebruik | Speler-characters | Physische objecten (barrels, ballen) |
| Animator-koppeling | Eenvoudig | Soms complex |

**Kies CharacterController als:** je volledige controle wilt over hoe de speler beweegt.  
**Kies Rigidbody als:** een object realistisch moet reageren op botsingen en krachten.

---

## Stap 1 — CharacterController toevoegen aan het karakter

1. Sleep het Worker-prefab (of je eigen Mixamo-karakter) naar de **Hierarchy**.
2. Selecteer het karakter.
3. In de Inspector: **Add Component > Physics > Character Controller**.
4. Stel de CharacterController in:
   - **Center:** Y = 1.0 (middelpunt op borsthoogte, afhankelijk van karakterhoogte)
   - **Radius:** 0.4 (breedte van de capsule)
   - **Height:** 2.0 (hoogte van het karakter)
5. Controleer in de Scene view: de groene capsule moet het karakter netjes omhullen.

> **Tip:** Klik op het **Gizmos**-dropdown in de Scene view en zorg dat Physics is aangevinkt om de capsule te zien.

---

## Stap 2 — Script aanmaken: MoveCharacterController.cs

1. Maak een nieuw C#-script: `MoveCharacterController`.
2. Schrijf de volgende code:

```csharp
using UnityEngine;
using UnityEngine.InputSystem;

public class MoveCharacterController : MonoBehaviour
{
    [SerializeField] private InputActionAsset inputAsset;
    [SerializeField] private string mapName = "Player";
    [SerializeField] private float moveSpeed = 5f;
    [SerializeField] private float sprintMultiplier = 2f;
    [SerializeField] private float rotationSpeed = 100f;
    [SerializeField] private float jumpHeight = 2f;
    [SerializeField] private float gravity = -20f;

    private InputActionMap map;
    private InputAction moveAction;
    private InputAction sprintAction;
    private InputAction jumpAction;

    private CharacterController characterController;
    private Animator animator;
    private float verticalVelocity;

    void Awake()
    {
        characterController = GetComponent<CharacterController>();
        animator = GetComponentInChildren<Animator>();

        map          = inputAsset.FindActionMap(mapName);
        moveAction   = map.FindAction("Move");
        sprintAction = map.FindAction("Sprint");
        jumpAction   = map.FindAction("Jump");
    }

    void OnEnable()  { map.Enable(); }
    void OnDisable() { map.Disable(); }

    void Update()
    {
        Vector2 movementInput = moveAction.ReadValue<Vector2>();

        // Sprint
        if (sprintAction.IsPressed())
            movementInput = movementInput.normalized * sprintMultiplier;
        else
            movementInput = movementInput.normalized;

        // Voorwaartse beweging
        Vector3 move = transform.forward * movementInput.y * moveSpeed * Time.deltaTime;

        // Rotatie (links/rechts draaien)
        transform.Rotate(Vector3.up * movementInput.x * rotationSpeed * Time.deltaTime);

        // Zwaartekracht en springen
        if (characterController.isGrounded)
        {
            verticalVelocity = -1f; // kleine downward force om grounded te blijven

            if (jumpAction.WasPressedThisFrame())
            {
                // Sprong-formule: v = sqrt(2 * |g| * h)
                verticalVelocity = Mathf.Sqrt(2f * Mathf.Abs(gravity) * jumpHeight);
                animator.SetTrigger("JumpTrigger");
            }
        }
        else
        {
            // Niet op de grond: zwaartekracht toepassen
            verticalVelocity += gravity * Time.deltaTime;
        }

        move.y = verticalVelocity * Time.deltaTime;

        characterController.Move(move);

        // Animator aansturen
        animator.SetFloat("InputVertical", movementInput.y);
        animator.SetBool("Grounded", characterController.isGrounded);
    }
}
```

3. Sla het script op.

---

## Stap 3 — De sprong-formule begrijpen

De formule `verticalVelocity = Mathf.Sqrt(2f * Mathf.Abs(gravity) * jumpHeight)` komt uit de natuurkunde.

**Kinematische vergelijking:**  
$$v^2 = u^2 + 2as$$

Waarbij:
- $v$ = eindsnelheid (0, op het hoogste punt)
- $u$ = beginsnelheid (wat we zoeken)
- $a$ = versnelling (zwaartekracht, negatief)
- $s$ = afstand (jumpHeight)

Oplossen naar $u$:
$$u = \sqrt{2 \times |g| \times h}$$

**Voorbeeld met waarden uit het script:**
- gravity = -20, jumpHeight = 2
- $u = \sqrt{2 \times 20 \times 2} = \sqrt{80} \approx 8.94$

Dit is de beginsnelheid die het karakter omhoog geeft om precies 2 meter hoog te springen.

---

## Stap 4 — Script koppelen aan het karakter

1. Selecteer het karakter in de Hierarchy.
2. Sleep het script `MoveCharacterController` naar de Inspector.
3. Vul de velden in:
   - **Input Asset:** sleep `PlayerInput.inputactions` hierheen
   - **Map Name:** `Player`
   - **Move Speed:** `5`
   - **Sprint Multiplier:** `2`
   - **Rotation Speed:** `100`
   - **Jump Height:** `2`
   - **Gravity:** `-20`

---

## Stap 5 — Testen: sprong aanpassen

1. Druk op **Play**.
2. Test het springen met Spatie.
3. Stop Play mode.
4. Verander **Jump Height** naar `5` en **Gravity** naar `-10` → langzame maansprong.
5. Verander **Jump Height** naar `1` en **Gravity** naar `-30` → snelle aardse sprong.
6. Noteer welke waarden het beste voelen voor je game.

---

## Stap 6 — Sprint-indicator toevoegen (UI)

### Canvas aanmaken
1. **GameObject > UI > Canvas**
2. Stel de Canvas **Render Mode** in op **Screen Space – Overlay**.

### Achtergrondpaneel voor de indicator
3. Rechtermuisknop op Canvas → **UI > Image**. Noem het `SprintBG`.
4. In de Inspector: stel Anchor in op linksonder. Geef het een grijze kleur.
5. Stel Width = 200, Height = 40 in.

### Indicator image
6. Rechtermuisknop op `SprintBG` → **UI > Image**. Noem het `SprintIndicator`.
7. Geef het een rode kleur. Stel Width = 200, Height = 40.

### StaminaUI-script
8. Maak een nieuw script `StaminaUI.cs` en koppel het aan het karakter:

```csharp
using UnityEngine;
using UnityEngine.UI;
using UnityEngine.InputSystem;

public class StaminaUI : MonoBehaviour
{
    [SerializeField] private Image sprintIndicator;
    [SerializeField] private float maxStamina = 3f;
    [SerializeField] private InputActionAsset inputAsset;

    private InputAction sprintAction;
    private float currentStamina;
    private bool staminaDepleted = false;

    void Awake()
    {
        sprintAction = inputAsset.FindActionMap("Player").FindAction("Sprint");
        currentStamina = maxStamina;
    }

    void OnEnable()  { inputAsset.FindActionMap("Player").Enable(); }
    void OnDisable() { inputAsset.FindActionMap("Player").Disable(); }

    void Update()
    {
        if (sprintAction.IsPressed() && !staminaDepleted)
        {
            currentStamina -= Time.deltaTime;
            sprintIndicator.color = Color.red;

            if (currentStamina <= 0)
            {
                currentStamina = 0;
                staminaDepleted = true;
            }
        }
        else
        {
            sprintIndicator.color = Color.green;
            currentStamina = Mathf.Min(currentStamina + Time.deltaTime, maxStamina);

            if (currentStamina >= maxStamina)
                staminaDepleted = false;
        }
    }
}
```

9. Sleep `SprintIndicator` naar het **Sprint Indicator**-veld in de Inspector.

---

## Stap 7 — Coyote Time toevoegen

Coyote time geeft de speler een korte tijdspanne om te springen nadat ze een platform zijn afgelopen, wat de besturing eerlijker maakt.

Voeg toe aan `MoveCharacterController.cs`:

```csharp
[SerializeField] private float coyoteTime = 0.15f;
private float coyoteTimer = 0f;

void Update()
{
    // Coyote timer bijhouden
    if (characterController.isGrounded)
        coyoteTimer = coyoteTime;
    else
        coyoteTimer -= Time.deltaTime;

    bool canJump = coyoteTimer > 0f;

    // ... (rest van de update code)

    if (characterController.isGrounded)
    {
        verticalVelocity = -1f;
    }
    else
    {
        verticalVelocity += gravity * Time.deltaTime;
    }

    // Springen: gebruik canJump in plaats van isGrounded
    if (jumpAction.WasPressedThisFrame() && canJump)
    {
        verticalVelocity = Mathf.Sqrt(2f * Mathf.Abs(gravity) * jumpHeight);
        coyoteTimer = 0f; // voorkom dubbele sprong
        animator.SetTrigger("JumpTrigger");
    }
}
```

---

## Stap 8 — Obstacle course bouwen

1. Maak in de scene een reeks platforms met **GameObject > 3D Object > Cube**.
2. Schaal ze op verschillende hoogtes: klein/breed, smal, op palen.
3. Voeg een bewegend platform toe:

```csharp
using UnityEngine;

public class MovingPlatform : MonoBehaviour
{
    [SerializeField] private Vector3 moveDirection = Vector3.right;
    [SerializeField] private float distance = 3f;
    [SerializeField] private float speed = 2f;

    private Vector3 startPosition;

    void Start() { startPosition = transform.position; }

    void Update()
    {
        float t = Mathf.PingPong(Time.time * speed, distance);
        transform.position = startPosition + moveDirection * t;
    }
}
```

4. Voeg een startzone toe: een groen plat vlak met een TextMeshPro tekst "START".
5. Voeg een eindzone toe: geel vlak met "FINISH" en een `OnTriggerEnter`-script dat "Gehaald!" print.

---

## Veelgemaakte fouten & oplossingen

| Probleem | Oorzaak | Oplossing |
|---|---|---|
| Karakter zakt door de vloer | CharacterController te klein | Pas Center en Height aan |
| Karakter stuitert | `verticalVelocity = -1f` ontbreekt | Altijd kleine downward force als `isGrounded` |
| Geen rotatie | `movementInput.x` aangestuurd | X-as van Move input stuurt rotatie, niet strafe |
| Sprong te laag | `jumpHeight` of `gravity` verkeerd | Controleer de formule — gravity moet negatief zijn |
| Sprint werkt niet | Sprint Action niet ingesteld | Controleer binding in InputActionAsset |
| Animator loopt niet | Script niet gekoppeld | Controleer `GetComponentInChildren<Animator>()` |

---

## Controlelijst voor afronding

- [ ] CharacterController component aanwezig en correct ingesteld (Radius, Height, Center)
- [ ] `MoveCharacterController.cs` geschreven en gekoppeld
- [ ] Bewegen voor/achter werkt met W/S
- [ ] Rotatie werkt met A/D
- [ ] Sprint verdubbelt snelheid
- [ ] Springen werkt met de correcte formule
- [ ] `isGrounded` check aanwezig — geen springen in de lucht
- [ ] Animator ontvangt `InputVertical`, `Grounded`, `JumpTrigger`
- [ ] Coyote time geïmplementeerd (bonus)
- [ ] Obstacle course gebouwd met bewegend platform
