- **ScoreManager.cs**:

  ```csharp
  using UnityEngine;
  using TMPro;

  public class ScoreManager : MonoBehaviour
  {
      //Maak een variabele waarmee je een referentie naar je textveld kan maken. Het type is TMP_Text.

      //Maak een variabele waarin de je de score kunt opslaan

      void Start()
      {
          //geef je beginscore weer in je textveld.
      }

      public void AddScore(int points)
      {
            //Tel de opgepakte punten op bij je score

            //Geef de geupdate score weer in je textveld.

      }
  }
  ```

- **PlayerMove.cs**:

```csharp

public class PlayerMove : MonoBehaviour{
    //Maak een variabele voor de snelheid van de speler

    //Maak een variabele waar je een referentie kunt opslaan naar het ScoreManager script

    //Sleep het gameobject waar het ScoreManager scipt op staat in deze variabele in de inspector

       private void Update(){
       //zorg dat de speler vloeiend links en rechts kan bewegen met de pijltjes en A, D.
    }
    private void OnTriggerEnter(Collider other)
    {
        //check de naam van het gameboject waarvan je de trigger raakt. Als dit "Coin" is voer dan de code uit.
        if (...)
        {
            //Roep de AddScore methode van het ScoreManager script aan om score te verhogen met 10

            //Vernietig de geraakte Coin

        }
    }
}
```
