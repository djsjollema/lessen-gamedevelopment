# Les 2: AddForce() - Krachten Toepassen

## Concept Uitleg

`AddForce()` is een methode van `Rigidbody2D` waarmee je krachten kan toepassen op een object. Dit zorgt ervoor dat het object accelereert in een bepaalde richting. Dit is essentieel voor dynamische beweging.

### Syntax
```csharp
rb.AddForce(new Vector2(x, y), ForceMode2D.Force);
```

### ForceMode2D Opties
- **Force:** Voegt versnelling toe (beïnvloed door massa)
- **Impulse:** Onmiddellijke snelheidsverandering

### Praktisch Voorbeeld (Flappy Bird Context)
In Flappy Bird geeft een "flap" direct een opwaarts kracht aan de vogel:

```csharp
public class Bird : MonoBehaviour
{
    private Rigidbody2D rb;
    public float flapForce = 5f;
    
    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            rb.velocity = Vector2.zero; // Reset snelheid
            rb.AddForce(Vector2.up * flapForce, ForceMode2D.Impulse);
        }
    }
}
```

## Oefening: Raket Lancering Simulator

### Doel
Maak een raket die met verschillende krachten omhoog kan worden gelanceerd.

### Stappen

1. **Setup Scene**
   - Creëer een 2D Scene
   - Voeg een Ground platform toe (Sprite + Rigidbody2D met Body Type: Static)
   - Creëer een Raket GameObject (vierkant of sprite)
   - Voeg Rigidbody2D toe aan de raket

2. **Script Maken: `RocketController.cs`**
```csharp
using UnityEngine;

public class RocketController : MonoBehaviour
{
    private Rigidbody2D rb;
    public float launchForce = 10f;
    private bool hasLaunched = false;
    
    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }
    
    void Update()
    {
        if (!hasLaunched && Input.GetKeyDown(KeyCode.Space))
        {
            Launch();
        }
        
        // Reset wanneer raket op grond is
        if (transform.position.y < -5f)
        {
            ResetPosition();
        }
    }
    
    void Launch()
    {
        rb.AddForce(Vector2.up * launchForce, ForceMode2D.Impulse);
        hasLaunched = true;
    }
    
    void ResetPosition()
    {
        transform.position = new Vector3(0, 1, 0);
        rb.velocity = Vector2.zero;
        hasLaunched = false;
    }
}
```

3. **Configuratie**
   - Attach het script aan de Raket
   - Stel `launchForce` in op verschillende waarden (5, 10, 20)
   - Test hoe hoog de raket komt per waarde

### Variatie
- Voeg meerdere raketten toe met verschillende `launchForce` waarden
- Wie bereikt het hoogst?

---

**Leerdoel:** Begrijpen hoe je `AddForce()` gebruikt om objecten in beweging te zetten.
