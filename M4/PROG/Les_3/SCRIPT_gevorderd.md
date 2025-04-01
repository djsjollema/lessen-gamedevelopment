**Niveau gevorderd:**

```csharp
using UnityEngine;

public class PlayerMove : MonoBehaviour
{
      //Maak een speed variabele
      void Update()
      {
         // Beweeg het blokje naar links en rechts met pijltjestoetsen of A,D
      }

      //Voer de code uit als je een trigger raakt
      void ...(Collider other)
      {
         // Munt oppakken als je de trigger raakt
         // Check de naam of tag van het geraakte gameobject
         if (other.gameObject.... == ...)
         {
            Debug.Log("Munt gepakt!");
            ... //Vernietig de geraakte munt
         }
      }
}
```
