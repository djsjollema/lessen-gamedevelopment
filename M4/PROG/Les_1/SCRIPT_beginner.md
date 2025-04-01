**Niveau beginner:**

```csharp

using UnityEngine;
using System.Collections.Generic;

public class PlayerScore : MonoBehaviour
{
   private ... score = 0;                     // Variabele voor score
   private List<...> coins = new List<...>(); // Lijst voor munten

   void Start()
   {
         // Loop: toon 3x een startbericht
         for (...;...;...)
         {
            Debug.Log("Spel begint!");
         }
   }

   void Update()
   {
         // If-statement: check of score >= 50
         ... (score >= 50)
         {
            Debug.Log("Je hebt gewonnen!");
         }

         // Test: druk op spatie om een munt toe te voegen
         ... (Input.GetKeyDown(KeyCode....))
         {
            ... // Roep functie AddCoin() aan en geef als arguement 10 punten mee
         }
   }

   // Functie om een munt toe te voegen
   void AddCoin(int coinValue)
   {
         coins....(coinValue);      // Voeg munt toe aan lijst
         ...        // Verhoog score met de waarde van coinValue
         Debug.Log("Munt gepakt! Score: " + score);
   }
}
```
