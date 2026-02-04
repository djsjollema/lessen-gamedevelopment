# Les 6.2 - UI Elementen: Score, Tijd & Levens

## Leerdoelen

Na deze les kun je:

- Unity's UI systeem gebruiken (Canvas, RectTransform)
- Score displays maken en updaten via code
- Een timer implementeren
- Levens weergeven (tekst en iconen)

---

## Deel 1: Unity UI Basics (15 min)

### Canvas Setup

Een **Canvas** is het "tekenvel" voor alle UI elementen.

```
Hierarchy:
├── Canvas
│   ├── ScorePanel
│   │   ├── ScoreLabel
│   │   └── ScoreValue
│   ├── LivesPanel
│   │   ├── Life1
│   │   ├── Life2
│   │   └── Life3
│   └── TimerText
└── EventSystem
```

### Canvas Instellingen

| Setting | Waarde | Beschrijving |
|---------|--------|--------------|
| Render Mode | Screen Space - Overlay | UI altijd bovenop |
| UI Scale Mode | Scale With Screen Size | Past aan schermgrootte |
| Reference Resolution | 1920 x 1080 | Ontwerp resolutie |

### RectTransform Anchors

Anchors bepalen hoe UI elementen zich gedragen bij resize:

```
┌────────────────────────────────────────┐
│ ┌──Score──┐                 ┌──Time──┐ │
│ └─────────┘                 └────────┘ │
│  (anchor:                    (anchor:  │
│   top-left)                  top-right)│
│                                        │
│                                        │
│                                        │
│ ┌─Lives───┐                            │
│ └─────────┘                            │
│  (anchor: bottom-left)                 │
└────────────────────────────────────────┘
```

---

## Deel 2: Score Display (15 min)

### UI Setup

1. **GameObject** → UI → **Text - TextMeshPro**
2. Noem het `ScoreText`
3. Anchor naar top-left
4. Position: (100, -50)

### Score Script

```csharp
using UnityEngine;
using TMPro;

public class ScoreDisplay : MonoBehaviour
{
    [SerializeField] private TMP_Text scoreText;
    
    private int displayedScore = 0;
    private int targetScore = 0;
    
    void Start()
    {
        UpdateDisplay();
    }
    
    void OnEnable()
    {
        // Subscribe to score events
        GameManager.OnScoreChanged += OnScoreChanged;
    }
    
    void OnDisable()
    {
        GameManager.OnScoreChanged -= OnScoreChanged;
    }
    
    void OnScoreChanged(int newScore)
    {
        targetScore = newScore;
    }
    
    void Update()
    {
        // Animated score counting
        if (displayedScore < targetScore)
        {
            displayedScore += Mathf.CeilToInt((targetScore - displayedScore) * Time.deltaTime * 5f);
            displayedScore = Mathf.Min(displayedScore, targetScore);
            UpdateDisplay();
        }
    }
    
    void UpdateDisplay()
    {
        scoreText.text = $"Score: {displayedScore:N0}";  // N0 = number format with thousands separator
    }
}
```

### Score met Animatie

```csharp
using UnityEngine;
using TMPro;
using System.Collections;

public class AnimatedScoreDisplay : MonoBehaviour
{
    [SerializeField] private TMP_Text scoreText;
    [SerializeField] private float punchScale = 1.2f;
    [SerializeField] private float punchDuration = 0.1f;
    
    void OnEnable()
    {
        GameManager.OnScoreChanged += OnScoreChanged;
    }
    
    void OnDisable()
    {
        GameManager.OnScoreChanged -= OnScoreChanged;
    }
    
    void OnScoreChanged(int newScore)
    {
        scoreText.text = $"Score: {newScore}";
        StartCoroutine(PunchScale());
    }
    
    IEnumerator PunchScale()
    {
        // Scale up
        scoreText.transform.localScale = Vector3.one * punchScale;
        
        // Scale back down
        float elapsed = 0f;
        while (elapsed < punchDuration)
        {
            elapsed += Time.deltaTime;
            float t = elapsed / punchDuration;
            scoreText.transform.localScale = Vector3.Lerp(
                Vector3.one * punchScale, 
                Vector3.one, 
                t
            );
            yield return null;
        }
        
        scoreText.transform.localScale = Vector3.one;
    }
}
```

---

## Deel 3: Timer Display (15 min)

### Timer Script

```csharp
using UnityEngine;
using TMPro;

public class TimerDisplay : MonoBehaviour
{
    [SerializeField] private TMP_Text timerText;
    [SerializeField] private float startTime = 120f;  // 2 minutes
    
    private float remainingTime;
    private bool isRunning = false;
    
    public event System.Action OnTimerComplete;
    
    void Start()
    {
        remainingTime = startTime;
        UpdateDisplay();
    }
    
    void OnEnable()
    {
        GameManager.OnGameStateChanged += OnGameStateChanged;
    }
    
    void OnDisable()
    {
        GameManager.OnGameStateChanged -= OnGameStateChanged;
    }
    
    void OnGameStateChanged(GameState state)
    {
        isRunning = (state == GameState.Playing);
    }
    
    void Update()
    {
        if (!isRunning) return;
        
        remainingTime -= Time.deltaTime;
        
        if (remainingTime <= 0f)
        {
            remainingTime = 0f;
            isRunning = false;
            OnTimerComplete?.Invoke();
        }
        
        UpdateDisplay();
    }
    
    void UpdateDisplay()
    {
        int minutes = Mathf.FloorToInt(remainingTime / 60f);
        int seconds = Mathf.FloorToInt(remainingTime % 60f);
        
        timerText.text = $"{minutes:00}:{seconds:00}";
        
        // Kleur verandert als tijd bijna op is
        if (remainingTime < 30f)
        {
            timerText.color = Color.red;
        }
        else if (remainingTime < 60f)
        {
            timerText.color = Color.yellow;
        }
    }
    
    public void AddTime(float seconds)
    {
        remainingTime += seconds;
    }
    
    public void ResetTimer()
    {
        remainingTime = startTime;
        UpdateDisplay();
    }
}
```

### Count-Up Timer Variant

```csharp
public class StopwatchDisplay : MonoBehaviour
{
    [SerializeField] private TMP_Text timerText;
    
    private float elapsedTime = 0f;
    private bool isRunning = false;
    
    void Update()
    {
        if (!isRunning) return;
        
        elapsedTime += Time.deltaTime;
        
        int minutes = Mathf.FloorToInt(elapsedTime / 60f);
        int seconds = Mathf.FloorToInt(elapsedTime % 60f);
        int milliseconds = Mathf.FloorToInt((elapsedTime % 1f) * 100f);
        
        timerText.text = $"{minutes:00}:{seconds:00}.{milliseconds:00}";
    }
    
    public void StartTimer() => isRunning = true;
    public void StopTimer() => isRunning = false;
    public void ResetTimer() { elapsedTime = 0f; UpdateDisplay(); }
}
```

---

## Deel 4: Lives Display (15 min)

### Methode 1: Tekst

```csharp
public class LivesDisplayText : MonoBehaviour
{
    [SerializeField] private TMP_Text livesText;
    
    void OnEnable()
    {
        GameManager.OnLivesChanged += UpdateDisplay;
    }
    
    void OnDisable()
    {
        GameManager.OnLivesChanged -= UpdateDisplay;
    }
    
    void Start()
    {
        UpdateDisplay(GameManager.Instance.Lives);
    }
    
    void UpdateDisplay(int lives)
    {
        livesText.text = $"Lives: {lives}";
        
        // Of met emoji-style hearts
        livesText.text = new string('❤', lives);
    }
}
```

### Methode 2: Iconen (Images)

```csharp
using UnityEngine;
using UnityEngine.UI;

public class LivesDisplayIcons : MonoBehaviour
{
    [SerializeField] private Image[] lifeIcons;  // Array van heart images
    [SerializeField] private Sprite fullHeart;
    [SerializeField] private Sprite emptyHeart;
    
    void OnEnable()
    {
        GameManager.OnLivesChanged += UpdateDisplay;
    }
    
    void OnDisable()
    {
        GameManager.OnLivesChanged -= UpdateDisplay;
    }
    
    void Start()
    {
        UpdateDisplay(GameManager.Instance.Lives);
    }
    
    void UpdateDisplay(int lives)
    {
        for (int i = 0; i < lifeIcons.Length; i++)
        {
            if (i < lives)
            {
                lifeIcons[i].sprite = fullHeart;
                lifeIcons[i].color = Color.white;
            }
            else
            {
                lifeIcons[i].sprite = emptyHeart;
                lifeIcons[i].color = new Color(1, 1, 1, 0.3f);  // Semi-transparant
            }
        }
    }
}
```

### UI Hierarchy voor Lives Icons

```
Hierarchy:
├── Canvas
│   └── LivesPanel (Horizontal Layout Group)
│       ├── Life1 (Image)
│       ├── Life2 (Image)
│       └── Life3 (Image)

Horizontal Layout Group settings:
- Spacing: 10
- Child Alignment: Middle Left
- Control Child Size: Width ❌, Height ❌
```

### Animatie bij Leven Verliezen

```csharp
using UnityEngine;
using UnityEngine.UI;
using System.Collections;

public class LivesDisplayAnimated : MonoBehaviour
{
    [SerializeField] private Image[] lifeIcons;
    
    private int previousLives;
    
    void OnEnable()
    {
        GameManager.OnLivesChanged += OnLivesChanged;
    }
    
    void OnDisable()
    {
        GameManager.OnLivesChanged -= OnLivesChanged;
    }
    
    void OnLivesChanged(int newLives)
    {
        if (newLives < previousLives)
        {
            // Leven verloren - animeer het verloren hart
            int lostIndex = newLives;  // Index van hart dat weg moet
            StartCoroutine(AnimateLostLife(lifeIcons[lostIndex]));
        }
        else if (newLives > previousLives)
        {
            // Leven gewonnen
            int gainedIndex = newLives - 1;
            StartCoroutine(AnimateGainedLife(lifeIcons[gainedIndex]));
        }
        
        previousLives = newLives;
    }
    
    IEnumerator AnimateLostLife(Image heart)
    {
        // Shake
        Vector3 originalPos = heart.transform.localPosition;
        for (int i = 0; i < 5; i++)
        {
            heart.transform.localPosition = originalPos + (Vector3)Random.insideUnitCircle * 5f;
            yield return new WaitForSeconds(0.05f);
        }
        heart.transform.localPosition = originalPos;
        
        // Fade out
        float elapsed = 0f;
        Color startColor = heart.color;
        while (elapsed < 0.3f)
        {
            elapsed += Time.deltaTime;
            heart.color = Color.Lerp(startColor, new Color(1, 1, 1, 0.3f), elapsed / 0.3f);
            yield return null;
        }
    }
    
    IEnumerator AnimateGainedLife(Image heart)
    {
        heart.color = Color.white;
        heart.transform.localScale = Vector3.one * 1.5f;
        
        float elapsed = 0f;
        while (elapsed < 0.2f)
        {
            elapsed += Time.deltaTime;
            heart.transform.localScale = Vector3.Lerp(Vector3.one * 1.5f, Vector3.one, elapsed / 0.2f);
            yield return null;
        }
    }
}
```

---

## Oefeningen (60 min)

### Oefening 1: Complete HUD (25 min)

Maak een HUD met:
1. Score (top-left)
2. Timer (top-center)
3. Lives (top-right)

**Verwachte layout:**
```
┌────────────────────────────────────────────────────────────┐
│ Score: 12,450        02:34           ❤️ ❤️ ❤️              │
├────────────────────────────────────────────────────────────┤
│                                                            │
│                                                            │
│                      [GAME AREA]                           │
│                                                            │
│                                                            │
└────────────────────────────────────────────────────────────┘
```

**Checklist:**
- [ ] Canvas met correct scale mode
- [ ] Score text met anchor top-left
- [ ] Timer text met anchor top-center
- [ ] Lives panel met anchor top-right

### Oefening 2: Score met Animatie (15 min)

1. Implementeer het AnimatedScoreDisplay script
2. Score moet "punchen" bij update
3. Bonus: laat score omhoog tellen ipv direct springen

**Verwacht gedrag:**
```
Dot collected → Score: 100 → tekst wordt groter → tekst wordt normaal

Score counting animation:
Score: 100 → 102 → 105 → 110 → ... → 200
(telt snel op naar nieuwe waarde)
```

### Oefening 3: Lives met Icons (20 min)

1. Maak/vind 2 sprites: full heart, empty heart
2. Maak 3 Image objecten in een Horizontal Layout Group
3. Implementeer LivesDisplayIcons script
4. Test door lives te verliezen

**Verwacht resultaat:**
```
Start (3 lives):     ❤️ ❤️ ❤️
Na 1 hit (2 lives):  ❤️ ❤️ 🤍
Na 2 hits (1 life):  ❤️ 🤍 🤍
Game Over (0 lives): 🤍 🤍 🤍
```

**Bonus:** Voeg shake animatie toe bij leven verliezen

---

## Samenvatting

### UI Componenten

| Component | Gebruik |
|-----------|---------|
| **Canvas** | Container voor alle UI |
| **Text (TMP)** | Tekst weergeven |
| **Image** | Sprites/iconen weergeven |
| **Panel** | Groeperen van elementen |
| **Horizontal/Vertical Layout** | Automatische layout |

### Common Patterns

```csharp
// Score updaten
scoreText.text = $"Score: {score}";
scoreText.text = $"Score: {score:N0}";  // Met duizendtallen

// Timer formatteren
timerText.text = $"{minutes:00}:{seconds:00}";

// Lives als hearts
livesText.text = new string('❤', lives);

// Color veranderen
text.color = Color.red;
image.color = new Color(1, 1, 1, 0.5f);  // 50% transparant
```

### Event-Driven UI Pattern

```csharp
// In UI Script
void OnEnable() { GameManager.OnScoreChanged += UpdateDisplay; }
void OnDisable() { GameManager.OnScoreChanged -= UpdateDisplay; }
void UpdateDisplay(int value) { text.text = value.ToString(); }
```

### UI Animatie Tips

| Effect | Implementatie |
|--------|---------------|
| Punch/Pop | Scale up → scale down |
| Shake | Random offset → reset position |
| Fade | Color alpha 1 → 0 |
| Count Up | Lerp value over time |

---

## Eindopdracht Checklist

Na deze les heb je alle bouwstenen voor je Pac-Man game:

- [x] Grid generation (Les 2.1)
- [x] Player movement & collision (Les 3.1)
- [x] Ghost AI met waypoints (Les 4.1)
- [x] Animaties (Les 5.1, 5.2)
- [x] Game states & manager (Les 6.1)
- [x] UI: Score, Timer, Lives (Les 6.2)

**Veel succes met jullie eindopdracht! 🎮**
