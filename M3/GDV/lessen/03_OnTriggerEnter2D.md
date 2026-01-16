# Les 3: OnTriggerEnter2D() - Trigger Collisions

## Concept Uitleg

`OnTriggerEnter2D()` is een callback-methode die wordt aangeroepen wanneer een object met een Collider2D door een andere Collider2D (met "Is Trigger" ingesteld) gaat. Dit is ideaal voor detectie zonder fysieke botsing.

### Het Verschil: Collider vs Trigger
- **Collider:** Zorgt voor fysieke botsing (objecten kunnen elkaar niet passeren)
- **Trigger (Is Trigger = true):** Laat objecten erdoorheen gaan, detecteert alleen doorgaan

### Praktisch Voorbeeld (Flappy Bird Context)
In Flappy Bird zijn de buizen triggers. De vogel kan erdoorheen gaan en we detecteren:
- Raakt vogel een buis? → Game Over
- Passeert vogel veilig door? → Score +1

```csharp
public class Bird : MonoBehaviour
{
    void OnTriggerEnter2D(Collider2D collision)
    {
        if (collision.CompareTag("Pipe"))
        {
            GameManager.GameOver();
        }
    }
}
```

## Oefening: Collectible Items Verzamelen

### Doel
Maak een speler die munten kan verzamelen door er doorheen te lopen.

### Stappen

1. **Setup Scene**
   - Creëer een Speler (Cube/Sprite met Rigidbody2D)
   - Maak 5 Munten als kleine Spheres/Sprites
   - Voeg aan elke munt een `CircleCollider2D` toe
   - Check "Is Trigger" op elk munten-collider
   - Voeg een Tag "Coin" toe en tag alle munten

2. **Script: `PlayerCollector.cs`**
```csharp
using UnityEngine;

public class PlayerCollector : MonoBehaviour
{
    private int coinCount = 0;
    
    void OnTriggerEnter2D(Collider2D collision)
    {
        if (collision.CompareTag("Coin"))
        {
            coinCount++;
            Debug.Log($"Munten verzameld: {coinCount}");
            Destroy(collision.gameObject);
        }
    }
}
```

3. **Speler Beweging Script: `PlayerMovement.cs`**
```csharp
using UnityEngine;

public class PlayerMovement : MonoBehaviour
{
    private Rigidbody2D rb;
    public float speed = 5f;
    
    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }
    
    void Update()
    {
        float moveX = Input.GetAxis("Horizontal");
        float moveY = Input.GetAxis("Vertical");
        
        rb.velocity = new Vector2(moveX * speed, moveY * speed);
    }
}
```

4. **Configuratie**
   - Plaats munten willekeurig in de scene
   - Speel af en verzamel alle munten
   - Bekijk console output

### Variatie
- Voeg verschillende types collectibles toe (Gold coins = 10 punten, Silver coins = 5 punten)
- Display totale punten op UI

---

**Leerdoel:** Begrijpen hoe triggers werken en objecten detecteren zonder fysieke botsing.
