# Les 1.1 - Herhaling C# Basics & Project Setup

## Leerdoelen

Na deze les kun je:

- C# basics toepassen (arrays, lists, variables, functions, if-statements)
- Een Unity project opzetten met correcte mappenstructuur
- Een Git repository aanmaken en koppelen
- Scenes laden en herladen via code

---

## Deel 1: Herhaling C# Basics (20 min)

### Variables

```csharp
// Basis datatypes
int score = 0;
float speed = 5.5f;
string playerName = "Pac-Man";
bool isAlive = true;
```

### Arrays

Een array heeft een **vaste grootte** die je bij aanmaak bepaalt.

```csharp
// Array aanmaken
int[] scores = new int[5];           // 5 lege plekken
string[] names = { "Jan", "Piet" };  // Direct vullen

// Toegang tot elementen (index begint bij 0)
scores[0] = 100;
Debug.Log(names[1]);  // Output: "Piet"

// Door array loopen
for (int i = 0; i < scores.Length; i++)
{
    Debug.Log(scores[i]);
}
```

### Lists

Een List kan **groeien en krimpen** tijdens runtime.

```csharp
using System.Collections.Generic;

// List aanmaken
List<int> highScores = new List<int>();

// Elementen toevoegen
highScores.Add(500);
highScores.Add(300);

// Element verwijderen
highScores.Remove(300);
highScores.RemoveAt(0);  // Verwijder op index

// Door list loopen
foreach (int score in highScores)
{
    Debug.Log(score);
}
```

### Functions (Methods)

```csharp
// Functie zonder return waarde
void SayHello()
{
    Debug.Log("Hello!");
}

// Functie met parameters
void AddScore(int points)
{
    score += points;
}

// Functie met return waarde
int GetDoubleScore(int input)
{
    return input * 2;
}
```

### If Statements

```csharp
if (score >= 100)
{
    Debug.Log("Gewonnen!");
}
else if (score >= 50)
{
    Debug.Log("Bijna...");
}
else
{
    Debug.Log("Blijf proberen!");
}
```

---

## Deel 2: Project Setup (20 min)

### Unity Project Aanmaken

1. Open Unity Hub
2. Klik **New Project**
3. Kies **2D Core** template
4. Geef een duidelijke naam: `PacMan_[Naam1]_[Naam2]`
5. Kies een locatie (niet in OneDrive!)

### Mappenstructuur

Maak de volgende mappen aan in je Project window:

```
Assets/
├── Animations/
├── Audio/
├── Materials/
├── Prefabs/
├── Scenes/
├── Scripts/
├── Sprites/
└── UI/
```

### Git Repository

1. Maak een **nieuwe repository** aan op GitHub
2. Voeg een **Unity .gitignore** toe
3. Clone naar je computer
4. Kopieer je Unity project naar de repo folder
5. Commit en push

**Tip:** Zorg dat beide teamleden als collaborator zijn toegevoegd!

---

## Deel 3: Scene Management (20 min)

### Scenes Toevoegen aan Build Settings

1. Ga naar **File > Build Settings**
2. Sleep je scenes naar de lijst
3. Elke scene krijgt een **index nummer** (0, 1, 2, ...)

### Scene Laden via Code

```csharp
using UnityEngine.SceneManagement;

public class SceneLoader : MonoBehaviour
{
    // Scene laden op naam
    public void LoadGame()
    {
        SceneManager.LoadScene("GameScene");
    }

    // Scene laden op index
    public void LoadMainMenu()
    {
        SceneManager.LoadScene(0);
    }

    // Huidige scene herladen (restart)
    public void RestartLevel()
    {
        Scene currentScene = SceneManager.GetActiveScene();
        SceneManager.LoadScene(currentScene.name);
    }

    // Alternatief: restart via index
    public void RestartLevelAlt()
    {
        SceneManager.LoadScene(SceneManager.GetActiveScene().buildIndex);
    }
}
```

### Scene Laden met Button

1. Maak een **UI Button** aan
2. Voeg het `SceneLoader` script toe aan een GameObject
3. Koppel de button aan de gewenste functie via de **OnClick()** event

---

## Oefeningen (60 min)

### Oefening 1: Project Setup (15 min)

- Maak duo's
- Maak een nieuw Unity 2D project aan
- Creëer de mappenstructuur
- Maak een Git repo en push het project
- Zorg dat beide teamleden kunnen pullen en pushen

### Oefening 2: Herhaling Script (20 min)

Maak een script `BasicsPractice.cs` met:

1. Een `int` array met 5 getallen
2. Een `List<string>` met namen van je teamleden
3. Een functie `PrintAllNumbers()` die alle getallen uit de array print
4. Een functie `int Sum()` die de som van alle getallen teruggeeft
5. Een `if-statement` in Start() dat checkt of de som groter is dan 20

**Voorbeeld output in Console:**

```
Getal: 5
Getal: 10
Getal: 3
Getal: 8
Getal: 12
Teamleden: Jan, Piet
De som is: 38
De som is groter dan 20!
```

### Oefening 3: Scene Management (25 min)

1. Maak 3 scenes: `MainMenu`, `Game`, `GameOver`
2. Voeg ze toe aan Build Settings
3. Maak een `SceneLoader` script
4. In MainMenu: een button "Start Game" → laadt Game scene
5. In Game: een button "Restart" → herlaadt Game scene
6. In Game: een button "Quit" → laadt MainMenu scene
7. In GameOver: een button "Try Again" → laadt Game scene
8. In GameOver: een button "Main Menu" → laadt MainMenu scene

**Verwacht resultaat:**

```
┌─────────────────────┐     ┌─────────────────────┐     ┌─────────────────────┐
│     MAIN MENU       │     │        GAME         │     │     GAME OVER       │
│                     │     │                     │     │                     │
│   [Start Game] ─────┼────►│   [Restart] ────────┼──┐  │   [Try Again] ──────┼──┐
│                     │     │                     │  │  │                     │  │
│   [Exit Game]       │◄────┼── [Quit]            │  │  │   [Main Menu] ──────┼──┼─┐
│                     │     │                     │  │  │                     │  │ │
└─────────────────────┘     └─────────────────────┘  │  └─────────────────────┘  │ │
        ▲                            ▲               │           ▲               │ │
        │                            └───────────────┴───────────┼───────────────┘ │
        └────────────────────────────────────────────────────────┘                 │
        └──────────────────────────────────────────────────────────────────────────┘
```

**Bonus:** Voeg `Application.Quit()` toe aan een "Exit Game" button in MainMenu.

---

## Samenvatting

| Concept          | Beschrijving                                            |
| ---------------- | ------------------------------------------------------- |
| Array            | Vaste grootte, snelle toegang via index                 |
| List             | Dynamische grootte, Add/Remove methodes                 |
| Function         | Herbruikbaar blok code, kan parameters en return hebben |
| SceneManager     | Laad scenes via naam of index                           |
| GetActiveScene() | Geeft info over huidige scene                           |

---

## Volgende Les

In **Les 1.2** gaan we de originele Pac-Man analyseren en bedenken jullie een eigen twist voor je game!
