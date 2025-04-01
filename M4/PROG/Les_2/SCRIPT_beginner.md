**Niveau beginner:**

```csharp
using UnityEngine;

public class PlayerControl : MonoBehaviour
{
   public Rigidbody rb;           // Referentie naar Rigidbody
   public ... moveSpeed = 5f;   // Snelheid van bewegen
   public ... jumpForce = 5f;   // Kracht van sprong

   void Start()
   {
         // Haal Rigidbody op
         rb = GetComponent<Rigidbody>();
         Debug.Log("Speler klaar!");
   }

   void Update()
   {
         //Zorg dat het blokje naar links en rechts kan bewegen met de snelheid moveSpeed
         float input = Input.GetAxis(...);
         transform.... += Vector3.right * input * ... * Time.deltaTime;

         // Omhoog springen met spatie en een AddForce op de rigidbody
         if (Input.GetKeyDown(KeyCode....))
         {
            rb....(Vector3.... * jumpForce, ForceMode.Impulse);
         }
   }
}
```
