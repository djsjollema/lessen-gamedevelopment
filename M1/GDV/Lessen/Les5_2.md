# Les 5.2: Logica Combineren met Botsingen en Input

## Wat Ga Je Leren?

In deze les combineer je eenvoudige logica met collision detection en input. Je gaat:

- If-statements gebruiken bij collision detection (Les 4.2 + 5.1)
- Input controleren met logische voorwaarden (Les 2.2 + 5.1)
- Eenvoudige interaction systemen maken
- Alles wat je hebt geleerd samenvoegen

---

## Herinnering: Wat Heb Je Al Geleerd?

**Les 2.2:** Input verwerken

```csharp
if (Input.GetKeyDown(KeyCode.Space))
{
    Debug.Log("Space pressed!");
}
```

**Les 4.2:** Collision detection

```csharp
void OnTriggerEnter(Collider other)
{
    if (other.CompareTag("Player"))
    {
        Debug.Log("Player touched me!");
    }
}
```

**Les 5.1:** If-statements en logica

```csharp
if (health > 0 && hasKey)
{
    Debug.Log("Player is alive AND has key!");
}
```

**Nu gaan we deze combineren!**

---

## Input met Voorwaarden

### Alleen Reageren Wanneer Het Mag

In Les 2.2 reageerde je altijd op input. Nu gaan we **slimmer** zijn:

```csharp
public class SmartPlayer : MonoBehaviour
{
    public int health = 100;
    public bool hasKey = false;

    void Update()
    {
        // Normale input uit Les 2.2
        if (Input.GetKeyDown(KeyCode.Space))
        {
            Jump(); // Altijd springen
        }

        // NIEUWE manier - springen met voorwaarden!
        if (Input.GetKeyDown(KeyCode.Space) && health > 0)
        {
            Jump(); // Alleen springen als je leeft
        }

        // Gebruik sleutel alleen als je er een hebt
        if (Input.GetKeyDown(KeyCode.E) && hasKey)
        {
            UseKey(); // Uit Les 3.2: functies maken
        }
    }

    void Jump() // Functie uit Les 3.2
    {
        Debug.Log("Player jumped!");
    }

    void UseKey() // Functie uit Les 3.2
    {
        Debug.Log("Key used!");
        hasKey = false; // Sleutel is op
    }
}
```

**Wat is er nieuw?**

- **Les 2.2**: `if (Input.GetKeyDown(KeyCode.Space))`
- **Les 5.1**: `&& health > 0` (EN operator)
- **Combinatie**: `if (Input.GetKeyDown(KeyCode.Space) && health > 0)`

### Meerdere Voorwaarden

```csharp
public class PlayerMovement : MonoBehaviour
{
    public float speed = 5f;
    public bool canMove = true;
    public bool isAlive = true;

    void Update()
    {
        // Beweging uit Les 2.1, maar nu met voorwaarden uit Les 5.1
        if (canMove && isAlive) // Beide moeten waar zijn
        {
            // WASD beweging uit Les 2.2
            if (Input.GetKey(KeyCode.W))
            {
                transform.position += Vector3.up * speed * Time.deltaTime;
            }

            if (Input.GetKey(KeyCode.S))
            {
                transform.position += Vector3.down * speed * Time.deltaTime;
            }
        }

        // Reset knop - werkt altijd
        if (Input.GetKeyDown(KeyCode.R))
        {
            ResetPlayer();
        }
    }

    void ResetPlayer()
    {
        transform.position = Vector3.zero; // Terug naar 0,0,0
        isAlive = true;
        canMove = true;
        Debug.Log("Player reset!");
    }
}
```

---

## Collision Detection met Logica

### Slimme Pickup Items

In Les 4.2 pakte je alles op. Nu worden we selectief:

```csharp
public class SmartPickup : MonoBehaviour
{
    public enum ItemType { Coin, HealthPotion, Key } // Uit Les 5.1: verschillende opties
    public ItemType itemType = ItemType.Coin;
    public int value = 10;

    void Start()
    {
        GetComponent<Collider>().isTrigger = true; // Les 4.1: trigger maken
    }

    void OnTriggerEnter(Collider other) // Les 4.2: collision detection
    {
        if (other.CompareTag("Player")) // Les 4.1: tag checking
        {
            SmartPlayer player = other.GetComponent<SmartPlayer>();

            // Switch uit Les 5.1 + collision uit Les 4.2
            switch (itemType)
            {
                case ItemType.Coin:
                    Debug.Log("Coin collected!");
                    Destroy(gameObject);
                    break;

                case ItemType.HealthPotion:
                    // Alleen oppakken als je schade hebt
                    if (player.health < 100)
                    {
                        player.health += value;
                        Debug.Log("Health restored!");
                        Destroy(gameObject);
                    }
                    else
                    {
                        Debug.Log("Health already full!");
                    }
                    break;

                case ItemType.Key:
                    if (!player.hasKey) // Als je nog geen sleutel hebt
                    {
                        player.hasKey = true;
                        Debug.Log("Key found!");
                        Destroy(gameObject);
                    }
                    break;
            }
        }
    }
}
```

### Interactieve Deur

```csharp
public class SimpleDoor : MonoBehaviour
{
    public bool needsKey = true;
    public bool isOpen = false;

    private bool playerNearby = false; // Bijhouden of speler dichtbij is

    void Start()
    {
        GetComponent<Collider>().isTrigger = true; // Les 4.1
    }

    void Update()
    {
        // Input uit Les 2.2 + logica uit Les 5.1
        if (playerNearby && Input.GetKeyDown(KeyCode.E))
        {
            TryOpenDoor(); // Functie uit Les 3.2
        }
    }

    void OnTriggerEnter(Collider other) // Les 4.2
    {
        if (other.CompareTag("Player"))
        {
            playerNearby = true;
            ShowHint(); // Functie uit Les 3.2
        }
    }

    void OnTriggerExit(Collider other) // Les 4.2
    {
        if (other.CompareTag("Player"))
        {
            playerNearby = false;
            Debug.Log(""); // Clear hint
        }
    }

    void TryOpenDoor() // Functie uit Les 3.2
    {
        SmartPlayer player = GameObject.FindWithTag("Player").GetComponent<SmartPlayer>();

        // If-else uit Les 5.1
        if (needsKey)
        {
            if (player.hasKey) // Heeft speler een sleutel?
            {
                OpenDoor();
                player.hasKey = false; // Sleutel gebruiken
            }
            else
            {
                Debug.Log("Need a key!");
            }
        }
        else
        {
            OpenDoor(); // Geen sleutel nodig
        }
    }

    void OpenDoor()
    {
        isOpen = true;
        Debug.Log("Door opened!");

        // Simpele beweging uit Les 2.1
        transform.position += Vector3.up * 3f;
    }

    void ShowHint()
    {
        if (needsKey)
        {
            Debug.Log("Press E to open (needs key)");
        }
        else
        {
            Debug.Log("Press E to open");
        }
    }
}
```

---

## Eenvoudig Game State System

### Game Manager (Versimpeld)

```csharp
public class SimpleGameManager : MonoBehaviour
{
    // Enum uit Les 5.1 - verschillende game states
    public enum GameState { Playing, Paused, GameOver }
    public GameState currentState = GameState.Playing;

    public int score = 0;
    public int lives = 3;

    void Update()
    {
        // Switch uit Les 5.1 + Input uit Les 2.2
        switch (currentState)
        {
            case GameState.Playing:
                HandlePlayingInput();
                break;

            case GameState.Paused:
                HandlePausedInput();
                break;

            case GameState.GameOver:
                HandleGameOverInput();
                break;
        }
    }

    void HandlePlayingInput() // Functie uit Les 3.2
    {
        if (Input.GetKeyDown(KeyCode.Escape))
        {
            PauseGame();
        }
    }

    void HandlePausedInput()
    {
        if (Input.GetKeyDown(KeyCode.Escape))
        {
            ResumeGame();
        }
    }

    void HandleGameOverInput()
    {
        if (Input.GetKeyDown(KeyCode.R))
        {
            RestartGame();
        }
    }

    void PauseGame()
    {
        currentState = GameState.Paused;
        Time.timeScale = 0f; // Stop tijd
        Debug.Log("Game Paused - Press ESC to resume");
    }

    void ResumeGame()
    {
        currentState = GameState.Playing;
        Time.timeScale = 1f; // Normale tijd
        Debug.Log("Game Resumed");
    }

    void RestartGame()
    {
        currentState = GameState.Playing;
        Time.timeScale = 1f;
        score = 0;
        lives = 3;
        Debug.Log("Game Restarted");
    }

    public void AddScore(int points) // Public functie - andere scripts kunnen dit aanroepen
    {
        score += points;
        Debug.Log("Score: " + score);
    }

    public void LoseLife()
    {
        lives--;
        if (lives <= 0)
        {
            GameOver();
        }
        else
        {
            Debug.Log("Lives left: " + lives);
        }
    }

    void GameOver()
    {
        currentState = GameState.GameOver;
        Debug.Log("GAME OVER! Press R to restart");
    }
}
```

---

## Alles Combineren: Complete Player

```csharp
public class CompletePlayer : MonoBehaviour
{
    [Header("Player Stats")] // Netjes organiseren in Inspector
    public int health = 100;
    public int maxHealth = 100;
    public bool hasKey = false;

    [Header("Movement")] // Les 2.1 beweging
    public float speed = 5f;

    [Header("References")]
    public SimpleGameManager gameManager;

    void Start()
    {
        gameManager = FindObjectOfType<SimpleGameManager>(); // Zoek GameManager
    }

    void Update()
    {
        // Alleen bewegen als game speelt (Les 5.1 logica)
        if (gameManager.currentState == SimpleGameManager.GameState.Playing)
        {
            HandleMovement(); // Functie uit Les 3.2
        }
    }

    void HandleMovement() // Beweging uit Les 2.1 + 2.2
    {
        if (health > 0) // Alleen bewegen als je leeft
        {
            float horizontal = Input.GetAxis("Horizontal"); // Les 2.2
            float vertical = Input.GetAxis("Vertical");

            Vector3 movement = new Vector3(horizontal, vertical, 0);
            transform.position += movement * speed * Time.deltaTime; // Les 2.1
        }
    }

    void OnTriggerEnter(Collider other) // Les 4.2
    {
        // Switch uit Les 5.1 voor verschillende objecten
        switch (other.tag)
        {
            case "Coin":
                gameManager.AddScore(10);
                Destroy(other.gameObject);
                break;

            case "Enemy":
                TakeDamage(25);
                break;

            case "HealthPotion":
                if (health < maxHealth) // Alleen heal als nodig
                {
                    health += 30;
                    if (health > maxHealth) health = maxHealth;
                    Debug.Log("Healed! Health: " + health);
                    Destroy(other.gameObject);
                }
                break;
        }
    }

    public void TakeDamage(int damage) // Public - andere scripts kunnen dit aanroepen
    {
        health -= damage;
        Debug.Log("Took damage! Health: " + health);

        if (health <= 0)
        {
            Die();
        }
    }

    void Die()
    {
        Debug.Log("Player died!");
        gameManager.LoseLife();
    }
}
```

---

## Aantekeningen maken

Maak aantekeningen over de behandelde stof in de les. Schrijf het nu zo op zodat je het later makkelijk begrijpt als je het terugleest.

**Belangrijke punten om te noteren:**

- Hoe combineer je input (Les 2.2) met if-statements (Les 5.1)?
- Hoe gebruik je switch statements (Les 5.1) in collision detection (Les 4.2)?
- Hoe organiseer je je code met functies (Les 3.2)?
- Welke patronen zie je terugkomen in alle voorbeelden?

Schrijf ook op wat je niet hebt begrepen uit deze les. Dan kun je hier later nog vragen over stellen aan de docent.

Bewaar al je aantekeningen goed! Deze moet je aan het einde van de periode inleveren.

## Oefeningen uitvoeren

Doe nu minimaal 1 oefening naar keuze voor les 5.2
De oefeningen vind je [hier](../Oefeningen/oefeningen_5_2.md) terug

## Wat Heb Je Geleerd?

### Checklist

- [ ] Je kunt input (Les 2.2) combineren met if-statements (Les 5.1)
- [ ] Je gebruikt switch statements (Les 5.1) in collision detection (Les 4.2)
- [ ] Je organiseert code met functies (Les 3.2)
- [ ] Je maakt slimme pickup systemen
- [ ] Je bouwt interactieve deuren
- [ ] Je hebt een eenvoudig game state system gemaakt
- [ ] Je combineert alles in één complete player script

### Volgende Stap

In Les 6.1 gaan we lijsten en arrays leren! Dan kunnen we meerdere objecten tegelijk beheren.

---

## Veelgestelde Vragen

### Q: Hoe weet ik wanneer ik welke les technieken moet gebruiken?

**A:**

- **Les 2.2**: Voor basis input en beweging
- **Les 4.2**: Voor objecten die elkaar raken
- **Les 5.1**: Voor beslissingen en keuzes
- **Combineer ze**: Voor slimme, interactieve systemen

### Q: Mijn code wordt te ingewikkeld, wat nu?

**A:** Gebruik **functies** (Les 3.2)! Deel grote stukken code op in kleine, begrijpelijke functies.

### Q: Wanneer gebruik ik switch vs if-else?

**A:**

- **Switch**: Voor één variabele met veel mogelijke waarden (zoals game states of item types)
- **If-else**: Voor complexere voorwaarden met meerdere variabelen

### Q: Kan ik dit allemaal onthouden?

**A:** Hoeft niet! Het belangrijkste is dat je begrijpt HOE het werkt. Je kunt altijd terug kijken naar eerdere lessen voor voorbeelden.

---

        if (gameManager.currentState == GameManager.GameState.Playing)
        {
            HandleMovement();
            HandleActions();
        }
    }

    void HandleMovement()
    {
        // Beweging alleen als speler leeft
        if (health > 0)
        {
            float horizontal = Input.GetAxis("Horizontal");
            float vertical = Input.GetAxis("Vertical");

            Vector3 movement = new Vector3(horizontal, 0, vertical);
            rb.AddForce(movement * moveSpeed);

            // Springen alleen als op grond
            if (Input.GetKeyDown(KeyCode.Space) && isGrounded)
            {
                rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
                isGrounded = false;
            }
        }
    }

    void HandleActions()
    {
        // Actie knoppen
        if (Input.GetKeyDown(KeyCode.H) && health < maxHealth)
        {
            TryHeal();
        }
    }

    void TryHeal()
    {
        // Logica: alleen heal als je minder dan vol leven hebt
        if (health < maxHealth)
        {
            health += 25;
            if (health > maxHealth) health = maxHealth;

            Debug.Log("Healed! Health: " + health + "/" + maxHealth);
        }
    }

    public void TakeDamage(int damage)
    {
        health -= damage;
        Debug.Log("Took " + damage + " damage! Health: " + health);

        if (health <= 0)
        {
            Die();
        }
    }

    void Die()
    {
        Debug.Log("Player died!");
        gameManager.PlayerDied();
    }

    // Collision detection
    void OnCollisionEnter(Collision collision)
    {
        if (collision.gameObject.CompareTag("Ground"))
        {
            isGrounded = true;
        }

        if (collision.gameObject.CompareTag("Enemy"))
        {
            TakeDamage(20);
        }
    }

    // Trigger detection
    void OnTriggerEnter(Collider other)
    {
        switch (other.tag)
        {
            case "Coin":
                gameManager.CollectCoin();
                Destroy(other.gameObject);
                break;

            case "HealthPotion":
                if (health < maxHealth)
                {
                    health += 30;
                    if (health > maxHealth) health = maxHealth;
                    Debug.Log("Health potion used!");
                    Destroy(other.gameObject);
                }
                break;

            case "Key":
                hasKey = true;
                Debug.Log("Key acquired!");
                Destroy(other.gameObject);
                break;

            case "DamageZone":
                TakeDamage(10);
                break;
        }
    }

}

```

---

## Aantekeningen maken

Maak aantekeningen over de behandelde stof in de les. Schrijf het nu zo op zodat je het later makkelijk begrijpt als je het terugleest.

**Belangrijke punten om te noteren:**

- Hoe combineer je input met logische voorwaarden?
- Hoe gebruik je switch statements in collision detection?
- Wat is de rol van game state management?
- Hoe kun je complexe interacties maken door alles te combineren?
- Welke patronen zie je terugkomen in interactieve systemen?

Schrijf ook op wat je niet hebt begrepen uit deze les. Dan kun je hier later nog vragen over stellen aan de docent.

Bewaar al je aantekeningen goed! Deze moet je aan het einde van de periode inleveren.

## Oefeningen uitvoeren

Doe nu minimaal 1 oefening naar keuze voor les 5.2
De oefeningen vind je [hier](../Oefeningen/oefeningen_5_2.md) terug

## Wat Heb Je Geleerd?

### Checklist

- [ ] Je kunt input combineren met logische voorwaarden
- [ ] Je gebruikt switch statements effectief in collision detection
- [ ] Je begrijpt game state management met enums
- [ ] Je kunt complexe interactieve systemen bouwen
- [ ] Je integreert kennis uit alle vorige lessen
- [ ] Je maakt slimme pickup en door systemen
- [ ] Je bouwt een complete game manager
- [ ] Je combineert physics, logic en input in één systeem

### Volgende Stap

In Les 6.1 gaan we lijsten en arrays leren! Dan kunnen we meerdere objecten tegelijk beheren en nog complexere systemen maken.

---

## Veelgestelde Vragen

### Q: Hoe voorkom ik dat mijn code te complex wordt?

**A:** Gebruik functies (Les 3.2) om je code op te delen in kleine, begrijpelijke stukjes. Elke functie moet één duidelijke taak hebben.

### Q: Wanneer gebruik ik switch vs if-else?

**A:** Switch voor één variabele met veel mogelijke waarden (zoals game states). If-else voor complexere voorwaarden of combinaties van variabelen.

### Q: Mijn collision detection werkt niet goed met complexe logica?

**A:** Gebruik guard clauses (Les 5.1) om eerst te checken of collision überhaupt geldig is voordat je complexe logica uitvoert.

### Q: Hoe organiseer ik grote scripts?

**A:** Deel op in secties met comments en gebruik #region tags in C# om code secties inklapbaar te maken.

### Q: Kan ik meerdere GameManagers hebben?

**A:** Technisch wel, maar meestal wil je één centrale GameManager. Gebruik Singleton pattern voor complexere projecten.

---
