# Les 8: Vector2.Lerp() - Smooth Movement

## Concept Uitleg

`Vector2.Lerp()` is een linear interpolation function die twee posities vloeiend mengt. Het is essentieel voor vloeiende animaties en acceleratie-effecten.

### Syntax
```csharp
Vector2.Lerp(startValue, endValue, t); // t: 0-1, waarbij 0=start, 1=end
```

### Praktisch Voorbeeld (Asteroids Context)
Smooth acceleratie van het schip in plaats van instant snelheid:

```csharp
public class Spaceship : MonoBehaviour
{
    private Vector2 velocity = Vector2.zero;
    public float acceleration = 5f;
    public float maxSpeed = 10f;
    
    void Update()
    {
        Vector2 targetVelocity = Vector2.zero;
        if (Input.GetKey(KeyCode.Up))
            targetVelocity = transform.up * maxSpeed;
        
        // Smooth interpolation
        velocity = Vector2.Lerp(velocity, targetVelocity, acceleration * Time.deltaTime);
        transform.position += (Vector3)velocity * Time.deltaTime;
    }
}
```

## Oefening: Smooth Camera Follow

### Doel
Maak een camera die vloeiend een player volgt in plaats van instant te snappen.

### Stappen

1. **Scene Setup**
   - Creëer een Player (Cube met Rigidbody2D)
   - Zet de Main Camera als child van Canvas (of apart)
   - Voeg terrain toe (lange platform)

2. **Script: `PlayerController.cs`**
```csharp
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    public float moveSpeed = 5f;
    private Rigidbody2D rb;
    
    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }
    
    void Update()
    {
        float moveX = Input.GetAxis("Horizontal");
        rb.velocity = new Vector2(moveX * moveSpeed, rb.velocity.y);
    }
}
```

3. **Script: `CameraFollower.cs`**
```csharp
using UnityEngine;

public class CameraFollower : MonoBehaviour
{
    public Transform target;
    public float smoothSpeed = 5f;
    public Vector3 offset = new Vector3(0, 0, -10);
    
    void LateUpdate()
    {
        if (target == null) return;
        
        Vector3 desiredPosition = target.position + offset;
        Vector3 smoothedPosition = Vector3.Lerp(
            transform.position,
            desiredPosition,
            smoothSpeed * Time.deltaTime
        );
        
        transform.position = smoothedPosition;
    }
}
```

4. **Attachment**
   - Attach PlayerController aan Player
   - Attach CameraFollower aan Camera
   - Sleep Player naar target field
   - Test: Voeg smoothSpeed toe (waarden 1-10)

### Variatie: Ease-in-out Effect
```csharp
float t = smoothSpeed * Time.deltaTime;
// Ease-in-out curve
t = t * t * (3f - 2f * t);

Vector3 smoothedPosition = Vector3.Lerp(desiredPosition, transform.position, t);
```

### Challenge: Multi-Target Lerp
Maak een camera die tussen meerdere waypoints beweegt:

```csharp
private Vector3[] waypoints;
private int currentWaypoint = 0;

void Update()
{
    Vector3 currentTarget = waypoints[currentWaypoint];
    transform.position = Vector3.Lerp(
        transform.position,
        currentTarget,
        smoothSpeed * Time.deltaTime
    );
    
    if (Vector3.Distance(transform.position, currentTarget) < 0.1f)
        currentWaypoint++;
}
```

---

**Leerdoel:** Begrijpen hoe Lerp vloeiende bewegingen en acceleraties creëert.
