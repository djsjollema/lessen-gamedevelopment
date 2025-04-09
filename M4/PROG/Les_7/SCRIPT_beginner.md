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
      ... void AddScore(...)
      {
          score += ...; //Verhoog de score met het meegegeven aantal punten

          scoreText.text = "Score: " + ...;// Voeg je nieuwe score toe aan het textveld.
      }
  }
  ```

- **PlayerMove.cs**:

```csharp

public class PlayerMove : Monobehaviour{
    public float speed = 5f;
    public ScoreManager scoreManager;//Maak een variabele aan van het Type ScoreManager en sleep het object waar dit script op zit in het veldje

    private void Update(){
        //Zorg dat de speler vloeiend heen en weer kan lopen met pijltjes en A en D
        transform.Translate(... * ... * Input.GetAxis(...) * ...);
    }
    private void OnTriggerEnter(Collider other)
    {
        //Als de naam van het gameobject dat je raakt "Coin" is moet je de code uitvoeren
        if (other.gameObject.name == ...)
        {
            //Voeg 10 punten toe aan je scorebord met de methode AddScore van je ScoreManager script.
            scoreManager....(...);
            //Vernietig het gameobject van de geraakte coin
            Destroy(...);
        }
    }
}
```
