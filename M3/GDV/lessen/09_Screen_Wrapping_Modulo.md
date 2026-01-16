# Les 9: Screen Boundary Wrapping met Modulo

## Concept Uitleg

Screen wrapping zorgt ervoor dat objecten die het scherm verlaten aan de andere kant verschijnen. Dit wordt gebruikt in klassieke arcade spellen. Modulo (%) helpt hierbij.

### Modulo Operator
```csharp
position.x = position.x % screenWidth; // Wrap rond schermrand
```

### Praktisch Voorbeeld (Asteroids Context)
Het schip verdwijnt links en verschijnt rechts:

```csharp
void Update()
{
    // Beweging
    transform.position += direction * speed * Time.deltaTime;
    
    // Wrapping
    Vector3 pos = transform.position;
    if (pos.x > screenWidth)
        pos.x = -screenWidth;
    else if (pos.x < -screenWidth)
        pos.x = screenWidth;
    
    transform.position = pos;
}
```

## Oefening: Pacman-Style Wrapping

### Doel
Maak een speler die rond een bepaald scherm wrappen kan.

### Stappen

1. **Scene Setup**
   - Creëer een Camera en stel orthographic mode in
   - Stel orthographic size in op 5
   - Creëer een Player (Cube)
   - Voeg Rigidbody2D toe (Body Type: Kinematic)

2. **Script: `WrappingPlayer.cs`**
```csharp
using UnityEngine;

public class WrappingPlayer : MonoBehaviour
{
    public float speed = 5f;
    private Vector2 direction = Vector2.zero;
    
    // Screen bounds
    private float screenWidth = 10f;  // orthographic size * aspect ratio
    private float screenHeight = 5f;   // orthographic size
    
    void Update()
    {
        // Input
        direction.x = Input.GetAxis("Horizontal");
        direction.y = Input.GetAxis("Vertical");
        
        // Beweging
        transform.position += (Vector3)direction * speed * Time.deltaTime;
        
        // Wrapping
        WrapPosition();
    }
    
    void WrapPosition()
    {
        Vector3 pos = transform.position;
        
        // X-as wrapping
        if (pos.x > screenWidth)
            pos.x = -screenWidth;
        else if (pos.x < -screenWidth)
            pos.x = screenWidth;
        
        // Y-as wrapping
        if (pos.y > screenHeight)
            pos.y = -screenHeight;
        else if (pos.y < -screenHeight)
            pos.y = screenHeight;
        
        transform.position = pos;
    }
}
```

3. **Test**
   - Attach script aan Player
   - Beweeg met pijltjes naar de rand
   - Observeer wrapping

### Variatie: Dynamische Screen Bounds
```csharp
void CalculateScreenBounds()
{
    Camera cam = Camera.main;
    screenHeight = cam.orthographicSize;
    screenWidth = screenHeight * cam.aspect;
}
```

### Challenge: Teleport Visuals
Voeg deeltjes toe wanneer de speler wrappen:

```csharp
public ParticleSystem wrapEffect;

if (wrapped)
{
    wrapEffect.Play();
}
```

---

**Leerdoel:** Begrijpen hoe screen wrapping werkt en screens definieert.
