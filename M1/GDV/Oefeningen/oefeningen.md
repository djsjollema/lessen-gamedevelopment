# Oefeningen Overzicht

## Les 1.2 + 2.2 Combi Oefeningen

Deze oefeningen combineren de kennis uit **Les 1.2** (Debug.Log, comments, basisstructuur) en **Les 2.2** (variabelen, datatypes, input) in leuke 2D scenarios.

### Waarom Deze Oefeningen?

- **Beginner vriendelijk**: Te maken in 1 uur zonder voorkennis
- **2D focus**: Simpel om te visualiseren en testen
- **Opbouwend**: Elke oefening voegt iets nieuws toe
- **Praktisch**: Direct toepasbaar in echte games

---

## Oefening 1: 2D Character Stats Display ⭐

**Combinatie**: Debug.Log + Variabelen

**Tijd**: 15-20 minuten

### Wat Ga Je Maken?

Een simpel character sheet systeem dat je character stats toont in de console.

### Opdracht:

1. Maak een nieuw script: `CharacterStats`
2. Gebruik verschillende datatypes om character informatie op te slaan
3. Toon alles netjes in de console met Debug.Log

```csharp
public class CharacterStats : MonoBehaviour
{
    void Start()
    {
        // Character informatie variabelen
        string characterName = "Hero";
        int level = 5;
        int health = 100;
        int mana = 50;
        float experience = 75.5f;
        bool isAlive = true;

        // Toon character sheet in console
        Debug.Log("=== CHARACTER SHEET ===");
        Debug.Log("Name: " + characterName);
        Debug.Log("Level: " + level);
        Debug.Log("Health: " + health + "/100");
        Debug.Log("Mana: " + mana + "/100");
        Debug.Log("Experience: " + experience + "%");
        Debug.Log("Status: " + (isAlive ? "Alive" : "Dead"));
        Debug.Log("=======================");
    }
}
```

### Extra Uitdaging:

- Voeg meer stats toe (strength, defense, speed)
- Bereken total combat power (health + mana + level)
- Maak verschillende character types (Wizard, Warrior, Archer)

---

## Oefening 2: 2D Sprite Color Controller ⭐

**Combinatie**: Variabelen + Input + 2D Sprites

**Tijd**: 20-25 minuten

### Wat Ga Je Maken?

Een 2D sprite die van kleur verandert met toetsenbordinput.

### Setup:

1. Maak een **2D Sprite** (GameObject → 2D Object → Sprite)
2. Maak een nieuw script: `SpriteColorController`
3. Sleep het script op de Sprite

```csharp
public class SpriteColorController : MonoBehaviour
{
    // Sprite component reference
    private SpriteRenderer spriteRenderer;

    // Color info
    public string currentColor = "White";
    public int colorChanges = 0;

    void Start()
    {
        // Get the sprite renderer component
        spriteRenderer = GetComponent<SpriteRenderer>();

        Debug.Log("=== SPRITE COLOR CONTROLLER ===");
        Debug.Log("Start color: " + currentColor);
        Debug.Log("Press R/G/B/Y to change colors!");
        Debug.Log("Press I for info");
    }

    void Update()
    {
        // Color controls
        if (Input.GetKeyDown(KeyCode.R))
        {
            spriteRenderer.color = Color.red;
            currentColor = "Red";
            colorChanges++;
            Debug.Log("Color changed to: " + currentColor);
        }

        if (Input.GetKeyDown(KeyCode.G))
        {
            spriteRenderer.color = Color.green;
            currentColor = "Green";
            colorChanges++;
            Debug.Log("Color changed to: " + currentColor);
        }

        if (Input.GetKeyDown(KeyCode.B))
        {
            spriteRenderer.color = Color.blue;
            currentColor = "Blue";
            colorChanges++;
            Debug.Log("Color changed to: " + currentColor);
        }

        if (Input.GetKeyDown(KeyCode.Y))
        {
            spriteRenderer.color = Color.yellow;
            currentColor = "Yellow";
            colorChanges++;
            Debug.Log("Color changed to: " + currentColor);
        }

        // Info display
        if (Input.GetKeyDown(KeyCode.I))
        {
            Debug.Log("=== COLOR INFO ===");
            Debug.Log("Current color: " + currentColor);
            Debug.Log("Total changes: " + colorChanges);
        }
    }
}
```

### Extra Uitdaging:

- Voeg meer kleuren toe (paars, oranje, zwart)
- Reset kleur naar wit met de W toets
- Laat de sprite groter worden bij elke kleurwissel

---

## Oefening 3: 2D Simple Mover ⭐⭐

**Combinatie**: Input + Transform + Variabelen

**Tijd**: 25-30 minuten

### Wat Ga Je Maken?

Een 2D sprite die je kunt besturen met WASD toetsen en info bijhoudt over beweging.

### Setup:

1. Maak een **2D Sprite** (gebruik een square of circle)
2. Maak een nieuw script: `Simple2DMover`
3. Sleep het script op de Sprite

```csharp
public class Simple2DMover : MonoBehaviour
{
    // Movement settings
    public float moveSpeed = 5.0f;
    public string playerName = "Player1";

    // Movement tracking
    private Vector2 startPosition;
    private float totalDistance = 0.0f;
    private int keyPresses = 0;

    void Start()
    {
        // Remember starting position
        startPosition = transform.position;

        Debug.Log("=== 2D SIMPLE MOVER ===");
        Debug.Log("Player: " + playerName);
        Debug.Log("Use WASD to move!");
        Debug.Log("Press I for info, H for home");
        Debug.Log("======================");
    }

    void Update()
    {
        // Remember old position for distance calculation
        Vector2 oldPosition = transform.position;

        // Movement controls
        if (Input.GetKey(KeyCode.W))
        {
            transform.position += Vector3.up * moveSpeed * Time.deltaTime;
            keyPresses++;
        }

        if (Input.GetKey(KeyCode.S))
        {
            transform.position += Vector3.down * moveSpeed * Time.deltaTime;
            keyPresses++;
        }

        if (Input.GetKey(KeyCode.A))
        {
            transform.position += Vector3.left * moveSpeed * Time.deltaTime;
            keyPresses++;
        }

        if (Input.GetKey(KeyCode.D))
        {
            transform.position += Vector3.right * moveSpeed * Time.deltaTime;
            keyPresses++;
        }

        // Calculate distance moved this frame
        float distanceMoved = Vector2.Distance(oldPosition, transform.position);
        totalDistance += distanceMoved;

        // Info display
        if (Input.GetKeyDown(KeyCode.I))
        {
            Debug.Log("=== MOVEMENT INFO ===");
            Debug.Log("Current position: " + transform.position);
            Debug.Log("Distance from start: " + Vector2.Distance(startPosition, transform.position));
            Debug.Log("Total distance traveled: " + totalDistance);
            Debug.Log("Total key presses: " + keyPresses);
        }

        // Return home
        if (Input.GetKeyDown(KeyCode.H))
        {
            transform.position = startPosition;
            totalDistance = 0.0f;
            keyPresses = 0;
            Debug.Log("Returned home! Stats reset.");
        }
    }
}
```

### Extra Uitdaging:

- Voeg een "speed boost" toe met Shift
- Laat een trail achter de speler (verander kleur na beweging)
- Voeg grenzen toe zodat de speler niet buiten beeld kan

---

## Oefening 4: 2D Inventory System ⭐⭐

**Combinatie**: Variabelen + Input + Logica

**Tijd**: 25-30 minuten

### Wat Ga Je Maken?

Een simpel inventory systeem waar je items kunt verzamelen en gebruiken.

### Setup:

1. Maak een **Empty GameObject**
2. Maak een nieuw script: `SimpleInventory`
3. Sleep het script op het GameObject

```csharp
public class SimpleInventory : MonoBehaviour
{
    // Inventory variabelen
    public string playerName = "Adventurer";
    public int coins = 0;
    public int healthPotions = 0;
    public int manaPotions = 0;
    public int keys = 0;

    // Player stats
    public int currentHealth = 100;
    public int maxHealth = 100;
    public int currentMana = 50;
    public int maxMana = 100;

    void Start()
    {
        Debug.Log("=== SIMPLE INVENTORY ===");
        Debug.Log("Player: " + playerName);
        Debug.Log("=== CONTROLS ===");
        Debug.Log("Press 1-4 to collect items");
        Debug.Log("Press Q/E to use potions");
        Debug.Log("Press I for inventory info");
        Debug.Log("Press S for player stats");
        Debug.Log("=======================");
    }

    void Update()
    {
        // Collect items
        if (Input.GetKeyDown(KeyCode.Alpha1))
        {
            coins += 10;
            Debug.Log("Found 10 coins! Total: " + coins);
        }

        if (Input.GetKeyDown(KeyCode.Alpha2))
        {
            healthPotions++;
            Debug.Log("Found health potion! Total: " + healthPotions);
        }

        if (Input.GetKeyDown(KeyCode.Alpha3))
        {
            manaPotions++;
            Debug.Log("Found mana potion! Total: " + manaPotions);
        }

        if (Input.GetKeyDown(KeyCode.Alpha4))
        {
            keys++;
            Debug.Log("Found a key! Total: " + keys);
        }

        // Use items
        if (Input.GetKeyDown(KeyCode.Q))
        {
            if (healthPotions > 0 && currentHealth < maxHealth)
            {
                healthPotions--;
                currentHealth += 25;
                if (currentHealth > maxHealth) currentHealth = maxHealth;
                Debug.Log("Used health potion! Health: " + currentHealth + "/" + maxHealth);
            }
            else if (healthPotions <= 0)
            {
                Debug.Log("No health potions left!");
            }
            else
            {
                Debug.Log("Health is already full!");
            }
        }

        if (Input.GetKeyDown(KeyCode.E))
        {
            if (manaPotions > 0 && currentMana < maxMana)
            {
                manaPotions--;
                currentMana += 30;
                if (currentMana > maxMana) currentMana = maxMana;
                Debug.Log("Used mana potion! Mana: " + currentMana + "/" + maxMana);
            }
            else if (manaPotions <= 0)
            {
                Debug.Log("No mana potions left!");
            }
            else
            {
                Debug.Log("Mana is already full!");
            }
        }

        // Display info
        if (Input.GetKeyDown(KeyCode.I))
        {
            Debug.Log("=== INVENTORY ===");
            Debug.Log("Coins: " + coins);
            Debug.Log("Health Potions: " + healthPotions);
            Debug.Log("Mana Potions: " + manaPotions);
            Debug.Log("Keys: " + keys);
        }

        if (Input.GetKeyDown(KeyCode.S))
        {
            Debug.Log("=== PLAYER STATS ===");
            Debug.Log("Health: " + currentHealth + "/" + maxHealth);
            Debug.Log("Mana: " + currentMana + "/" + maxMana);
        }
    }
}
```

### Extra Uitdaging:

- Voeg een shop systeem toe (koop potions met coins)
- Laat health/mana langzaam afnemen over tijd
- Voeg verschillende soorten keys toe (golden key, silver key)

---

## Oefening 5: 2D Pet Simulator ⭐⭐⭐

**Combinatie**: Alle concepten + Time.time

**Tijd**: 35-40 minuten

### Wat Ga Je Maken?

Een virtuele 2D pet die je moet verzorgen met eten, spelen en slapen.

### Setup:

1. Maak een **2D Sprite** (je pet)
2. Maak een nieuw script: `VirtualPet2D`
3. Sleep het script op de Sprite

```csharp
public class VirtualPet2D : MonoBehaviour
{
    // Pet info
    public string petName = "Buddy";
    public string petType = "Cat";

    // Pet needs (0-100)
    public float hunger = 50.0f;
    public float happiness = 50.0f;
    public float energy = 50.0f;

    // Pet status
    private bool isAlive = true;
    private string currentMood = "Neutral";

    // Sprite reference
    private SpriteRenderer spriteRenderer;

    // Time tracking
    private float lastUpdateTime;

    void Start()
    {
        spriteRenderer = GetComponent<SpriteRenderer>();
        lastUpdateTime = Time.time;

        Debug.Log("=== VIRTUAL PET 2D ===");
        Debug.Log("Meet your new pet: " + petName + " the " + petType);
        Debug.Log("=== CONTROLS ===");
        Debug.Log("Press F to feed");
        Debug.Log("Press P to play");
        Debug.Log("Press R to rest");
        Debug.Log("Press I for pet info");
        Debug.Log("====================");

        UpdatePetVisuals();
    }

    void Update()
    {
        if (!isAlive) return;

        // Update pet needs over time (every second)
        if (Time.time - lastUpdateTime >= 1.0f)
        {
            hunger -= 2.0f;
            happiness -= 1.0f;
            energy -= 1.5f;

            // Clamp values
            hunger = Mathf.Clamp(hunger, 0, 100);
            happiness = Mathf.Clamp(happiness, 0, 100);
            energy = Mathf.Clamp(energy, 0, 100);

            lastUpdateTime = Time.time;
            UpdatePetMood();
            UpdatePetVisuals();

            // Check if pet is still alive
            if (hunger <= 0 || happiness <= 0 || energy <= 0)
            {
                PetDied();
            }
        }

        // Player actions
        if (Input.GetKeyDown(KeyCode.F))
        {
            FeedPet();
        }

        if (Input.GetKeyDown(KeyCode.P))
        {
            PlayWithPet();
        }

        if (Input.GetKeyDown(KeyCode.R))
        {
            LetPetRest();
        }

        if (Input.GetKeyDown(KeyCode.I))
        {
            ShowPetInfo();
        }
    }

    void FeedPet()
    {
        hunger += 20.0f;
        happiness += 5.0f;
        hunger = Mathf.Clamp(hunger, 0, 100);
        happiness = Mathf.Clamp(happiness, 0, 100);

        Debug.Log(petName + " enjoyed the food! *chomp chomp*");
        UpdatePetMood();
        UpdatePetVisuals();
    }

    void PlayWithPet()
    {
        happiness += 15.0f;
        energy -= 10.0f;
        happiness = Mathf.Clamp(happiness, 0, 100);
        energy = Mathf.Clamp(energy, 0, 100);

        Debug.Log(petName + " had fun playing! *happy sounds*");
        UpdatePetMood();
        UpdatePetVisuals();
    }

    void LetPetRest()
    {
        energy += 25.0f;
        hunger -= 5.0f;
        energy = Mathf.Clamp(energy, 0, 100);
        hunger = Mathf.Clamp(hunger, 0, 100);

        Debug.Log(petName + " is resting... *sleepy sounds*");
        UpdatePetMood();
        UpdatePetVisuals();
    }

    void UpdatePetMood()
    {
        float averageNeed = (hunger + happiness + energy) / 3.0f;

        if (averageNeed > 75)
        {
            currentMood = "Very Happy";
        }
        else if (averageNeed > 50)
        {
            currentMood = "Content";
        }
        else if (averageNeed > 25)
        {
            currentMood = "Unhappy";
        }
        else
        {
            currentMood = "Very Sad";
        }
    }

    void UpdatePetVisuals()
    {
        // Change color based on mood
        if (currentMood == "Very Happy")
        {
            spriteRenderer.color = Color.green;
        }
        else if (currentMood == "Content")
        {
            spriteRenderer.color = Color.white;
        }
        else if (currentMood == "Unhappy")
        {
            spriteRenderer.color = Color.yellow;
        }
        else
        {
            spriteRenderer.color = Color.red;
        }
    }

    void ShowPetInfo()
    {
        Debug.Log("=== PET STATUS ===");
        Debug.Log("Name: " + petName + " the " + petType);
        Debug.Log("Mood: " + currentMood);
        Debug.Log("Hunger: " + (int)hunger + "/100");
        Debug.Log("Happiness: " + (int)happiness + "/100");
        Debug.Log("Energy: " + (int)energy + "/100");
        Debug.Log("Status: " + (isAlive ? "Alive" : "Dead"));
    }

    void PetDied()
    {
        isAlive = false;
        spriteRenderer.color = Color.black;

        Debug.Log("=================");
        Debug.Log("Oh no! " + petName + " has died!");
        Debug.Log("You need to take better care of your pet!");
        Debug.Log("=================");
    }
}
```

### Extra Uitdaging:

- Voeg een "revival" systeem toe (R toets om pet weer tot leven te wekken)
- Laat de pet groeien (groter worden) naarmate je er goed voor zorgt
- Voeg verschillende pet types toe met verschillende behoeften

---

## Inlever Format

Voor elke oefening die je maakt, voeg je het volgende toe aan je README:

```markdown
## [Oefening Naam]

### Beschrijving

Korte uitleg van wat je hebt gemaakt.

### Wat ik heb geleerd

- Specifieke technieken/concepten die je hebt toegepast
- Problemen die je hebt opgelost

### Demo

![Demo GIF](link-naar-gif)

### Code

[Link naar script bestand](link-naar-code)
```

## Tips voor Succes

1. **Start klein**: Begin met oefening 1 en werk omhoog
2. **Test vaak**: Druk regelmatig op Play om je code te testen
3. **Lees foutmeldingen**: Unity helpt je altijd met duidelijke foutmeldingen
4. **Experimenteer**: Pas waarden aan en kijk wat er gebeurt
5. **Vraag hulp**: Als je vastloopt, vraag dan hulp aan de docent of medestudenten

Veel plezier met programmeren! 🎮
