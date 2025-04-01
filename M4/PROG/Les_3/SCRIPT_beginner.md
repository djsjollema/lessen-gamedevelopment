**Niveau beginner:**

```csharp
using UnityEngine;

public class PlayerMove : MonoBehaviour
{
      ... = 5f;   //Maak een float voor je "speed"

      void Update()
      {

         // Beweging links en rechts met pijltjestoetsen gebruik de Translate functie
         // Zorg dat de beweging soepel is onafhankelijk van de framerate
         // Zorg dat de speed wordt overgenomen via de variabele "speed"
         float input = Input....;
         transform....(Vector3.right * input * ... * ...);

      }
      //Zorg dat deze code wordt uitgevoerd als je de trigger van een muntje raakt
      void On...Enter(Collider other)
      {
         // Munt oppakken
         if (other.gameObject.name == "Coin")//Let op dat je de munten in je scene allemaal "Coin" noemt
         {
            Debug.Log("Munt gepakt!");
            Destroy(...); // Vernietig de opgepakte coin
         }
      }
}
```
