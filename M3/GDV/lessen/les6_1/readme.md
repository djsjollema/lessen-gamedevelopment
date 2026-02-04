# Les 6.1 - Game States & Game Manager

## Leerdoelen

Na deze les kun je:

- Game States definiëren en beheren
- Een Game Manager singleton implementeren
- Data versturen tussen scripts (verschillende methodes)
- Action Events gebruiken voor losse koppeling

---

## Deel 1: Game States (15 min)

### Wat zijn Game States?

Een game state bepaalt "waar" de game zich bevindt:

```
┌─────────────────────────────────────────────────────────────┐
│                      GAME STATES                             │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│   [MainMenu] ──► [Playing] ──► [Paused] ──► [Playing]      │
│                      │                           │          │
│                      │                           │          │
│                      ▼                           │          │
│                 [GameOver] ◄─────────────────────┘          │
│                      │                                      │
│                      ▼                                      │
│                 [MainMenu]                                  │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### State Enum

```csharp
public enum GameState
{
    MainMenu,
    Playing,
    Paused,
    GameOver,
    LevelComplete
}
```

### State Gedrag

| State | Time.timeScale | Input | UI |
|-------|---------------|-------|-----|
| MainMenu | 1 | Menu only | Main menu |
| Playing | 1 | Full game | HUD |
| Paused | 0 | Pause menu | Pause menu |
| GameOver | 0 of 1 | Retry/Menu | Game over screen |

---

## Deel 2: Game Manager Singleton (20 min)

### Wat is een Singleton?

Een singleton zorgt ervoor dat er **maar één instantie** van een class bestaat, en maakt deze globaal toegankelijk.

### Basis Game Manager

```csharp
using UnityEngine;

public class GameManager : MonoBehaviour
{
    // Singleton instance
    public static GameManager Instance { get; private set; }
    
    // Game State
    public GameState CurrentState { get; private set; }
    
    // Game Data
    public int Score { get; private set; }
    public int Lives { get; private set; }
    public int Level { get; private set; }
    
    void Awake()
    {
        // Singleton pattern
        if (Instance != null && Instance != this)
        {
            Destroy(gameObject);
            return;
        }
        
        Instance = this;
        DontDestroyOnLoad(gameObject);  // Blijft bestaan tussen scenes
    }
    
    void Start()
    {
        InitializeGame();
    }
    
    void InitializeGame()
    {
        Score = 0;
        Lives = 3;
        Level = 1;
        SetState(GameState.MainMenu);
    }
    
    public void SetState(GameState newState)
    {
        CurrentState = newState;
        
        switch (newState)
        {
            case GameState.MainMenu:
                Time.timeScale = 1f;
                break;
                
            case GameState.Playing:
                Time.timeScale = 1f;
                break;
                
            case GameState.Paused:
                Time.timeScale = 0f;
                break;
                
            case GameState.GameOver:
                Time.timeScale = 0f;
                break;
        }
        
        Debug.Log($"Game State changed to: {newState}");
    }
    
    public void StartGame()
    {
        Score = 0;
        Lives = 3;
        SetState(GameState.Playing);
    }
    
    public void PauseGame()
    {
        if (CurrentState == GameState.Playing)
        {
            SetState(GameState.Paused);
        }
    }
    
    public void ResumeGame()
    {
        if (CurrentState == GameState.Paused)
        {
            SetState(GameState.Playing);
        }
    }
    
    public void AddScore(int points)
    {
        Score += points;
        Debug.Log($"Score: {Score}");
    }
    
    public void LoseLife()
    {
        Lives--;
        
        if (Lives <= 0)
        {
            SetState(GameState.GameOver);
        }
    }
}
```

### GameManager Gebruiken

```csharp
// Vanuit elk script:
GameManager.Instance.AddScore(100);
GameManager.Instance.LoseLife();
GameManager.Instance.PauseGame();

// State checken:
if (GameManager.Instance.CurrentState == GameState.Playing)
{
    // Doe game logic
}
```

---

## Deel 3: Data Delen Tussen Scripts (15 min)

### Methode 1: Direct Reference (Inspector)

```csharp
public class Player : MonoBehaviour
{
    [SerializeField] private ScoreDisplay scoreDisplay;  // Sleep in Inspector
    
    void CollectDot()
    {
        scoreDisplay.UpdateScore(10);
    }
}
```

**Pro:** Simpel, duidelijk
**Con:** Tight coupling, veel drag & drop

### Methode 2: FindObjectOfType

```csharp
public class Player : MonoBehaviour
{
    private ScoreDisplay scoreDisplay;
    
    void Start()
    {
        scoreDisplay = FindObjectOfType<ScoreDisplay>();
    }
    
    void CollectDot()
    {
        scoreDisplay.UpdateScore(10);
    }
}
```

**Pro:** Geen Inspector setup nodig
**Con:** Langzaam (niet in Update gebruiken!), kan null zijn

### Methode 3: Singleton (GameManager)

```csharp
public class Player : MonoBehaviour
{
    void CollectDot()
    {
        GameManager.Instance.AddScore(10);
    }
}
```

**Pro:** Globaal toegankelijk, centrale plek
**Con:** Kan leiden tot "god object"

### Methode 4: ScriptableObject als Data Container

```csharp
// GameData.cs (ScriptableObject)
[CreateAssetMenu(fileName = "GameData", menuName = "Game/GameData")]
public class GameData : ScriptableObject
{
    public int score;
    public int lives;
}

// Player.cs
public class Player : MonoBehaviour
{
    [SerializeField] private GameData gameData;
    
    void CollectDot()
    {
        gameData.score += 10;
    }
}

// ScoreDisplay.cs - zelfde GameData asset in Inspector
public class ScoreDisplay : MonoBehaviour
{
    [SerializeField] private GameData gameData;
    
    void Update()
    {
        scoreText.text = gameData.score.ToString();
    }
}
```

**Pro:** Decoupled, easy testing, persistent in editor
**Con:** Iets meer setup

---

## Deel 4: Action Events (10 min)

### Waarom Events?

Events zorgen voor **losse koppeling**: scripts hoeven elkaar niet te kennen.

```
ZONDER EVENTS:                    MET EVENTS:
                                  
Player ──► ScoreUI                Player ──► Event: "ScoreChanged"
Player ──► AudioManager                           │
Player ──► ParticleManager                        ├──► ScoreUI
                                                  ├──► AudioManager
Tight coupling!                                   └──► ParticleManager
                                  
                                  Loose coupling!
```

### System.Action Events

```csharp
using System;
using UnityEngine;

public class GameManager : MonoBehaviour
{
    public static GameManager Instance { get; private set; }
    
    // Events declareren
    public static event Action<int> OnScoreChanged;
    public static event Action<int> OnLivesChanged;
    public static event Action<GameState> OnGameStateChanged;
    
    private int score;
    private int lives;
    
    public void AddScore(int points)
    {
        score += points;
        
        // Event aanroepen (notify all listeners)
        OnScoreChanged?.Invoke(score);
    }
    
    public void LoseLife()
    {
        lives--;
        OnLivesChanged?.Invoke(lives);
        
        if (lives <= 0)
        {
            SetState(GameState.GameOver);
        }
    }
    
    public void SetState(GameState newState)
    {
        // ... state logic ...
        OnGameStateChanged?.Invoke(newState);
    }
}
```

### Event Listeners

```csharp
public class ScoreUI : MonoBehaviour
{
    [SerializeField] private TMP_Text scoreText;
    
    void OnEnable()
    {
        // Subscribe to event
        GameManager.OnScoreChanged += UpdateScoreDisplay;
    }
    
    void OnDisable()
    {
        // Unsubscribe (BELANGRIJK!)
        GameManager.OnScoreChanged -= UpdateScoreDisplay;
    }
    
    void UpdateScoreDisplay(int newScore)
    {
        scoreText.text = $"Score: {newScore}";
    }
}
```

### Meerdere Listeners

```csharp
// AudioManager luistert ook naar score changes
public class AudioManager : MonoBehaviour
{
    void OnEnable()
    {
        GameManager.OnScoreChanged += PlayScoreSound;
    }
    
    void OnDisable()
    {
        GameManager.OnScoreChanged -= PlayScoreSound;
    }
    
    void PlayScoreSound(int score)
    {
        // Speel geluidje af
    }
}

// ParticleManager ook
public class ParticleManager : MonoBehaviour
{
    void OnEnable()
    {
        GameManager.OnScoreChanged += SpawnParticles;
    }
    
    // etc...
}
```

---

## Oefeningen (60 min)

### Oefening 1: Game Manager Setup (20 min)

1. Maak een `GameManager` script met singleton
2. Voeg toe:
   - `GameState` enum (MainMenu, Playing, Paused, GameOver)
   - Score, Lives, Level properties
   - `SetState()` methode
3. Test door state te loggen

**Console output:**
```
Game initialized
State changed to: MainMenu
[Start button pressed]
State changed to: Playing
Score: 0, Lives: 3
[Pause button pressed]
State changed to: Paused
Time.timeScale = 0
```

### Oefening 2: Score & Lives System (20 min)

1. Maak `AddScore(int points)` methode
2. Maak `LoseLife()` methode
3. Trigger GameOver als lives = 0
4. Test met debug buttons of collisions

**Test scenario:**
```csharp
// Test in een apart script
void Update()
{
    if (Input.GetKeyDown(KeyCode.S))
        GameManager.Instance.AddScore(100);
    
    if (Input.GetKeyDown(KeyCode.L))
        GameManager.Instance.LoseLife();
}
```

**Console output:**
```
Score: 100
Score: 200
Lives: 2
Lives: 1
Lives: 0
State changed to: GameOver
```

### Oefening 3: Events Implementeren (20 min)

1. Voeg events toe aan GameManager:
   - `OnScoreChanged`
   - `OnLivesChanged`
   - `OnGameStateChanged`
   
2. Maak een `UIManager` die luistert naar events
3. Log wanneer events ontvangen worden

**Event flow test:**
```
Player raakt dot
  └─► GameManager.AddScore(10)
        └─► OnScoreChanged.Invoke(10)
              ├─► ScoreUI: "Score: 10"
              └─► AudioManager: *pling*

Player raakt ghost
  └─► GameManager.LoseLife()
        └─► OnLivesChanged.Invoke(2)
              └─► LivesUI: "❤️❤️"
```

---

## Samenvatting

### Data Delen Methodes

| Methode | Wanneer Gebruiken |
|---------|-------------------|
| Inspector Reference | Objecten in zelfde scene, weinig relaties |
| FindObjectOfType | Eenmalig in Start, als Inspector niet kan |
| Singleton | Globale managers (GameManager, AudioManager) |
| ScriptableObject | Shared data, settings, levels |
| Events | Losse koppeling, meerdere listeners |

### Event Checklist

- [ ] Event declareren: `public static event Action<T> OnEventName;`
- [ ] Event aanroepen: `OnEventName?.Invoke(value);`
- [ ] Subscribe in OnEnable: `ClassName.OnEventName += Handler;`
- [ ] Unsubscribe in OnDisable: `ClassName.OnEventName -= Handler;`

### GameManager Template

```csharp
public class GameManager : MonoBehaviour
{
    public static GameManager Instance { get; private set; }
    public static event Action<int> OnScoreChanged;
    
    public GameState CurrentState { get; private set; }
    public int Score { get; private set; }
    
    void Awake()
    {
        if (Instance != null) { Destroy(gameObject); return; }
        Instance = this;
        DontDestroyOnLoad(gameObject);
    }
    
    public void AddScore(int points)
    {
        Score += points;
        OnScoreChanged?.Invoke(Score);
    }
}
```

---

## Volgende Les

In **Les 6.2** gaan we UI elementen maken voor score, tijd en levens!
