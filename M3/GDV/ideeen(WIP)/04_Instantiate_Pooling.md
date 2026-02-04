# Les 4: Instantiate & Object Pooling - Object Creatie

## Concept Uitleg

`Instantiate()` is een methode om nieuwe objecten tijdens runtime aan te maken. In games (zoals het genereren van buizen in Flappy Bird) moet je vaak dezelfde prefab meerdere keren klonen.

**Object Pooling** is een optimalisatie waarbij je objecten hergebruikt in plaats van ze constant aan te maken en te vernietigen.

### Instantiate Syntax
```csharp
Instantiate(prefab, position, rotation);
```

### Praktisch Voorbeeld (Flappy Bird Context)
Buizen worden herhaaldelijk gegenereerd:

```csharp
public class PipeSpawner : MonoBehaviour
{
    public GameObject pipePrefab;
    public float spawnRate = 2f;
    private float nextSpawnTime = 0f;
    
    void Update()
    {
        if (Time.time > nextSpawnTime)
        {
            Vector3 spawnPos = new Vector3(transform.position.x, Random.Range(-2f, 2f), 0);
            Instantiate(pipePrefab, spawnPos, Quaternion.identity);
            nextSpawnTime = Time.time + spawnRate;
        }
    }
}
```

## Oefening: Kogel Schiet Systeem

### Doel
Maak een speler die kogels kan afvuren door knopen in te drukken.

### Stappen

1. **Prefab Maken**
   - Maak een Bullet GameObject (kleine Sphere)
   - Voeg Rigidbody2D toe
   - Maak dit GameObject een Prefab (drag naar Assets folder)
   - Delete het uit de Scene

2. **Scene Opzetten**
   - Creëer een Speler GameObject
   - Voeg Rigidbody2D toe (Body Type: Dynamic, Gravity Scale: 0)

3. **Script: `GunController.cs`**
```csharp
using UnityEngine;

public class GunController : MonoBehaviour
{
    public GameObject bulletPrefab;
    public Transform firePoint;
    public float bulletSpeed = 10f;
    public float fireRate = 0.2f;
    private float lastFireTime = 0f;
    
    void Update()
    {
        if (Input.GetMouseButton(0) && Time.time > lastFireTime)
        {
            Fire();
            lastFireTime = Time.time + fireRate;
        }
    }
    
    void Fire()
    {
        GameObject bullet = Instantiate(bulletPrefab, firePoint.position, Quaternion.identity);
        Rigidbody2D bulletRb = bullet.GetComponent<Rigidbody2D>();
        bulletRb.velocity = firePoint.right * bulletSpeed;
        
        // Verwijder kogel na 5 seconden
        Destroy(bullet, 5f);
    }
}
```

4. **Configuratie**
   - Attach script aan Speler
   - Sleep bulletPrefab naar de inspector
   - Maak een GameObject als "FirePoint" (child van Speler aan voorkant)
   - Sleep FirePoint naar inspector

### Uitdaging: Object Pooling
```csharp
public class BulletPool : MonoBehaviour
{
    public GameObject bulletPrefab;
    private Queue<GameObject> pooledBullets = new Queue<GameObject>();
    private int poolSize = 20;
    
    void Start()
    {
        for (int i = 0; i < poolSize; i++)
        {
            GameObject bullet = Instantiate(bulletPrefab);
            bullet.SetActive(false);
            pooledBullets.Enqueue(bullet);
        }
    }
    
    public GameObject GetBullet(Vector3 position)
    {
        if (pooledBullets.Count == 0)
            return Instantiate(bulletPrefab, position, Quaternion.identity);
        
        GameObject bullet = pooledBullets.Dequeue();
        bullet.transform.position = position;
        bullet.SetActive(true);
        return bullet;
    }
    
    public void ReturnBullet(GameObject bullet)
    {
        bullet.SetActive(false);
        pooledBullets.Enqueue(bullet);
    }
}
```

---

**Leerdoel:** Begrijpen hoe je objecten aanmaakt en optimaliseert met object pooling.
