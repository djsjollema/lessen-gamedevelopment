### Niveau Beginner

- **ScoreManager.cs**:

  ```csharp
  using UnityEngine;
  using ...;      //Zorg dat je de TMPro package importeert!

  public class ScoreManager : MonoBehaviour
  {
      public ... scoreText;    //Maak een variabele van het type TMP_Text
      private int score = 0;

      void Start()
      {
          scoreText.text = "Score: " + ...; //verander de  inhoud van het textveld in je UI en zet daar de score in;
      }

      //Zorg dat de methode AddScore vanaf een ander script aangeroepen kan worden en dat je daar een aantal punten aan mee kunt geven.
      ... void AddScore(int points)
      {
          score += points;
          scoreText.text = "Score: " + score;
      }
  }
  ```

- **PlayerMove.cs**:

```csharp

public class PlayerMove{
    public float speed = 5f;
    public ScoreManager scoreManager;
    private void Update(){
        transform.Translate(Vector3.right * speed * Input.GetAxis("Horizontal") * Time.deltaTime);
    }
    private void OnTriggerEnter(Collider other)
    {
        if (other.name == "Coin")
        {
            scoreManager.AddScore(10);
            Destroy(other.gameObject);
        }
    }
}
```
