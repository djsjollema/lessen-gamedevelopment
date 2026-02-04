# Les 5: Random - Willekeurige Waarden

## Concept Uitleg

`Random` genereert willekeurige waarden, essentieel voor speldesign. In Flappy Bird bepaal je willekeurig waar het gat tussen buizen verschijnt.

### Veelgebruikte Methods
```csharp
Random.Range(0f, 10f);           // Float tussen 0-10
Random.Range(1, 11);             // Int tussen 1-10
Random.value;                     // Float tussen 0-1
Random.insideUnitCircle;         // Random punt in cirkel
Random.onUnitSphere;             // Random richting
```

### Praktisch Voorbeeld (Flappy Bird Context)
```csharp
float gapPosition = Random.Range(-2f, 2f);
Instantiate(pipePrefab, new Vector3(10f, gapPosition, 0), Quaternion.identity);
```

## Oefening: Random Kleur Generator

### Doel
Maak een scene met objecten die willekeurige kleuren krijgen.

### Stappen

1. **Scene Setup**
   - Creëer 10 Cubes in een rij
   - Plaats ze op verschillende X-posities
   - Zorg dat ze niet overlappen

2. **Script: `RandomColorGenerator.cs`**
```csharp
using UnityEngine;

public class RandomColorGenerator : MonoBehaviour
{
    public SpriteRenderer spriteRenderer;
    public float changeInterval = 1f;
    private float nextChangeTime = 0f;
    
    void Start()
    {
        spriteRenderer = GetComponent<SpriteRenderer>();
        ChangeColor();
    }
    
    void Update()
    {
        if (Time.time > nextChangeTime)
        {
            ChangeColor();
            nextChangeTime = Time.time + changeInterval;
        }
    }
    
    void ChangeColor()
    {
        Color randomColor = new Color(
            Random.value,  // Red 0-1
            Random.value,  // Green 0-1
            Random.value   // Blue 0-1
        );
        spriteRenderer.color = randomColor;
    }
}
```

3. **Attachment**
   - Attach script aan elke cube
   - Test in Play Mode

### Variatie 1: Random Grootte
```csharp
void Start()
{
    float randomScale = Random.Range(0.5f, 2f);
    transform.localScale = Vector3.one * randomScale;
}
```

### Variatie 2: Random Positie
```csharp
void Randomize()
{
    float randomX = Random.Range(-10f, 10f);
    float randomY = Random.Range(-5f, 5f);
    transform.position = new Vector3(randomX, randomY, 0);
}
```

### Challenge: Willekeurige Obstakels
Creëer een script dat willekeurig obstakels spawn tussen bepaalde waarden (net als gaten in Flappy Bird):

```csharp
public class ObstacleSpawner : MonoBehaviour
{
    public GameObject obstaclePrefab;
    public float minGap = 2f;
    public float maxGap = 5f;
    
    void SpawnObstacle()
    {
        float randomGap = Random.Range(minGap, maxGap);
        // Spawn twee obstakels met randomGap tussen
    }
}
```

---

**Leerdoel:** Begrijpen hoe willekeurigheid spelenwerk maakt en hoe je Random() gebruikt.
