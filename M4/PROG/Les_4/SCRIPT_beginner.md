**Niveau beginner:**

- **SceneSwitcher.cs** (voor StartScene):

  ```csharp
  using UnityEngine;
  using UnityEngine.SceneManagement;

  public class SceneSwitcher : MonoBehaviour
  {
      void ...()                      //Zorg dat de code elk frame wordt uitgevoerd
      {
          if (...(KeyCode.Space))     //Check of de speler de spatie indrukt
          {
              SceneManager....(...);  //Laad de "GameScene" in met de LoadScene methode
          }
      }
  }
  ```

- **PlayerControl.cs** (voor GameScene):

  ```csharp
  using UnityEngine;

  public class PlayerControl : MonoBehaviour
  {
      ... float speed = 5f;             // Aanpasbaar in Inspector
      ... GameObject coinPrefab;        // Sleep prefab hierin

      void Start()
      {
          float randVal = Random.Range(-10,10);
          ...(..., new Vector3(randVal, 0, 0), Quaternion.identity); //Gebruik de Instantiate methode om de coinPrefab in de scene te zetten.

      }

      void Update()
      {
          // Beweging met pijltjestoetsen links en rechts of A en D
          float input = Input....("Horizontal");
          //Vermenigvuldig de richting met de snelheid en de horizontale input waarde
          transform.Translate(... * ... * ... * Time.deltaTime);
      }
  }
  ```
