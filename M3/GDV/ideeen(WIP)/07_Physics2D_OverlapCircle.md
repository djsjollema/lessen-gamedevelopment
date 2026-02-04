# Les 7: Physics2D.OverlapCircle() - Collision Detection

## Concept Uitleg

`Physics2D.OverlapCircle()` is een query-methode die alle Colliders in een bepaald gebied detecteert. Dit is handig voor explosies, hit detection, en omliggende objecten vinden.

### Syntax
```csharp
Collider2D[] colliders = Physics2D.OverlapCircleAll(center, radius, layerMask);
```

### Praktisch Voorbeeld (Asteroids Context)
Wanneer een projectiel een asteroïde raakt, controleer je alles in die omgeving:

```csharp
void OnTriggerEnter2D(Collider2D collision)
{
    Collider2D[] hitsAtExplosion = Physics2D.OverlapCircleAll(transform.position, 2f);
    foreach (Collider2D hit in hitsAtExplosion)
    {
        if (hit.CompareTag("Asteroid"))
        {
            hit.GetComponent<Asteroid>().TakeDamage();
        }
    }
}
```

## Oefening: Explosie Damage System

### Doel
Maak objecten die Schade aan hun omgeving kunnen aanrichten met een explosie.

### Stappen

1. **Scene Setup**
   - Creëer 1 Explosie-punt GameObject (Sphere, rood)
   - Creëer 5 Vijand GameObjects (Cubes, blauw) verspreid eromheen
   - Voeg aan elk Vijand een Rigidbody2D toe (geen gravity)

2. **Script: `Enemy.cs`**
```csharp
using UnityEngine;

public class Enemy : MonoBehaviour
{
    public float health = 100f;
    private SpriteRenderer spriteRenderer;
    
    void Start()
    {
        spriteRenderer = GetComponent<SpriteRenderer>();
    }
    
    public void TakeDamage(float damage)
    {
        health -= damage;
        Debug.Log($"Vijand geraakt! Health: {health}");
        
        if (health <= 0)
            Destroy(gameObject);
    }
}
```

3. **Script: `ExplosionManager.cs`**
```csharp
using UnityEngine;

public class ExplosionManager : MonoBehaviour
{
    public float explosionRadius = 5f;
    public float explosionDamage = 50f;
    public float explosionForce = 500f;
    
    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
            TriggerExplosion();
    }
    
    void TriggerExplosion()
    {
        Collider2D[] objectsHit = Physics2D.OverlapCircleAll(
            transform.position,
            explosionRadius
        );
        
        foreach (Collider2D hit in objectsHit)
        {
            Enemy enemy = hit.GetComponent<Enemy>();
            if (enemy != null)
            {
                enemy.TakeDamage(explosionDamage);
                
                // Explosieve kracht toepassen
                Rigidbody2D rb = hit.GetComponent<Rigidbody2D>();
                if (rb != null)
                {
                    Vector2 direction = (hit.transform.position - transform.position).normalized;
                    rb.AddForce(direction * explosionForce, ForceMode2D.Impulse);
                }
            }
        }
    }
}
```

4. **Test**
   - Attach ExplosionManager aan het explosie-punt
   - Stel explosionRadius in op 5
   - Druk SPATIE om explosie te triggeren
   - Observeer welke vijanden Schade nemen

### Variatie: Visualisatie
```csharp
void OnDrawGizmosSelected()
{
    Gizmos.color = Color.red;
    Gizmos.DrawWireSphere(transform.position, explosionRadius);
}
```

### Challenge: Meerdere Explosies
Maak een systeem waarbij explosies elkaar kunnen ketenen als vijanden elkaar treffen.

---

**Leerdoel:** Begrijpen hoe je Physics2D queries gebruikt voor area detection.
