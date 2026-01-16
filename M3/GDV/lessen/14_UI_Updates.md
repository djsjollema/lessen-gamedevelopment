# Les 14: UI-Update voor Score en High Score

## Concept Uitleg

UI updates betreffen het bijwerken van scherm-elementen als Text, Image, Slider op basis van game-staat. Dit omvat score tracking, health bars, countdown timers, etc.

### Praktisch Voorbeeld (Flappy Bird Context)
```csharp
public class ScoreManager : MonoBehaviour
{
    public Text scoreText;
    public Text highScoreText;
    private int currentScore = 0;
    private int highScore = 0;
    
    void Start()
    {
        highScore = PlayerPrefs.GetInt("HighScore", 0);
        UpdateUI();
    }
    
    public void AddScore(int points)
    {
        currentScore += points;
        if (currentScore > highScore)
        {
            highScore = currentScore;
            PlayerPrefs.SetInt("HighScore", highScore);
        }
        UpdateUI();
    }
    
    void UpdateUI()
    {
        scoreText.text = $"Score: {currentScore}";
        highScoreText.text = $"High Score: {highScore}";
    }
}
```

## Oefening: Complete Game UI Systeem

### Doel
Maak een volledige UI met score, health, waves en high scores.

### Stappen

1. **Canvas Setup**
   - Creëer Canvas (Right-click: UI > Canvas)
   - Voeg deze Text elementen toe:
     - `ScoreText` - boven links
     - `HighScoreText` - boven rechts
     - `HealthText` - midden links
     - `WaveText` - midden boven
     - `GameOverText` - midden (inactief)

2. **Script: `GameUIManager.cs`**
```csharp
using UnityEngine;
using UnityEngine.UI;

public class GameUIManager : MonoBehaviour
{
    [SerializeField] private Text scoreText;
    [SerializeField] private Text highScoreText;
    [SerializeField] private Text healthText;
    [SerializeField] private Text waveText;
    [SerializeField] private Text gameOverText;
    [SerializeField] private Image healthBar;
    
    private int currentScore = 0;
    private int highScore;
    private int currentHealth = 100;
    private int currentWave = 1;
    private bool gameOver = false;
    
    void Start()
    {
        LoadHighScore();
        UpdateAllUI();
    }
    
    void LoadHighScore()
    {
        highScore = PlayerPrefs.GetInt("HighScore", 0);
    }
    
    public void AddScore(int points)
    {
        if (gameOver) return;
        
        currentScore += points;
        
        if (currentScore > highScore)
        {
            highScore = currentScore;
            PlayerPrefs.SetInt("HighScore", highScore);
        }
        
        UpdateScoreUI();
    }
    
    public void TakeDamage(int damage)
    {
        currentHealth -= damage;
        if (currentHealth < 0) currentHealth = 0;
        
        UpdateHealthUI();
        
        if (currentHealth <= 0)
        {
            GameOver();
        }
    }
    
    public void NextWave()
    {
        currentWave++;
        UpdateWaveUI();
    }
    
    void UpdateScoreUI()
    {
        scoreText.text = $"Score: {currentScore}";
        highScoreText.text = $"High Score: {highScore}";
    }
    
    void UpdateHealthUI()
    {
        healthText.text = $"Health: {currentHealth}";
        healthBar.fillAmount = currentHealth / 100f;
    }
    
    void UpdateWaveUI()
    {
        waveText.text = $"Wave: {currentWave}";
    }
    
    void UpdateAllUI()
    {
        UpdateScoreUI();
        UpdateHealthUI();
        UpdateWaveUI();
    }
    
    void GameOver()
    {
        gameOver = true;
        gameOverText.gameObject.SetActive(true);
        gameOverText.text = $"Game Over!\nFinal Score: {currentScore}\nHigh Score: {highScore}";
        Time.timeScale = 0f; // Pauzeer spel
    }
}
```

3. **Script: `Collectible.cs` (Example)**
```csharp
using UnityEngine;

public class Collectible : MonoBehaviour
{
    public int pointValue = 10;
    private GameUIManager uiManager;
    
    void Start()
    {
        uiManager = FindObjectOfType<GameUIManager>();
    }
    
    void OnTriggerEnter2D(Collider2D collision)
    {
        if (collision.CompareTag("Player"))
        {
            uiManager.AddScore(pointValue);
            Destroy(gameObject);
        }
    }
}
```

4. **Setup in Inspector**
   - Attach GameUIManager aan Canvas
   - Sleep alle Text elementen naar de inspector fields
   - Sleep healthBar Image naar inspector
   - Test: Score moet update tonen

### Variatie: Animatie UI Updates
```csharp
public void AddScore(int points)
{
    currentScore += points;
    
    // Toon popup
    StartCoroutine(PopupScore(points));
    
    UpdateScoreUI();
}

IEnumerator PopupScore(int points)
{
    Text popupText = Instantiate(scorePopupPrefab, scoreText.transform.parent);
    popupText.text = $"+{points}";
    popupText.color = Color.green;
    
    float duration = 1f;
    float elapsed = 0f;
    
    while (elapsed < duration)
    {
        elapsed += Time.deltaTime;
        popupText.transform.position += Vector3.up * 50f * Time.deltaTime;
        popupText.color = Color.Lerp(Color.green, Color.clear, elapsed / duration);
        yield return null;
    }
    
    Destroy(popupText.gameObject);
}
```

### Challenge: Persistent Data
```csharp
void SaveGameData()
{
    PlayerPrefs.SetInt("HighScore", highScore);
    PlayerPrefs.SetInt("TotalGamesPlayed", totalGames);
    PlayerPrefs.SetFloat("TotalPlayTime", totalTime);
}

void LoadGameData()
{
    highScore = PlayerPrefs.GetInt("HighScore", 0);
    totalGames = PlayerPrefs.GetInt("TotalGamesPlayed", 0);
    totalTime = PlayerPrefs.GetFloat("TotalPlayTime", 0f);
}
```

---

**Leerdoel:** Begrijpen hoe UI-elementen werken en game-data bijhoudt.
