**Niveau gevorderd:**

```csharp
using UnityEngine;
using System.Collections.Generic;

public class PlayerScore : MonoBehaviour
{
   // To Do's:
   // Private Variabele voor score type int
   // Private List voor "Coins" type int

   void Start()
   {
         // Loop: toon 3x een startbericht met Debug.Log in een loop

   }

   void Update()
   {
         // If-statement: check of score >= 50
         // Zo ja geef een bericht met Debug.Log dat je hebt gewonnen


         // Test: druk op spatie om een munt toe te voegen
         {
            ...
            // Roep functie AddCoin aan en geef de waarde van de coin mee
            // Gebruik Random.Range(int min, int max) om een random waarde aan je coin te geven
         }
   }

   // Functie om een munt toe te voegen
   void AddCoin(int coinValue)
   {
         // Voeg munt toe aan lijst
         // Verhoog score met de coin value
         // Geef bericht dat je een coin hebt gepakt en toon je nieuwe score
   }
}
```
