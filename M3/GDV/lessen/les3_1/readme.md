# Les 3.1 - Player Movement, Input & Collision Detection

## Leerdoelen

Na deze les kun je:

- Input afhandelen met Unity's Input System
- Verschillende bewegingsmethodes toepassen (Translate, position, Rigidbody)
- Grid-based movement implementeren
- Collision detection toepassen met Colliders en Triggers
- Raycasts gebruiken voor collision checks
- Items verzamelen met triggers

---

## Deel 1: Unity Input (15 min)

### Legacy Input Manager

De simpelste manier om input te lezen:

```csharp
void Update()
{
    // Horizontale as (-1 tot 1)
    float horizontal = Input.GetAxis("Horizontal");

    // Verticale as (-1 tot 1)
    float vertical = Input.GetAxis("Vertical");

    // Specifieke toets ingedrukt
    if (Input.GetKeyDown(KeyCode.Space))
    {
        Jump();
    }

    // Toets ingehouden
    if (Input.GetKey(KeyCode.LeftShift))
    {
        Run();
    }

    // Toets losgelaten
    if (Input.GetKeyUp(KeyCode.Space))
    {
        EndJump();
    }
}
```

### Input Methodes

| Methode            | Wanneer True                        |
| ------------------ | ----------------------------------- |
| `GetKeyDown(key)`  | Frame waarin toets ingedrukt wordt  |
| `GetKey(key)`      | Elke frame dat toets ingehouden is  |
| `GetKeyUp(key)`    | Frame waarin toets losgelaten wordt |
| `GetAxis(name)`    | Geeft float -1 tot 1 (smooth)       |
| `GetAxisRaw(name)` | Geeft -1, 0, of 1 (geen smoothing)  |

### Grid-Based Input

Voor Pac-Man wil je vaak één richting tegelijk:

```csharp
Vector2 GetInputDirection()
{
    // Prioriteit: laatst ingedrukte richting
    if (Input.GetKeyDown(KeyCode.W) || Input.GetKeyDown(KeyCode.UpArrow))
        return Vector2.up;
    if (Input.GetKeyDown(KeyCode.S) || Input.GetKeyDown(KeyCode.DownArrow))
        return Vector2.down;
    if (Input.GetKeyDown(KeyCode.A) || Input.GetKeyDown(KeyCode.LeftArrow))
        return Vector2.left;
    if (Input.GetKeyDown(KeyCode.D) || Input.GetKeyDown(KeyCode.RightArrow))
        return Vector2.right;

    return Vector2.zero;
}
```

---

## Deel 2: Manieren om GameObjects te Bewegen (15 min)

Er zijn verschillende manieren om een GameObject te verplaatsen in Unity. Elke methode heeft voor- en nadelen.

### Methode 1: Transform.position direct aanpassen

```csharp
// Absolute positie instellen
transform.position = new Vector3(5, 0, 0);

// Relatief verplaatsen met +=
transform.position += new Vector3(1, 0, 0);

// Met Vector2 (2D games)
transform.position += (Vector3)direction * speed * Time.deltaTime;
```

**Voordelen:** Simpel, direct, volledige controle
**Nadelen:** Negeert physics/colliders, kan door muren gaan

### Methode 2: Transform.Translate()

```csharp
// Beweeg relatief aan huidige positie
transform.Translate(Vector3.right * speed * Time.deltaTime);

// In world space (onafhankelijk van rotatie)
transform.Translate(Vector3.right * speed * Time.deltaTime, Space.World);

// In local space (relatief aan object rotatie) - dit is de default
transform.Translate(Vector3.forward * speed * Time.deltaTime, Space.Self);
```

**Voordelen:** Handige shortcut, kan kiezen tussen local/world space
**Nadelen:** Negeert ook physics, zelfde probleem als position +=

### Methode 3: Rigidbody2D.MovePosition()

```csharp
private Rigidbody2D rb;

void Start()
{
    rb = GetComponent<Rigidbody2D>();
}

void FixedUpdate()  // Let op: FixedUpdate voor physics!
{
    Vector2 newPosition = rb.position + direction * speed * Time.fixedDeltaTime;
    rb.MovePosition(newPosition);
}
```

**Voordelen:** Respecteert physics, smooth interpolatie
**Nadelen:** Moet in FixedUpdate, iets complexer

### Methode 4: Rigidbody2D.velocity

```csharp
void FixedUpdate()
{
    rb.velocity = direction * speed;
}
```

**Voordelen:** Physics-based, automatische collision
**Nadelen:** Kan "glijden" voelen, minder directe controle

### Methode 5: Vector3.MoveTowards()

```csharp
public Vector3 targetPosition;
public float speed = 5f;

void Update()
{
    transform.position = Vector3.MoveTowards(
        transform.position,    // Huidige positie
        targetPosition,        // Doel positie
        speed * Time.deltaTime // Max afstand per frame
    );
}
```

**Voordelen:** Smooth beweging naar doel, stopt precies op doel
**Nadelen:** Negeert physics

### Vergelijkingstabel

| Methode          | Physics? | Collision? | Gebruik voor               |
| ---------------- | -------- | ---------- | -------------------------- |
| `position +=`    | Nee      | Nee        | Simpele prototypes, UI     |
| `Translate()`    | Nee      | Nee        | Simpele beweging, camera   |
| `MovePosition()` | Ja       | Ja         | Grid movement, platforms   |
| `velocity`       | Ja       | Ja         | Platformers, physics games |
| `MoveTowards()`  | Nee      | Nee        | Smooth naar doel bewegen   |

### Welke kies je voor Pac-Man?

Voor een grid-based game zoals Pac-Man zijn er twee goede opties:

**Optie A: `transform.position` + Raycast**

```csharp
// Check eerst of beweging mogelijk is met raycast
if (!IsBlocked(direction))
{
    transform.position += (Vector3)direction * speed * Time.deltaTime;
}
```

→ Simpel, maar je moet zelf collision checken

**Optie B: `Rigidbody2D.MovePosition()`**

```csharp
// Physics handelt collision af
Vector2 newPos = rb.position + direction * speed * Time.fixedDeltaTime;
rb.MovePosition(newPos);
```

→ Physics doet collision, maar moet in FixedUpdate

---

## Deel 3: Grid-Based Movement (20 min)

### Optie B: Continuous Movement (Pac-Man Stijl)

Karakter blijft bewegen in huidige richting:

```csharp
public class PacManMovement : MonoBehaviour
{
    public float moveSpeed = 5f;

    private Vector2 currentDirection = Vector2.zero;
    private Vector2 nextDirection = Vector2.zero;

    void Update()
    {
        HandleInput();
        TryChangeDirection();
        Move();
    }

    void HandleInput()
    {
        // Buffer de gewenste richting
        if (Input.GetKeyDown(KeyCode.W)) nextDirection = Vector2.up;
        if (Input.GetKeyDown(KeyCode.S)) nextDirection = Vector2.down;
        if (Input.GetKeyDown(KeyCode.A)) nextDirection = Vector2.left;
        if (Input.GetKeyDown(KeyCode.D)) nextDirection = Vector2.right;
    }

    void TryChangeDirection()
    {
        // Probeer van richting te veranderen als mogelijk
        if (nextDirection != Vector2.zero && CanMove(nextDirection))
        {
            currentDirection = nextDirection;
        }
    }

    void Move()
    {
        if (currentDirection == Vector2.zero) return;
        if (!CanMove(currentDirection)) return;

        transform.position += (Vector3)currentDirection * moveSpeed * Time.deltaTime;
    }

    bool CanMove(Vector2 direction)
    {
        // Raycast check
        RaycastHit2D hit = Physics2D.Raycast(
            transform.position,
            direction,
            0.6f
        );
        return hit.collider == null;
    }
}
```

---

## Deel 4: Collision Detection (15 min)

### Colliders vs Triggers

| Type         | Gedrag                            | Gebruik            |
| ------------ | --------------------------------- | ------------------ |
| **Collider** | Blokkeert beweging                | Muren, obstakels   |
| **Trigger**  | Detecteert overlap, geen blokkade | Items, checkpoints |

### Collider Setup

1. Voeg `BoxCollider2D` of `CircleCollider2D` toe
2. **Is Trigger** uit = fysieke blokkade
3. Zorg voor `Rigidbody2D` op bewegende objecten

### Trigger Events

```csharp
public class Player : MonoBehaviour
{
    // Iets komt trigger binnen
    void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Dot"))
        {
            CollectDot(other.gameObject);
        }
    }

    // Iets verlaat trigger
    void OnTriggerExit2D(Collider2D other)
    {
        Debug.Log("Verlaten: " + other.name);
    }

    // Iets blijft in trigger (elke frame)
    void OnTriggerStay2D(Collider2D other)
    {
        // Gebruik spaarzaam, wordt elk frame aangeroepen
    }
}
```

### Collision Events (voor fysieke botsingen)

```csharp
void OnCollisionEnter2D(Collision2D collision)
{
    if (collision.gameObject.CompareTag("Enemy"))
    {
        TakeDamage();
    }
}
```

---

## Deel 5: Raycasts (10 min)

### Raycast voor Collision Check

Een raycast schiet een onzichtbare lijn en detecteert wat het raakt:

```csharp
bool CanMoveInDirection(Vector2 direction)
{
    // Raycast vanaf speler positie
    RaycastHit2D hit = Physics2D.Raycast(
        transform.position,     // Start positie
        direction,              // Richting
        1f                      // Afstand
    );

    // hit.collider is null als niets geraakt
    return hit.collider == null;
}
```

### Layer Masks

Filter wat de raycast kan raken:

```csharp
public LayerMask wallLayer;

bool IsWallAhead(Vector2 direction)
{
    RaycastHit2D hit = Physics2D.Raycast(
        transform.position,
        direction,
        1f,
        wallLayer  // Alleen deze layer checken
    );

    return hit.collider != null;
}
```

### Debug Visualisatie

```csharp
void Update()
{
    Vector2 direction = Vector2.right;
    float distance = 1f;

    // Teken lijn in Scene view
    Debug.DrawRay(transform.position, direction * distance, Color.red);
}
```

---

## Oefeningen (60 min)

### Oefening 1: Basis Movement (15 min)

1. Maak een nieuwe scene met een speler sprite
2. Voeg een `Rigidbody2D` toe (Gravity Scale = 0)
3. Maak een `PlayerMovement` script met:
   - WASD input
   - Beweging in 4 richtingen
4. Test de movement

**Verwacht gedrag:**

```
        [W]
         ▲
         │
[A] ◄── ● ──► [D]
         │
         ▼
        [S]

Bij indrukken W: speler beweegt omhoog
Bij indrukken S: speler beweegt omlaag
Bij indrukken A: speler beweegt naar links
Bij indrukken D: speler beweegt naar rechts
```

**Console output (optioneel voor debugging):**

```
Moving: (0, 1)    // W ingedrukt
Moving: (-1, 0)   // A ingedrukt
Moving: (0, -1)   // S ingedrukt
Moving: (1, 0)    // D ingedrukt
```

### Oefening 2: Grid Movement (20 min)

1. Gebruik het `GridMovement` script uit Deel 2
2. Pas aan zodat de speler:
   - Smooth van tile naar tile beweegt
   - Alleen kan bewegen als vorige beweging klaar is
3. Voeg muren toe (sprites met `BoxCollider2D`)
4. Implementeer `IsBlocked()` met een Raycast

**Verwacht gedrag:**

```
Frame 1:  ● op positie (0, 0)
Frame 10: ● halverwege naar (1, 0)  [smooth beweging]
Frame 20: ● op positie (1, 0)       [aangekomen]
Frame 21: Nieuwe input mogelijk

Bij muur:
 ● → ■   Speler probeert naar rechts
 ●   ■   Raycast detecteert muur, beweging geblokkeerd
```

**Console output:**

```
Moving to: (1, 0)
Arrived at: (1, 0)
Moving to: (2, 0)
Blocked! Wall detected at (3, 0)
```

### Oefening 3: Collectibles (25 min)

1. Maak een `Dot` prefab:
   - Kleine sprite
   - `CircleCollider2D` met **Is Trigger = true**
   - Tag: "Dot"

2. Maak een `Collectible` script:

   ```csharp
   public class Collectible : MonoBehaviour
   {
       public int points = 10;

       public void Collect()
       {
           // Voeg punten toe (later met GameManager)
           Debug.Log("Collected! +" + points);
           Destroy(gameObject);
       }
   }
   ```

3. In je `Player` script:
   - Detecteer trigger collision met dots
   - Roep `Collect()` aan op de dot

4. Test met meerdere dots

**Verwacht gedrag:**

```
Voor:    ● ● ● ● ●    (5 dots)
         P →          (speler beweegt naar rechts)

Tijdens: ● ● ● ●      (4 dots, 1 opgegeten)
           P →

Na:      ● ● ●        (3 dots)
             P →
```

**Console output:**

```
Collected! +10
Collected! +10
Collected! +10
Total dots remaining: 2
```

**Bonus Challenges:**

- Voeg een `PowerPellet` toe met 50 punten
- Speel een geluidje af bij collecten
- Maak de dot groter worden voordat hij verdwijnt

---

## Samenvatting

| Concept                | Gebruik                         |
| ---------------------- | ------------------------------- |
| `Input.GetAxis()`      | Smooth input waarde (-1 tot 1)  |
| `Input.GetKeyDown()`   | Detecteer toets indrukken       |
| `Physics2D.Raycast()`  | Check collision in een richting |
| `OnTriggerEnter2D()`   | Detecteer overlap met trigger   |
| `OnCollisionEnter2D()` | Detecteer fysieke botsing       |
| `CompareTag()`         | Check object tag                |
| `Destroy()`            | Verwijder GameObject            |

### Quick Reference

```csharp
// Raycast check
RaycastHit2D hit = Physics2D.Raycast(position, direction, distance);
if (hit.collider != null) { /* Iets geraakt */ }

// Trigger detection
void OnTriggerEnter2D(Collider2D other)
{
    if (other.CompareTag("Item"))
    {
        Destroy(other.gameObject);
    }
}
```

---

## Volgende Les

In **Les 3.2** gaan we verder met het Game Design Document!
