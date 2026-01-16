# Les 12: AI Pathfinding - Simpel Volgen

## Concept Uitleg

AI-pathfinding zorgt ervoor dat NPC's intelligent zich bewegen. Een eenvoudig "volgen" systeem gebruikt `Vector2.Lerp()` of `Vector2.MoveTowards()` om langzaam naar een target te gaan.

### Praktisch Voorbeeld (Joust Context)
Tegenstanders vliegen naar de speler:

```csharp
public class EnemyKnight : MonoBehaviour
{
    public Transform player;
    public float moveSpeed = 3f;
    public float stoppingDistance = 1f;
    
    void Update()
    {
        if (Vector2.Distance(transform.position, player.position) > stoppingDistance)
        {
            Vector2 direction = ((Vector2)player.position - (Vector2)transform.position).normalized;
            transform.position += (Vector3)direction * moveSpeed * Time.deltaTime;
        }
    }
}
```

## Oefening: Follow the Leader Game

### Doel
Maak een spel waar AI-vijanden de speler achtervolgen en intelligent gedrag vertonen.

### Stappen

1. **Scene Setup**
   - Creëer een Player (blauwe cube met movement)
   - Creëer 3 Enemies (rode cubes)
   - Voeg Rigidbody2D toe (Body Type: Kinematic)
   - Voeg BoxCollider2D toe aan allen

2. **Script: `Player.cs`**
```csharp
using UnityEngine;

public class Player : MonoBehaviour
{
    public float moveSpeed = 5f;
    
    void Update()
    {
        float moveX = Input.GetAxis("Horizontal");
        float moveY = Input.GetAxis("Vertical");
        
        transform.position += new Vector3(moveX, moveY, 0) * moveSpeed * Time.deltaTime;
    }
}
```

3. **Script: `EnemyAI.cs`**
```csharp
using UnityEngine;

public class EnemyAI : MonoBehaviour
{
    public Transform target;
    public float moveSpeed = 3f;
    public float stoppingDistance = 0.5f;
    public float updateInterval = 0.2f;
    private float nextUpdateTime = 0f;
    private Vector2 moveDirection = Vector2.zero;
    
    void Update()
    {
        if (target == null) return;
        
        float distanceToTarget = Vector2.Distance(transform.position, target.position);
        
        if (distanceToTarget > stoppingDistance)
        {
            if (Time.time > nextUpdateTime)
            {
                // Bereken richting naar target
                moveDirection = ((Vector2)target.position - (Vector2)transform.position).normalized;
                nextUpdateTime = Time.time + updateInterval;
            }
            
            // Beweeg naar target
            transform.position += (Vector3)moveDirection * moveSpeed * Time.deltaTime;
        }
        else
        {
            // Gestopt bij target
            moveDirection = Vector2.zero;
        }
    }
}
```

4. **Setup**
   - Attach Player script aan de speler
   - Attach EnemyAI aan elk vijand
   - Sleep Player naar target field van elk vijand
   - Test: Beweeg met pijltjes, vijanden moeten volgen

### Variatie 1: Patrouille Mode
```csharp
public enum AIState { Following, Patrolling }
public AIState currentState = AIState.Patrolling;
public Vector2[] patrolPoints;

void Update()
{
    if (Vector2.Distance(transform.position, target.position) < detectionRange)
    {
        currentState = AIState.Following;
    }
    else if (currentState == AIState.Following)
    {
        currentState = AIState.Patrolling;
    }
    
    if (currentState == AIState.Following)
        FollowTarget();
    else
        Patrol();
}
```

### Variatie 2: Smooth Movement
```csharp
Vector2 targetDirection = ((Vector2)target.position - (Vector2)transform.position).normalized;
moveDirection = Vector2.Lerp(moveDirection, targetDirection, 5f * Time.deltaTime);
```

### Challenge: Intelligente Avoidance
```csharp
void AvoidObstacles()
{
    Collider2D[] nearbyObjects = Physics2D.OverlapCircleAll(
        transform.position,
        2f
    );
    
    foreach (Collider2D obj in nearbyObjects)
    {
        if (obj.gameObject != gameObject)
        {
            // Wijzig richting om botsing te vermijden
        }
    }
}
```

---

**Leerdoel:** Begrijpen hoe eenvoudige AI-beweging werkt met pathfinding.
