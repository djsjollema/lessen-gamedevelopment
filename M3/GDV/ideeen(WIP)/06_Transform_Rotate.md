# Les 6: Transform.Rotate() - Rotatie

## Concept Uitleg

`Transform.Rotate()` is een methode om GameObjects te draaien rond assen. In Asteroids draait het schip rond de Z-as (omdat het een 2D spel is).

### Syntax
```csharp
transform.Rotate(x, y, z); // Graden per frame
// of
transform.Rotate(Vector3.forward * speed); // Rond Z-as
```

### Praktisch Voorbeeld (Asteroids Context)
Het schip in Asteroids roteert op basis van input:

```csharp
public class Spaceship : MonoBehaviour
{
    public float rotationSpeed = 200f;
    
    void Update()
    {
        float rotation = 0f;
        if (Input.GetKey(KeyCode.Left))
            rotation = rotationSpeed * Time.deltaTime;
        else if (Input.GetKey(KeyCode.Right))
            rotation = -rotationSpeed * Time.deltaTime;
        
        transform.Rotate(0, 0, rotation);
    }
}
```

## Oefening: Draaiende Platformgenerator

### Doel
Maak platforms die rond een centraal punt draaien.

### Stappen

1. **Scene Setup**
   - Creëer een leeg GameObject als "RotationCenter"
   - Creëer 3 Cubes als platforms
   - Zet elk platform als child van RotationCenter
   - Positioneer ze op verschillende afstanden

2. **Script: `RotatingPlatform.cs`**
```csharp
using UnityEngine;

public class RotatingPlatform : MonoBehaviour
{
    public float rotationSpeed = 45f; // Graden per seconde
    
    void Update()
    {
        transform.Rotate(0, 0, rotationSpeed * Time.deltaTime);
    }
}
```

3. **Attachment**
   - Attach script aan RotationCenter
   - Stel rotationSpeed in: 45, 90, 180
   - Observeer hoe snel het draait

### Variatie 1: Invertible Rotation
```csharp
public class RotatingPlatform : MonoBehaviour
{
    public float rotationSpeed = 45f;
    private bool clockwise = true;
    
    void Update()
    {
        float direction = clockwise ? 1f : -1f;
        transform.Rotate(0, 0, rotationSpeed * Time.deltaTime * direction);
        
        if (Input.GetKeyDown(KeyCode.R))
            clockwise = !clockwise;
    }
}
```

### Variatie 2: Player-Controlled Rotation
```csharp
public class PlayerRotation : MonoBehaviour
{
    public float rotationSpeed = 200f;
    
    void Update()
    {
        if (Input.GetKey(KeyCode.A))
            transform.Rotate(0, 0, rotationSpeed * Time.deltaTime);
        if (Input.GetKey(KeyCode.D))
            transform.Rotate(0, 0, -rotationSpeed * Time.deltaTime);
    }
}
```

### Challenge: 3D Rotatie
Maak een object dat rond alle assen draait:

```csharp
void Update()
{
    transform.Rotate(
        rotationSpeed * Time.deltaTime,  // X-as
        rotationSpeed * Time.deltaTime,  // Y-as
        rotationSpeed * Time.deltaTime   // Z-as
    );
}
```

---

**Leerdoel:** Begrijpen hoe rotatie werkt en hoe je objecten rond assen draait.
