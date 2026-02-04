# Les 4.1 - Waypoint Systeem voor AI Beweging

## Leerdoelen

Na deze les kun je:

- Een waypoint systeem opzetten voor AI navigatie
- Vijanden laten patrouilleren langs waypoints
- Verschillende bewegingspatronen implementeren
- Vijand gedrag aanpassen op basis van game state

---

## Deel 1: Waypoint Concept (15 min)

### Wat zijn Waypoints?

Waypoints zijn onzichtbare punten in je level die een pad definiëren. AI characters volgen deze punten om zich door het level te bewegen.

```
    [W1]----[W2]----[W3]
     |               |
     |     LEVEL     |
     |               |
    [W4]----[W5]----[W6]
    
    Ghost volgt: W1 → W2 → W3 → W6 → W5 → W4 → W1 ...
```

### Waypoint vs Pathfinding

| Methode | Beschrijving | Gebruik |
|---------|--------------|---------|
| **Waypoints** | Vooraf gedefinieerde punten | Patrouilles, voorspelbaar gedrag |
| **Pathfinding** | Berekent route real-time | Dynamisch volgen, complexe levels |

Voor Pac-Man ghosts gebruiken we waypoints omdat:
- Gedrag moet voorspelbaar zijn (speler kan leren)
- Elke ghost heeft eigen patroon
- Simpeler te implementeren

---

## Deel 2: Waypoint Setup (15 min)

### Waypoint Script

```csharp
using UnityEngine;

public class Waypoint : MonoBehaviour
{
    public Waypoint[] connectedWaypoints;  // Waar kan je heen vanaf hier?
    
    void OnDrawGizmos()
    {
        // Teken waypoint in Scene view
        Gizmos.color = Color.yellow;
        Gizmos.DrawSphere(transform.position, 0.2f);
        
        // Teken connecties
        Gizmos.color = Color.white;
        foreach (Waypoint wp in connectedWaypoints)
        {
            if (wp != null)
            {
                Gizmos.DrawLine(transform.position, wp.transform.position);
            }
        }
    }
}
```

### Waypoints Plaatsen

1. Maak een lege GameObject `Waypoints` als parent
2. Maak child GameObjects voor elk waypoint
3. Voeg `Waypoint` script toe aan elk punt
4. Verbind waypoints via de Inspector (connectedWaypoints array)

**Tip:** Plaats waypoints op kruispunten in je doolhof!

```
Hierarchy:
├── Waypoints
│   ├── WP_TopLeft
│   ├── WP_TopRight
│   ├── WP_Center
│   ├── WP_BottomLeft
│   └── WP_BottomRight
```

---

## Deel 3: Ghost Movement (20 min)

### Basis Ghost Controller

```csharp
using UnityEngine;

public class GhostController : MonoBehaviour
{
    [Header("Movement")]
    public float moveSpeed = 4f;
    public Waypoint currentWaypoint;
    
    [Header("Behavior")]
    public GhostState state = GhostState.Patrol;
    
    private Waypoint targetWaypoint;
    
    public enum GhostState
    {
        Patrol,      // Normale patrouille
        Chase,       // Achtervolg speler
        Frightened,  // Vlucht (na power pellet)
        Eaten        // Terugkeren naar spawn
    }
    
    void Start()
    {
        if (currentWaypoint != null)
        {
            transform.position = currentWaypoint.transform.position;
            ChooseNextWaypoint();
        }
    }
    
    void Update()
    {
        MoveTowardsTarget();
        CheckArrival();
    }
    
    void MoveTowardsTarget()
    {
        if (targetWaypoint == null) return;
        
        Vector3 direction = (targetWaypoint.transform.position - transform.position).normalized;
        transform.position += direction * moveSpeed * Time.deltaTime;
    }
    
    void CheckArrival()
    {
        if (targetWaypoint == null) return;
        
        float distance = Vector3.Distance(transform.position, targetWaypoint.transform.position);
        
        if (distance < 0.1f)
        {
            // Aangekomen bij waypoint
            transform.position = targetWaypoint.transform.position;
            currentWaypoint = targetWaypoint;
            ChooseNextWaypoint();
        }
    }
    
    void ChooseNextWaypoint()
    {
        if (currentWaypoint.connectedWaypoints.Length == 0) return;
        
        switch (state)
        {
            case GhostState.Patrol:
                // Kies random verbonden waypoint
                int randomIndex = Random.Range(0, currentWaypoint.connectedWaypoints.Length);
                targetWaypoint = currentWaypoint.connectedWaypoints[randomIndex];
                break;
                
            case GhostState.Chase:
                // Kies waypoint dichtstbij speler
                targetWaypoint = GetWaypointClosestToPlayer();
                break;
                
            case GhostState.Frightened:
                // Kies waypoint verst van speler
                targetWaypoint = GetWaypointFarthestFromPlayer();
                break;
        }
    }
    
    Waypoint GetWaypointClosestToPlayer()
    {
        GameObject player = GameObject.FindWithTag("Player");
        if (player == null) return currentWaypoint.connectedWaypoints[0];
        
        Waypoint closest = null;
        float closestDistance = float.MaxValue;
        
        foreach (Waypoint wp in currentWaypoint.connectedWaypoints)
        {
            float dist = Vector3.Distance(wp.transform.position, player.transform.position);
            if (dist < closestDistance)
            {
                closestDistance = dist;
                closest = wp;
            }
        }
        
        return closest;
    }
    
    Waypoint GetWaypointFarthestFromPlayer()
    {
        GameObject player = GameObject.FindWithTag("Player");
        if (player == null) return currentWaypoint.connectedWaypoints[0];
        
        Waypoint farthest = null;
        float farthestDistance = 0f;
        
        foreach (Waypoint wp in currentWaypoint.connectedWaypoints)
        {
            float dist = Vector3.Distance(wp.transform.position, player.transform.position);
            if (dist > farthestDistance)
            {
                farthestDistance = dist;
                farthest = wp;
            }
        }
        
        return farthest;
    }
    
    // Publieke methode om state te veranderen
    public void SetState(GhostState newState)
    {
        state = newState;
        ChooseNextWaypoint(); // Herbereken route
    }
}
```

### Ghost Gedrag Uitleg

| State | Gedrag | Trigger |
|-------|--------|---------|
| **Patrol** | Random waypoints volgen | Start, timer |
| **Chase** | Naar speler toe bewegen | Speler in range |
| **Frightened** | Van speler weg vluchten | Power pellet |
| **Eaten** | Terug naar spawn | Ghost opgegeten |

---

## Deel 4: Geavanceerde Patronen (10 min)

### Voorkom Terugkeren (No U-Turn)

```csharp
private Waypoint previousWaypoint;

void ChooseNextWaypoint()
{
    // Filter: niet terug naar waar we vandaan kwamen
    List<Waypoint> validWaypoints = new List<Waypoint>();
    
    foreach (Waypoint wp in currentWaypoint.connectedWaypoints)
    {
        if (wp != previousWaypoint)
        {
            validWaypoints.Add(wp);
        }
    }
    
    // Als alleen terugweg mogelijk, dan toch terugkeren
    if (validWaypoints.Count == 0)
    {
        validWaypoints.Add(previousWaypoint);
    }
    
    // Kies uit geldige opties
    int index = Random.Range(0, validWaypoints.Count);
    previousWaypoint = currentWaypoint;
    targetWaypoint = validWaypoints[index];
}
```

### Unieke Ghost Persoonlijkheden

```csharp
public enum GhostPersonality
{
    Aggressive,  // Altijd chase
    Shy,         // Wisselt tussen patrol en chase
    Ambusher,    // Gaat naar waar speler naartoe gaat
    Random       // Onvoorspelbaar
}

public GhostPersonality personality;

void ChooseNextWaypoint()
{
    switch (personality)
    {
        case GhostPersonality.Aggressive:
            targetWaypoint = GetWaypointClosestToPlayer();
            break;
            
        case GhostPersonality.Ambusher:
            targetWaypoint = GetWaypointAheadOfPlayer();
            break;
            
        // etc...
    }
}
```

---

## Oefeningen (60 min)

### Oefening 1: Waypoint Netwerk (20 min)

1. Maak een simpel level met muren (of gebruik je grid uit Les 2.1)
2. Plaats 6-8 waypoints op kruispunten
3. Verbind de waypoints via de Inspector
4. Test of de gizmos correct tekenen in Scene view

**Verwacht resultaat in Scene view:**
```
    ○─────────○─────────○
    │         │         │
    │    ▢    │    ▢    │
    │         │         │
    ○─────────○─────────○
    │         │         │
    │    ▢    │    ▢    │
    │         │         │
    ○─────────○─────────○
    
    ○ = Waypoint (geel)
    ─ = Connectie (wit)
    ▢ = Muur
```

### Oefening 2: Patrouillerende Ghost (25 min)

1. Maak een Ghost prefab met sprite
2. Voeg `GhostController` script toe
3. Wijs een start waypoint toe
4. Test of ghost patrouilleert

**Verwacht gedrag:**
```
Ghost beweegt: WP1 → WP2 → WP3 → WP2 → WP4 → ...

Console output:
Moving to: WP_TopRight
Arrived at: WP_TopRight
Moving to: WP_Center
Arrived at: WP_Center
...
```

### Oefening 3: Ghost States (15 min)

1. Voeg een test-trigger toe die ghost state verandert
2. Test alle states:
   - Patrol: random beweging
   - Chase: beweegt naar speler
   - Frightened: vlucht van speler

**Test scenario:**
```csharp
// Test script op een trigger zone
void OnTriggerEnter2D(Collider2D other)
{
    if (other.CompareTag("Ghost"))
    {
        GhostController ghost = other.GetComponent<GhostController>();
        ghost.SetState(GhostController.GhostState.Frightened);
    }
}
```

**Verwacht gedrag:**
```
Normaal:      Ghost beweegt random
Speler nabij: Ghost beweegt naar speler (Chase)
Power pellet: Ghost vlucht van speler (Frightened)
```

---

## Samenvatting

| Concept | Code |
|---------|------|
| Waypoint maken | `public Waypoint[] connectedWaypoints;` |
| Naar waypoint bewegen | `Vector3.MoveTowards()` of `direction * speed` |
| Aankomst checken | `Vector3.Distance() < threshold` |
| Volgende kiezen | Random of gebaseerd op speler positie |
| State veranderen | `SetState(GhostState.Chase)` |

### Ghost AI Checklist

- [ ] Waypoints geplaatst op kruispunten
- [ ] Waypoints verbonden (geen dead ends)
- [ ] Ghost beweegt smooth tussen waypoints
- [ ] Ghost kiest nieuwe richting bij aankomst
- [ ] Geen U-turns (optioneel)
- [ ] States werken (Patrol, Chase, Frightened)

---

## Volgende Les

In **Les 4.2** gaan we usability en gameplay testen met echte spelers!
