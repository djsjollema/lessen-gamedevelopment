```csharp
using UnityEngine;
using System.Collections;

public class SpawnManager : MonoBehaviour
{
     //Maak een variabele om je prefab op te slaan.
    //Geef de prefab van je enemy mee via de inspector

    void Start()
    {
        //Start de SpawnWave coroutine
    }

    //Maak van de SpawnWave functie een coroutine. Doe dit door deze het juiste return type te geven
    ... SpawnWave()
    {
        //Maak een loop die 5x uitgevoerd wordt
        {
            //gebruik het yield commando en laat de code 2 seconden wachten

            //bereken de positie voor je nieuwe enemy
            //elke nieuwe enemy moet op dezelfde afstand rechts van de vorige enemy geplaatst worden.
            Vector3 pos = ... + Vector3.right * .. * 2;

            //Instantieer de prefab en geeft deze de juiste positie.
            Instantiate(..., ..., Quaternion.identity);


            //Geef met debug log aan welke vijand er gespawned is dus ook het nummer van de vijand (0 tm 4)
        }
    }
}
```
