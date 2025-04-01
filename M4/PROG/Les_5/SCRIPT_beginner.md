**Niveau beginner:**

- **ScoreManager.cs**:

  ```csharp
  using UnityEngine;

  public class ScoreManager : MonoBehaviour
  {
      ... ... score = ...; // Zorg voor een logische startscore moet deze aanpasbaar zijn in de inspector?

      // Zorg dat de methode AddScore vanaf een ander script ook punten kan doorgeven als argument
      public void AddScore(...)
      {
            //Tel de meegegeven punten op bij de score
            ... += points;
            // Debug de score naar de console
            Debug.Log("Score bijgewerkt: " + ...);
      }
  }
  ```

- **PlayerMove.cs**:

  ```csharp
  using UnityEngine;

  public class PlayerMove : MonoBehaviour
  {
      ... float speed = 5f;         // Maak de Snelheid van de speler aanpasbaar in de inspector
      public ... scoreManager;// Zorg dat je een Referentie naar je score-script kunt ontvangen door de classnaam als type aan te geven.

      void Start()
      {
          // Controleer of er een referentie naar je score-script is meegegeven in de inspector. Als die er niet is krijg je een "null - referentie"
          if (scoreManager == ...)
          {
            //debug het met een eigen error
              ....LogError("ScoreManager niet ingesteld!");
          }
      }

      void Update()
      {
          // Beweeg de speler links en rechts met pijltjestoetsen of A,D. gebruik ook de aanpasbare snelheid.
          float moveX = ....GetAxis(...) * ... * Time.delta.Time;
          Vector3 move = new Vector3(moveX,0f,0f);
          transform.Translate(move);
      }

      void OnTriggerEnter(Collider other)
      {
          // Check of het een munt is
          if (other.name == "Coin")
          {
              ...(10); // Roep de AddScore methode van de je score-script aan en geef 10 punten mee

              //Geef in de console een bericht dat je een munt hebt gepakt!
              ...("Munt gepakt!");

              //Vernietig de munt
              Destroy(...);
          }
      }
  }
  ```
