# Les 11: Hoogte-Berekening voor Combat

## Concept Uitleg

In Joust bepaalt de hoogte van je ridder of je wint of verliest. Dit vereist positie-berekeningen om te bepalen wie hoger vliegt.

### Praktisch Voorbeeld (Joust Context)
```csharp
bool IsAboveOpponent(Transform opponent)
{
    return transform.position.y > opponent.position.y;
}

void OnCollisionEnter2D(Collision2D collision)
{
    if (IsAboveOpponent(collision.transform))
    {
        // Je wint!
        DefeatOpponent(collision.gameObject);
    }
    else
    {
        // Je verliest!
        TakeDamage();
    }
}
```

## Oefening: Hoogte-Gebaseerde Dominantie Systeem

### Doel
Maak een spel waarbij hoogte bepaalt wie wint in een botsing.

### Stappen

1. **Scene Setup**
   - Creëer 2 Knights (Sprites of Cubes)
   - Voeg Rigidbody2D toe aan elk (Body Type: Dynamic)
   - Creëer een Ground (Static Rigidbody2D)

2. **Script: `Knight.cs`**
```csharp
using UnityEngine;

public class Knight : MonoBehaviour
{
    public string knightName = "Knight 1";
    public float maxHealth = 100f;
    private float health;
    private Rigidbody2D rb;
    private SpriteRenderer spriteRenderer;
    private Color originalColor;
    
    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
        spriteRenderer = GetComponent<SpriteRenderer>();
        originalColor = spriteRenderer.color;
        health = maxHealth;
    }
    
    bool IsAbove(Transform opponent)
    {
        return transform.position.y > opponent.position.y;
    }
    
    void OnCollisionEnter2D(Collision2D collision)
    {
        Knight opponent = collision.gameObject.GetComponent<Knight>();
        if (opponent == null) return;
        
        if (IsAbove(opponent.transform))
        {
            Debug.Log($"{knightName} wint! Is hoger.");
            opponent.TakeDamage(25f);
            spriteRenderer.color = Color.green;
        }
        else
        {
            Debug.Log($"{knightName} verliest! Is lager.");
            TakeDamage(25f);
            spriteRenderer.color = Color.red;
        }
        
        Invoke("ResetColor", 0.5f);
    }
    
    void ResetColor()
    {
        spriteRenderer.color = originalColor;
    }
    
    public void TakeDamage(float damage)
    {
        health -= damage;
        Debug.Log($"{knightName} health: {health}");
        
        if (health <= 0)
        {
            Defeat();
        }
    }
    
    void Defeat()
    {
        Debug.Log($"{knightName} verslagen!");
        Destroy(gameObject);
    }
}
```

3. **Script: `KnightController.cs`**
```csharp
using UnityEngine;

public class KnightController : MonoBehaviour
{
    private Rigidbody2D rb;
    public float moveSpeed = 5f;
    public float flapForce = 5f;
    public string moveAxis = "Horizontal";
    public KeyCode flapKey = KeyCode.W;
    
    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }
    
    void Update()
    {
        // Horizontale beweging
        float moveX = Input.GetAxis(moveAxis);
        rb.velocity = new Vector2(moveX * moveSpeed, rb.velocity.y);
        
        // Flap
        if (Input.GetKeyDown(flapKey))
        {
            rb.velocity = new Vector2(rb.velocity.x, 0);
            rb.AddForce(Vector2.up * flapForce, ForceMode2D.Impulse);
        }
    }
}
```

4. **Setup**
   - Duplicate Knight, noem ze Knight 1 en Knight 2
   - Voeg KnightController toe
   - Knight 1: moveAxis = "Horizontal", flapKey = KeyCode.W
   - Knight 2: Maak custom axis voor Arrow Keys of andere toets

### Test Scenario
- Plaats Knight 1 hoger dan Knight 2
- Laat ze botsen
- Knight 1 zou moeten winnen

### Challenge: Combo System
```csharp
private int consecutiveWins = 0;

void OnCollisionEnter2D(Collision2D collision)
{
    if (IsAbove(opponent.transform))
    {
        consecutiveWins++;
        // Damage = 25 * combo multiplier
        opponent.TakeDamage(25f * (1f + consecutiveWins * 0.1f));
    }
    else
    {
        consecutiveWins = 0;
    }
}
```

---

**Leerdoel:** Begrijpen hoe positie-gebaseerde gamelogica werkt.
