# Les 13: Wave Management & Enemy Spawning

## Concept Uitleg

Wave management regelt wanneer en hoeveel vijanden verschijnen. Dit zorgt voor progressief moeilijker gameplay. Spawning omvat `Instantiate()` op bepaalde tijdstaten of triggers.

### Praktisch Voorbeeld (Joust Context)
```csharp
public class WaveManager : MonoBehaviour
{
    private int currentWave = 1;
    private int enemiesPerWave;
    private int enemiesDefeated = 0;
    
    void CheckWaveComplete()
    {
        if (enemiesDefeated >= enemiesPerWave)
        {
            currentWave++;
            enemiesPerWave = 2 + (currentWave * 2); // Stijgt per wave
            SpawnWave();
        }
    }
    
    void SpawnWave()
    {
        for (int i = 0; i < enemiesPerWave; i++)
        {
            Instantiate(enemyPrefab, GetRandomSpawnPoint(), Quaternion.identity);
        }
    }
}
```

## Oefening: Progressieve Wave Arena

### Doel
Maak een arena waar golven vijanden verschijnen met stijgende moeilijkheid.

### Stappen

1. **Scene Setup**
   - Creëer een Arena (Platform)
   - Creëer Player
   - Creëer Enemy Prefab (Red Cube met Rigidbody2D)

2. **Script: `Enemy.cs`**
```csharp
using UnityEngine;

public class Enemy : MonoBehaviour
{
    public float health = 50f;
    public float moveSpeed = 2f;
    private WaveManager waveManager;
    
    void Start()
    {
        waveManager = FindObjectOfType<WaveManager>();
    }
    
    public void TakeDamage(float damage)
    {
        health -= damage;
        if (health <= 0)
        {
            Defeated();
        }
    }
    
    void Defeated()
    {
        if (waveManager != null)
            waveManager.EnemyDefeated();
        Destroy(gameObject);
    }
}
```

3. **Script: `WaveManager.cs`**
```csharp
using UnityEngine;
using UnityEngine.UI;

public class WaveManager : MonoBehaviour
{
    public GameObject enemyPrefab;
    public Transform[] spawnPoints;
    public Text waveText;
    
    private int currentWave = 1;
    private int enemiesInWave = 2;
    private int enemiesDefeated = 0;
    private int enemiesSpawned = 0;
    private bool waveActive = false;
    
    void Start()
    {
        SpawnWave();
    }
    
    void SpawnWave()
    {
        waveActive = true;
        enemiesSpawned = 0;
        enemiesDefeated = 0;
        enemiesInWave = 2 + (currentWave * 2); // Moeilijker per wave
        
        UpdateUI();
        Debug.Log($"Wave {currentWave} started! Enemies: {enemiesInWave}");
        
        // Spawn enemies staggered
        InvokeRepeating("SpawnSingleEnemy", 0f, 1f);
    }
    
    void SpawnSingleEnemy()
    {
        if (enemiesSpawned >= enemiesInWave)
        {
            CancelInvoke("SpawnSingleEnemy");
            return;
        }
        
        Transform spawnPoint = spawnPoints[Random.Range(0, spawnPoints.Length)];
        GameObject enemy = Instantiate(enemyPrefab, spawnPoint.position, Quaternion.identity);
        enemiesSpawned++;
    }
    
    public void EnemyDefeated()
    {
        enemiesDefeated++;
        
        if (enemiesDefeated >= enemiesInWave)
        {
            WaveComplete();
        }
    }
    
    void WaveComplete()
    {
        currentWave++;
        Debug.Log($"Wave {currentWave - 1} complete!");
        Invoke("SpawnWave", 3f);
    }
    
    void UpdateUI()
    {
        if (waveText != null)
            waveText.text = $"Wave: {currentWave}";
    }
}
```

4. **Setup**
   - Creëer 2-3 spawn points (lege GameObjects op arena)
   - Attach WaveManager aan Canvas of GameManager
   - Sleep enemyPrefab naar inspector
   - Sleep spawnPoints naar array
   - Test: Verslaa vijanden, volgende wave start

### Variatie: Difficulty Scaling
```csharp
void UpdateEnemyStats()
{
    Enemy enemy = spawnedEnemy.GetComponent<Enemy>();
    enemy.health = 50f + (currentWave * 10f);
    enemy.moveSpeed = 2f + (currentWave * 0.5f);
}
```

### Challenge: Boss Waves
```csharp
if (currentWave % 5 == 0)
{
    SpawnBoss(); // Elke 5e wave een baas
}
```

---

**Leerdoel:** Begrijpen hoe wave-systemen en progressieve moeilijkheid werken.
