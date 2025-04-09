```csharp
using UnityEngine;
using System.Collections;

public class SpawnManager : MonoBehaviour
{
    ... enemyPrefab; //maak een enemyPrefab variabele waaraan je in de inspector een prefab mee kan geven.

    void Start()
    {
        //De SpawnWave functie is een "coroutine" dit herken je aan het IEnumerator type ervoor.
        //Start nu dus de coroutine SpawnWave()
        StartCoroutine(...);
    }

    IEnumerator SpawnWave()
    {
        //gebruik de for loop om de code 5x te herhalen
        for (...)
        {
            //laat de coroutine 2 seconden wachten met yield return new WaitForSeconds()
            yield return new WaitForSeconds(...);

            //sla de nieuwe positie van je enemy op in de varabele pos.
            //Bereken deze op basis van de positie van je spawnpoint
            //een position heeft 3 assen (x,y,z) bedenk zelf welk type deze variabele dus moet hebben.


            ... pos = ... + Vector3.right * i * 2;

            //Gebruik de Instantiate methode om een nieuwe enemy in je scene te plaatsen
            //Geef de prefab en de nieuwe positie mee.
            Instantiate(..., ..., Quaternion.identity);

            //Geef met debug log aan welke vijand er gespawned is dus ook het nummer van de vijand (0 tm 4)

        }
    }
}
```
