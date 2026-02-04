# Les 5.1 - Animaties Aanroepen in Unity

## Leerdoelen

Na deze les kun je:

- Het Unity Animation systeem begrijpen (Animator, Clips, Controller)
- Animaties aanroepen via code met Triggers en Booleans
- Parameters gebruiken om animaties te sturen
- Blend Trees begrijpen voor vloeiende overgangen

---

## Deel 1: Animation Systeem Overzicht (10 min)

### Componenten

```
┌─────────────────────────────────────────────────────────────┐
│                    ANIMATION SYSTEEM                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │  Animator   │───►│  Animator   │───►│  Animation  │     │
│  │  Component  │    │  Controller │    │    Clips    │     │
│  └─────────────┘    └─────────────┘    └─────────────┘     │
│        │                  │                   │             │
│   Op GameObject      State Machine       Keyframe data      │
│                      (states, transitions)  (.anim files)   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

| Component | Functie |
|-----------|---------|
| **Animation Clip** | Bevat keyframes voor één animatie |
| **Animator Controller** | State machine die clips beheert |
| **Animator Component** | Speelt de controller af op een GameObject |

### Animator Controller Voorbeeld

```
┌──────────────────────────────────────────────────────┐
│               ANIMATOR CONTROLLER                     │
├──────────────────────────────────────────────────────┤
│                                                      │
│   [Entry]──►[Idle]◄──────────────────┐              │
│               │                       │              │
│               │ speed > 0.1          │              │
│               ▼                       │              │
│            [Walk]──────────────────►──┤ speed < 0.1 │
│               │                       │              │
│               │ isJumping = true      │              │
│               ▼                       │              │
│            [Jump]─────────────────────┘              │
│                   animation complete                 │
│                                                      │
└──────────────────────────────────────────────────────┘
```

---

## Deel 2: Animator Setup (15 min)

### Stap 1: Animator Controller Aanmaken

1. **Project window** → Rechtermuisknop → Create → **Animator Controller**
2. Noem het `PlayerAnimator`
3. Dubbelklik om **Animator window** te openen

### Stap 2: Animation Clips Toevoegen

1. Sleep animation clips naar het Animator window
2. Of: Rechtermuisknop → **Create State** → **Empty**
3. Selecteer state → Inspector → Motion → kies clip

### Stap 3: Transitions Maken

1. Rechtermuisknop op een state → **Make Transition**
2. Klik op de doel-state
3. Selecteer de pijl om conditions in te stellen

### Stap 4: Parameters Aanmaken

In het Animator window, klik op **Parameters** tab:

| Parameter Type | Gebruik |
|---------------|---------|
| **Float** | Snelheid, richting (continuous) |
| **Int** | Discrete states |
| **Bool** | Aan/uit states |
| **Trigger** | Eenmalige events |

```
Parameters:
├── speed (Float)
├── isGrounded (Bool)
├── direction (Float)
└── jump (Trigger)
```

---

## Deel 3: Animaties Aanroepen via Code (20 min)

### Animator Referentie

```csharp
using UnityEngine;

public class PlayerAnimation : MonoBehaviour
{
    private Animator animator;
    
    void Start()
    {
        animator = GetComponent<Animator>();
    }
}
```

### Parameters Instellen

```csharp
void Update()
{
    // Float parameter (bijv. voor snelheid)
    float speed = Input.GetAxis("Horizontal");
    animator.SetFloat("speed", Mathf.Abs(speed));
    
    // Bool parameter
    animator.SetBool("isGrounded", IsGrounded());
    
    // Int parameter
    animator.SetInteger("health", currentHealth);
    
    // Trigger (eenmalig event)
    if (Input.GetKeyDown(KeyCode.Space))
    {
        animator.SetTrigger("jump");
    }
}
```

### Parameters Uitlezen

```csharp
// Huidige waarde opvragen
float currentSpeed = animator.GetFloat("speed");
bool grounded = animator.GetBool("isGrounded");
int health = animator.GetInteger("health");
```

### Complete Voorbeeld: Pac-Man Animaties

```csharp
public class PacManAnimation : MonoBehaviour
{
    private Animator animator;
    private Vector2 moveDirection;
    
    void Start()
    {
        animator = GetComponent<Animator>();
    }
    
    void Update()
    {
        // Bewegingsrichting naar animator
        animator.SetFloat("moveX", moveDirection.x);
        animator.SetFloat("moveY", moveDirection.y);
        
        // Is Pac-Man aan het bewegen?
        bool isMoving = moveDirection.magnitude > 0.1f;
        animator.SetBool("isMoving", isMoving);
    }
    
    // Aangeroepen door movement script
    public void SetMoveDirection(Vector2 direction)
    {
        moveDirection = direction;
    }
    
    // Aangeroepen bij power-up
    public void PlayPowerUpAnimation()
    {
        animator.SetTrigger("powerUp");
    }
    
    // Aangeroepen bij death
    public void PlayDeathAnimation()
    {
        animator.SetTrigger("die");
    }
}
```

---

## Deel 4: Transition Settings (15 min)

### Transition Configuratie

Selecteer een transition pijl in de Animator:

| Setting | Beschrijving | Typische waarde |
|---------|--------------|-----------------|
| **Has Exit Time** | Wacht tot animatie klaar is | Uit voor responsive controls |
| **Exit Time** | Wanneer transition mag starten (0-1) | 0.9 (bijna einde) |
| **Transition Duration** | Blend tijd tussen animaties | 0.1-0.25 |
| **Conditions** | Wanneer transition triggert | Parameter checks |

### Responsive vs Smooth

```csharp
// Voor RESPONSIVE controls (actie games):
// Has Exit Time: OFF
// Transition Duration: 0-0.1

// Voor SMOOTH animations (cutscenes):
// Has Exit Time: ON
// Transition Duration: 0.25-0.5
```

### Any State Transitions

Voor animaties die vanuit élke state kunnen starten:

1. Rechtermuisknop op **Any State**
2. Make Transition naar je doel state
3. Handig voor: death, damage, power-ups

```
┌─────────────────────────────────────────┐
│                                         │
│  [Any State]────► [Death]               │
│       │              │                  │
│       │              └──► [Exit]        │
│       │                                 │
│       └─────────► [Damage]              │
│                      │                  │
│                      └──► (terug naar   │
│                           vorige state) │
└─────────────────────────────────────────┘
```

---

## Oefeningen (60 min)

### Oefening 1: Animator Setup (20 min)

1. Maak een nieuw `PlayerAnimator` controller
2. Voeg 3 states toe: `Idle`, `Walk`, `Die`
3. Maak parameters:
   - `speed` (Float)
   - `die` (Trigger)
4. Stel transitions in:
   - Idle → Walk: speed > 0.1
   - Walk → Idle: speed < 0.1
   - Any State → Die: die trigger

**Verwachte Animator setup:**
```
[Entry]
    │
    ▼
[Idle] ◄────────────────┐
    │                   │
    │ speed > 0.1      │ speed < 0.1
    ▼                   │
[Walk] ─────────────────┘

[Any State]
    │
    │ die (trigger)
    ▼
[Die]
```

### Oefening 2: Animatie via Code (20 min)

1. Maak een `PlayerAnimation` script
2. Koppel aan een player met Animator
3. Stuur de `speed` parameter vanuit je movement script
4. Trigger `die` wanneer speler een enemy raakt

**Test scenario:**
```
Speler staat stil → Idle animatie speelt
Speler beweegt   → Walk animatie speelt
Speler stopt     → Terug naar Idle
Speler raakt enemy → Death animatie speelt

Console output:
Setting speed: 0
Setting speed: 0.8
Setting speed: 1.0
Setting speed: 0.3
Setting speed: 0
Triggering: die
```

### Oefening 3: Directional Animation (20 min)

Voor Pac-Man heb je animaties nodig voor alle richtingen.

1. Voeg parameters toe:
   - `moveX` (Float): -1 tot 1
   - `moveY` (Float): -1 tot 1
2. Maak states: `WalkUp`, `WalkDown`, `WalkLeft`, `WalkRight`
3. Gebruik conditions om juiste richting te kiezen

**Transition conditions:**
```
Idle → WalkRight:  moveX > 0.5
Idle → WalkLeft:   moveX < -0.5
Idle → WalkUp:     moveY > 0.5
Idle → WalkDown:   moveY < -0.5

All Walk states → Idle:  speed < 0.1
```

**Code:**
```csharp
void UpdateAnimation(Vector2 direction)
{
    animator.SetFloat("moveX", direction.x);
    animator.SetFloat("moveY", direction.y);
    animator.SetFloat("speed", direction.magnitude);
}
```

---

## Samenvatting

| Actie | Code |
|-------|------|
| Animator ophalen | `animator = GetComponent<Animator>();` |
| Float instellen | `animator.SetFloat("name", value);` |
| Bool instellen | `animator.SetBool("name", true/false);` |
| Trigger activeren | `animator.SetTrigger("name");` |
| Waarde opvragen | `animator.GetFloat("name");` |

### Parameter Types

| Type | Wanneer Gebruiken |
|------|-------------------|
| **Float** | Snelheid, richting, blending |
| **Bool** | Toggle states (grounded, powered) |
| **Trigger** | Eenmalige events (jump, attack, die) |
| **Int** | Discrete states (weapon type, level) |

### Quick Reference: Transition Settings

```
Voor snelle response (actiegames):
├── Has Exit Time: ❌ OFF
├── Transition Duration: 0 - 0.1
└── Conditions: Gebruik triggers/bools

Voor smooth blending:
├── Has Exit Time: ✅ ON
├── Transition Duration: 0.2 - 0.5
└── Exit Time: 0.8 - 1.0
```

---

## Volgende Les

In **Les 5.2** gaan we eigen animaties creëren met het Animation window!
