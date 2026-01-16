# Les 10: OnCollisionEnter2D() - Fysieke Botsingen

## Concept Uitleg

`OnCollisionEnter2D()` is een callback die wordt aangeroepen wanneer twee objecten met Rigidbody2D fysiek botsen. Dit is anders van Triggers - hier vindt echte fysieke interactie plaats.

### Verschil met OnTriggerEnter2D
- **OnCollisionEnter2D:** Fysieke botsing (objecten kunnen niet door elkaar)
- **OnTriggerEnter2D:** Geen fysieke botsing (Is Trigger = true)

### Praktisch Voorbeeld (Joust Context)
Ridders botsen op elkaar; hoogte bepaalt de uitkomst:

```csharp
public class Knight : MonoBehaviour
{
    void OnCollisionEnter2D(Collision2D collision)
    {
        if (collision.gameObject.CompareTag("Knight"))
        {
            // Controleer wie hoger is
            if (transform.position.y > collision.transform.position.y)
            {
                // Ik win!
                Debug.Log("Victory!");
            }
        }
    }
}
```

## Oefening: Botsende Ballen Arena

### Doel
Maak ballen die tegen elkaar en de muur botsen met realistische fysica.

### Stappen

1. **Scene Setup**
   - Creëer een Canvas/Boundary (4 Walls als kinderen)
   - Zet alle walls als Rigidbody2D (Body Type: Static, Collider2D)
   - Creëer 3 Ballen (Spheres met Rigidbody2D, Body Type: Dynamic)
   - Voeg CircleCollider2D toe aan elke bal

2. **Script: `Ball.cs`**
```csharp
using UnityEngine;

public class Ball : MonoBehaviour
{
    public string ballName = "Ball";
    private Rigidbody2D rb;
    
    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }
    
    void OnCollisionEnter2D(Collision2D collision)
    {
        Debug.Log($"{ballName} botste met {collision.gameObject.name}");
        
        // Impact effect
        float impactForce = rb.velocity.magnitude;
        Debug.Log($"Impact kracht: {impactForce}");
    }
}
```

3. **Script: `BallLauncher.cs`**
```csharp
using UnityEngine;

public class BallLauncher : MonoBehaviour
{
    public Rigidbody2D targetBall;
    public float launchForce = 10f;
    
    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            LaunchBall();
        }
    }
    
    void LaunchBall()
    {
        Vector2 direction = new Vector2(
            Random.Range(-1f, 1f),
            Random.Range(-1f, 1f)
        ).normalized;
        
        targetBall.velocity = direction * launchForce;
    }
}
```

4. **Test**
   - Attach Ball script aan elke bal
   - Attach BallLauncher aan een GameManager
   - Druk SPATIE om ballen te lanceren
   - Bekijk collision logs

### Variatie: Botsing Effecten
```csharp
void OnCollisionEnter2D(Collision2D collision)
{
    // Partikel effect
    Instantiate(impactEffect, transform.position, Quaternion.identity);
    
    // Geluid
    AudioSource.PlayClipAtPoint(collisionSound, transform.position);
    
    // Kleurverandering
    GetComponent<SpriteRenderer>().color = Color.red;
}
```

### Challenge: Health System
```csharp
public float health = 100f;

void OnCollisionEnter2D(Collision2D collision)
{
    float damage = rb.velocity.magnitude * 10f;
    health -= damage;
    
    if (health <= 0)
        Destroy(gameObject);
}
```

---

**Leerdoel:** Begrijpen hoe fysieke botsingen werken en daarop reageren.
