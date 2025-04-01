**Niveau Gevorderd:**

- **SceneSwitcher.cs** (voor StartScene):

  ```csharp
  using UnityEngine;
  using UnityEngine.SceneManagement;

  public class SceneSwitcher : MonoBehaviour
  {
          //Check of de speler de spatie indrukt
          //Laad de "GameScene" in met de LoadScene methode

  }
  ```

- **PlayerControl.cs** (voor GameScene):

  ```csharp
  using UnityEngine;

  public class PlayerControl : MonoBehaviour
  {
      // Maak een speed variabele die aanpasbaar is in de Inspector
      // Maak een variabele voor je prefab

      void Start()
      {
          //Maak een random waarde tussen de -10 en de 10 voor het plaatsen van een munt op de x-as
          //Gebruik de Instantiate methode om de coinPrefab op een random x-positie in de scene te zetten.

      }

      void Update()
      {
          //Beweeg de speler ging met pijltjestoetsen links en rechts of A en D
      }
  }
  ```
