**Niveau gevorderd:**

- **ScoreManager.cs**:

  ```csharp
  using UnityEngine;

  public class ScoreManager : MonoBehaviour
  {
      // Zorg voor een variabele met je startscore

      // Maak een methode AddScore die vanaf een ander script aangeroepen kan worden en waaraan je de gescoorde punten mee kunt geven als argument.
      ... AddScore(...)
      {
            //tel de punten op bij de score

            //Stuur bericht naar de console dat je een munt hebt gepakt!
      }
  }
  ```

- **PlayerMove.cs**:

  ```csharp
  using UnityEngine;

  public class PlayerMove : MonoBehaviour
  {
        //Maak een aanpasbare snelheid variabele voor de besturing van de speler
        ... speed = ...;
        //Maak een variabele waarmee je een referentie naar het score-script kunt opslaan door deze in de inspector toe te voegen.
        ... scoreManager;

      void Start()
      {
          // Controleer of je scoreManager is meegegeven in de inspector
          if (... == ...)
          {
            //Geef een error als dat niet zo is
              ...("ScoreManager ontbreekt!");
          }
      }
      void Update()
      {
          // Beweeg speler met pijltjestoetsen en A,D links en rechts
      }

      void OnTriggerEnter(...)
      {
          // Check of je een gameobject raakt met de naam "Coin"
          if (... == "Coin")
          {
                //Stuur 10 punten naar de scoreManager

                //stuur bericht naar de console "Munt gepakt!"

                //Vernietig de munt
          }
      }
  }
  ```
