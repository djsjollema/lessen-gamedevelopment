# Les 4.2: Botsingen Afvangen met Code

## Wat Ga Je Leren?

In deze les leer je hoe je met code kunt reageren op botsingen en trigger events. Je gaat:

- OnTriggerEnter() gebruiken om trigger contact te detecteren
- OnCollisionEnter() gebruiken om echte botsingen af te vangen
- Praktische game systemen bouwen (pickup, checkpoint, damage)
- Het verschil begrijpen tussen triggers en physics collisions
- Functies uit Les 3.2 toepassen in collision systemen
- Debuggen in collisions

---

## Trigger Detection in Code

### OnTriggerEnter() - Eerste Contact

In Les 4.1 heb je geleerd hoe je triggers instelt. Nu gaan we er met code op reageren!

```csharp
public class TriggerDetector : MonoBehaviour
{
    void OnTriggerEnter(Collider other)
    {
        Debug.Log("Iets is de trigger binnen gekomen!");
        Debug.Log("Object naam: " + other.gameObject.name);
    }
}
```

**Wat gebeurt er:**

- `OnTriggerEnter()` wordt aangeroepen zodra iets de trigger **binnenkomt**
- `Collider other` = de collider van het object dat de trigger binnenkomt
- `other.gameObject` = het GameObject dat contact maakt

**💡 Herinnering uit Les 4.1:** Voor triggers heb je nodig:

- Eén object met Rigidbody (mag Kinematic zijn)
- Eén object met Collider waar "Is Trigger" aanstaat

### Tags Controleren in Triggers

Zoals je in Les 4.1 hebt geleerd, gebruik je tags om objecten te identificeren:

```csharp
public class SmartTrigger : MonoBehaviour
{
    void OnTriggerEnter(Collider other)
    {
        // Check of het de Player is
        if (other.gameObject.CompareTag("Player"))
        {
            Debug.Log("Player entered the trigger!");
            // Doe iets speciaals voor de player
        }

        // Check of het een Enemy is
        if (other.gameObject.CompareTag("Enemy"))
        {
            Debug.Log("Enemy detected!");
            // Reageer op vijanden
        }

        // Check of het een Pickup is
        if (other.gameObject.CompareTag("Pickup"))
        {
            Debug.Log("Pickup found!");
            // Verzamel het item
        }
    }
}
```

### Alle Trigger Events

```csharp
public class CompleteTrigger : MonoBehaviour
{
    void OnTriggerEnter(Collider other)
    {
        Debug.Log(other.name + " kwam de trigger binnen");
    }

    void OnTriggerStay(Collider other)
    {
        Debug.Log(other.name + " blijft in de trigger");
    }

    void OnTriggerExit(Collider other)
    {
        Debug.Log(other.name + " verliet de trigger");
    }
}
```

**Wanneer gebruiken:**

- **OnTriggerEnter**: Eenmalige acties (pickup verzamelen, checkpoint)
- **OnTriggerStay**: Continue acties (healing zone, damage over time)
- **OnTriggerExit**: Cleanup acties (leave area, stop effect)

---

## Collision Detection - Echte Physics Botsingen

### OnCollisionEnter() - Physics Contact

Terwijl triggers **door elkaar heen** gaan, detecteert `OnCollisionEnter()` **echte physics botsingen** waar objecten daadwerkelijk tegen elkaar botsen.

```csharp
public class CollisionDetector : MonoBehaviour
{
    void OnCollisionEnter(Collision collision)
    {
        Debug.Log("Ik ben tegen iets gebotst!");
        Debug.Log("Gebotst tegen: " + collision.gameObject.name);
    }
}
```

**Verschil met Triggers:**

- **Trigger**: Objecten gaan door elkaar heen, maar je detecteert contact
- **Collision**: Objecten botsen echt tegen elkaar en stoppen

### Collision Events

```csharp
public class CollisionHandler : MonoBehaviour
{
    void OnCollisionEnter(Collision collision)
    {
        Debug.Log("Botsing gestart met: " + collision.gameObject.name);
    }

    void OnCollisionStay(Collision collision)
    {
        Debug.Log("Nog steeds in contact met: " + collision.gameObject.name);
    }

    void OnCollisionExit(Collision collision)
    {
        Debug.Log("Contact verloren met: " + collision.gameObject.name);
    }
}
```

### Collision vs Trigger - Wanneer Wat Gebruiken?

**Gebruik Triggers voor:**

- Pickup items
- Checkpoints
- Detectie zones
- Invisible triggers

**Gebruik Collisions voor:**

- Muren die je tegenhoudt
- Platforms waar je op loopt
- Objecten die van elkaar af stuiteren
- Realistische physics interacties

---

## Praktische Voorbeelden

### 1. Pickup Item System (met Functies uit Les 3.2)

```csharp
public class PickupItem : MonoBehaviour
{
    public int pointValue = 10;
    public string itemName = "Coin";

    void Start()
    {
        // Zorg dat dit object een trigger is
        GetComponent<Collider>().isTrigger = true;
    }

    void OnTriggerEnter(Collider other)
    {
        // Alleen de player kan items oppakken
        if (other.gameObject.CompareTag("Player"))
        {
            // Gebruik functie om punten toe te voegen (Les 3.2!)
            AddPointsToPlayer(pointValue);

            // Gebruik functie om pickup effect te tonen
            ShowPickupEffect();

            // Vernietig het pickup item
            Destroy(gameObject);
        }
    }

    // Functie om punten toe te voegen (Les 3.2 kennis!)
    void AddPointsToPlayer(int points)
    {
        Debug.Log("Player picked up: " + itemName);
        Debug.Log("Points gained: " + points);

        // Hier zou je later de score kunnen bijwerken
        // PlayerScript.Instance.AddScore(points);
    }

    // Functie om visueel effect te tonen
    void ShowPickupEffect()
    {
        Debug.Log("✨ Pickup effect! ✨");
        // Hier zou je later een particle effect kunnen spelen
    }
}
```

### 2. Checkpoint System

```csharp
public class Checkpoint : MonoBehaviour
{
    public Vector3 respawnPosition;
    private bool isActivated = false;

    void Start()
    {
        respawnPosition = transform.position;
        GetComponent<Collider>().isTrigger = true;
    }

    void OnTriggerEnter(Collider other)
    {
        if (other.gameObject.CompareTag("Player") && !isActivated)
        {
            ActivateCheckpoint();
        }
    }

    // Functie om checkpoint te activeren (Les 3.2 organisatie!)
    void ActivateCheckpoint()
    {
        isActivated = true;
        Debug.Log("Checkpoint activated!");

        // Verander kleur naar groen
        ChangeColor(Color.green);
    }

    // Herbruikbare functie voor kleur veranderen
    void ChangeColor(Color newColor)
    {
        Renderer renderer = GetComponent<Renderer>();
        if (renderer != null)
        {
            renderer.material.color = newColor;
        }
    }
}
```

### 3. Damage Zone (met OnTriggerStay)

```csharp
public class DamageZone : MonoBehaviour
{
    public int damagePerSecond = 10;
    private float damageTimer = 0f;

    void Start()
    {
        GetComponent<Collider>().isTrigger = true;
        SetDangerAppearance();
    }

    void OnTriggerEnter(Collider other)
    {
        if (other.gameObject.CompareTag("Player"))
        {
            Debug.Log("Player entered danger zone!");
        }
    }

    void OnTriggerStay(Collider other)
    {
        if (other.gameObject.CompareTag("Player"))
        {
            // Damage over time
            damageTimer += Time.deltaTime;

            if (damageTimer >= 1.0f) // Elke seconde damage
            {
                ApplyDamage(other.gameObject, damagePerSecond);
                damageTimer = 0f;
            }
        }
    }

    void OnTriggerExit(Collider other)
    {
        if (other.gameObject.CompareTag("Player"))
        {
            Debug.Log("Player left danger zone - safe now!");
            damageTimer = 0f; // Reset timer
        }
    }

    // Functie voor damage toepassen
    void ApplyDamage(GameObject target, int damage)
    {
        Debug.Log("Player takes " + damage + " damage!");
        // Hier zou je later PlayerHealth kunnen verminderen
    }

    // Functie voor danger zone uiterlijk
    void SetDangerAppearance()
    {
        Renderer renderer = GetComponent<Renderer>();
        if (renderer != null)
        {
            renderer.material.color = new Color(1f, 0f, 0f, 0.5f); // Rood, half transparant
        }
    }
}
```

### 4. Auto Door System (met Physics)

```csharp
public class AutoDoor : MonoBehaviour
{
    public float openSpeed = 2.0f;
    private Vector3 closedPosition;
    private Vector3 openPosition;
    private bool isPlayerNear = false;

    void Start()
    {
        closedPosition = transform.position;
        openPosition = closedPosition + Vector3.up * 3.0f; // 3 units omhoog

        GetComponent<Collider>().isTrigger = true;
    }

    void Update()
    {
        MoveDoor();
    }

    void OnTriggerEnter(Collider other)
    {
        if (other.gameObject.CompareTag("Player"))
        {
            OpenDoor();
        }
    }

    void OnTriggerExit(Collider other)
    {
        if (other.gameObject.CompareTag("Player"))
        {
            CloseDoor();
        }
    }

    // Functie om deur te openen
    void OpenDoor()
    {
        isPlayerNear = true;
        Debug.Log("Door opening...");
    }

    // Functie om deur te sluiten
    void CloseDoor()
    {
        isPlayerNear = false;
        Debug.Log("Door closing...");
    }

    // Functie om deur te bewegen (gebruikt Les 2.1 kennis!)
    void MoveDoor()
    {
        Vector3 targetPosition;
        if(isPlayerNear)
        {
            targetPosition = openPosition;
        }
        else
        {
            targetPosition = closedPosition;
        }
        transform.position = Vector3.MoveTowards(transform.position, targetPosition, openSpeed * Time.deltaTime);
    }
}
```

### 5. Bouncing Ball (Physics Collision)

```csharp
public class BouncingBall : MonoBehaviour
{
    public float bounceForce = 10f;
    private Rigidbody rb;

    void Start()
    {
        rb = GetComponent<Rigidbody>();

        // Zorg dat dit GEEN trigger is - we willen echte physics
        GetComponent<Collider>().isTrigger = false;
    }

    void OnCollisionEnter(Collision collision)
    {
        // Check wat we raken
        if (collision.gameObject.CompareTag("Ground"))
        {
            BounceBall(collision);
        }
        else if (collision.gameObject.CompareTag("Wall"))
        {
            HandleWallBounce(collision);
        }
    }

    // Functie om bal te laten stuiteren
    void BounceBall(Collision collision)
    {
        Vector3 bounceDirection = collision.contacts[0].normal;
        rb.AddForce(-bounceDirection * bounceForce, ForceMode.Impulse);

        Debug.Log("Ball bounced!");
    }

    // Functie om muur botsing af te handelen
    void HandleWallBounce(Collision collision)
    {
        Debug.Log("Hit wall!");
        // Hier kun je special wall bounce logic toevoegen
    }
}
```

---

## Combineer Input met Collisions (Les 2.2 + 4.2)

### Player Controller met Collision Detection

```csharp
public class PlayerController : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float jumpForce = 10f;
    private Rigidbody rb;
    private bool isGrounded = false;

    void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    void Update()
    {
        HandleMovement(); // Les 2.2 input kennis
        HandleJumping();
    }

    // Beweging met input (Les 2.2)
    void HandleMovement()
    {
        float horizontal = Input.GetAxis("Horizontal");
        float vertical = Input.GetAxis("Vertical");

        Vector3 movement = new Vector3(horizontal, 0, vertical);
        rb.AddForce(movement * moveSpeed);
    }

    // Springen met collision check
    void HandleJumping()
    {
        if (Input.GetKeyDown(KeyCode.Space) && isGrounded)
        {
            Jump();
        }
    }

    // Collision detection voor grond check
    void OnCollisionEnter(Collision collision)
    {
        if (collision.gameObject.CompareTag("Ground"))
        {
            isGrounded = true;
            Debug.Log("Player landed!");
        }
    }

    void OnCollisionExit(Collision collision)
    {
        if (collision.gameObject.CompareTag("Ground"))
        {
            isGrounded = false;
            Debug.Log("Player left ground!");
        }
    }

    // Jump functie (Les 3.2 organisatie)
    void Jump()
    {
        rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
        Debug.Log("Player jumped!");
    }
}
```

---

## Tag Comparison Best Practices

### CompareTag() - De Betere Methode (Herhaling Les 4.1)

```csharp
// ✅ Goed - gebruikt CompareTag()
if (other.gameObject.CompareTag("Player"))
{
    Debug.Log("Player detected!");
}

// ❌ Minder goed - string vergelijking
if (other.gameObject.tag == "Player")
{
    Debug.Log("Player detected!");
}
```

---

## Debugging Collisions en Triggers

### Debug Script

```csharp
public class CollisionDebugger : MonoBehaviour
{
    void OnTriggerEnter(Collider other)
    {
        LogTriggerInfo("TRIGGER ENTER", other);
    }

    void OnTriggerExit(Collider other)
    {
        LogTriggerInfo("TRIGGER EXIT", other);
    }

    void OnCollisionEnter(Collision collision)
    {
        LogCollisionInfo("COLLISION ENTER", collision);
    }

    void OnCollisionExit(Collision collision)
    {
        LogCollisionInfo("COLLISION EXIT", collision);
    }

    // Functie voor trigger debug info
    void LogTriggerInfo(string eventType, Collider other)
    {
        Debug.Log("=== " + eventType + " ===");
        Debug.Log("This object: " + gameObject.name);
        Debug.Log("Other object: " + other.gameObject.name);
        Debug.Log("Other tag: " + other.gameObject.tag);
        Debug.Log("Has Rigidbody: " + (other.GetComponent<Rigidbody>() != null));
    }

    // Functie voor collision debug info
    void LogCollisionInfo(string eventType, Collision collision)
    {
        Debug.Log("=== " + eventType + " ===");
        Debug.Log("This object: " + gameObject.name);
        Debug.Log("Other object: " + collision.gameObject.name);
        Debug.Log("Impact force: " + collision.relativeVelocity.magnitude);
    }
}
```

### Veelvoorkomende Problemen en Oplossingen

**❌ OnTriggerEnter werkt niet:**

```csharp
// Checklist functie
void CheckTriggerSetup()
{
    Debug.Log("=== TRIGGER SETUP CHECK ===");

    Collider col = GetComponent<Collider>();
    Debug.Log("Has Collider: " + (col != null));
    Debug.Log("Is Trigger: " + (col != null ? col.isTrigger : false));

    Rigidbody rb = GetComponent<Rigidbody>();
    Debug.Log("Has Rigidbody: " + (rb != null));

    Debug.Log("GameObject active: " + gameObject.activeInHierarchy);
}
```

**❌ OnCollisionEnter werkt niet:**

```csharp
// Checklist functie voor collisions
void CheckCollisionSetup()
{
    Debug.Log("=== COLLISION SETUP CHECK ===");

    Collider col = GetComponent<Collider>();
    Debug.Log("Has Collider: " + (col != null));
    Debug.Log("Is NOT Trigger: " + (col != null ? !col.isTrigger : false));

    Rigidbody rb = GetComponent<Rigidbody>();
    Debug.Log("Has Rigidbody: " + (rb != null));
    Debug.Log("Is NOT Kinematic: " + (rb != null ? !rb.isKinematic : false));
}
```

---

## Aantekeningen maken

Maak aantekeningen over de behandelde stof in de les. Schrijf het nu zo op zodat je het later makkelijk begrijpt als je het terugleest.

**Belangrijke punten om te noteren:**

- Wat is het verschil tussen OnTriggerEnter() en OnCollisionEnter()?
- Wanneer gebruik je triggers en wanneer physics collisions?
- Hoe controleer je welk object contact maakt met je collider?
- Hoe gebruik je functies (Les 3.2) om je collision code te organiseren?
- Welke collision events zijn er (Enter, Stay, Exit)?
- Hoe debug je collision problemen?

Schrijf ook op wat je niet hebt begrepen uit deze les. Dan kun je hier later nog vragen over stellen aan de docent.

Bewaar al je aantekeningen goed! Deze moet je aan het einde van de periode inleveren.

![notes](https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExeHhzdzZzbHQzYWgyNG1mZDRhdW05dWIwMDI2b2xoNWtkMWN0ODl2dSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/3o7GUB9ExWUxjiSrKw/giphy.gif)

## Oefeningen uitvoeren

Doe nu minimaal 1 oefening naar keuze voor les 4.2
De oefeningen vind je [hier](../Oefeningen/oefeningen_4_2.md) terug

![exercise](https://media.giphy.com/media/v1.Y2lkPWVjZjA1ZTQ3ZXRrc3QwYWV1Ym5oY2FrZnF5YWxnaW9heTRsNnZzdnpnMmRxeXM1ZiZlcD12MV9naWZzX3JlbGF0ZWQmY3Q9Zw/x1BVziEYuKBd1aVZRz/giphy.gif)

## Wat Heb Je Geleerd?

### Checklist

- [ ] Je weet hoe je OnTriggerEnter(), OnTriggerStay() en OnTriggerExit() gebruikt
- [ ] Je begrijpt het verschil tussen triggers en physics collisions
- [ ] Je kunt OnCollisionEnter() gebruiken voor echte botsingen
- [ ] Je hebt praktische systemen gemaakt (pickup, checkpoint, damage zone)
- [ ] Je kunt collision events debuggen en problemen oplossen
- [ ] Je gebruikt functies (Les 3.2) om je code georganiseerd te houden
- [ ] Je combineert input (Les 2.2) met collision detection
- [ ] Je begrijpt wanneer je triggers vs collisions moet gebruiken

### Volgende Stap

In Les 5.1 gaan we leren over if-statements en switch statements! Dan kunnen we complexere logica maken en betere beslissingen nemen in onze code.

---

## Veelgestelde Vragen

### Q: Waarom wordt mijn OnTriggerEnter() niet aangeroepen?

**A:** Check deze punten:

- Is "Is Trigger" aangevinkt op de Collider?
- Heeft één van de objecten een Rigidbody?
- Zijn beide objecten actief (niet disabled)?
- Staat het script op het juiste GameObject?

### Q: Wat is het verschil tussen Collision en Collider parameters?

**A:**

- **OnTriggerEnter(Collider other)**: Voor triggers, krijgt je de Collider van het andere object
- **OnCollisionEnter(Collision collision)**: Voor physics botsingen, krijgt je uitgebreide collision informatie

### Q: Kan ik zowel triggers als collisions op hetzelfde object hebben?

**A:** Ja, maar niet met dezelfde Collider. Je kunt meerdere Colliders toevoegen - één als trigger, één voor physics.

### Q: Wanneer gebruik ik OnTriggerStay vs OnCollisionStay?

**A:**

- **OnTriggerStay**: Voor continue effecten (healing zone, damage over time)
- **OnCollisionStay**: Minder vaak gebruikt, voor wanneer objecten tegen elkaar gedrukt blijven

### Q: Mijn collision detection werkt niet betrouwbaar?

**A:** Dit komt vaak door:

- Te snelle beweging (objecten "teleporteren" door colliders heen)
- Verkeerde Collision Detection setting op Rigidbody
- Te kleine colliders voor de snelheid van beweging

### Q: Hoe stop ik een object dat door collision systemen heen gaat?

**A:** Zet Collision Detection op de Rigidbody van "Discrete" naar "Continuous" voor betere high-speed collision detection.

---
