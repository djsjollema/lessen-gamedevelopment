# Les 2.1 - Grid Generatie met Arrays & Modulo

## Leerdoelen

Na deze les kun je:

- Een 1D array gebruiken om een 2D grid voor te stellen
- De modulo operator (%) gebruiken voor grid berekeningen
- Procedureel een level genereren met code
- Verschillende tile types spawnen op basis van data

---

## Deel 1: 1D Array als 2D Grid (20 min)

### Waarom 1D in plaats van 2D?

Een 2D array (`int[,]`) werkt, maar een 1D array is:

- Makkelijker te serialiseren (opslaan/laden)
- Efficiënter in geheugen
- Simpeler te loopen

### Grid Concept

Een 5x3 grid (5 breed, 3 hoog):

```
Visueel:              Als 1D array:
[0] [1] [2] [3] [4]   [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14]
[5] [6] [7] [8] [9]
[10][11][12][13][14]
```

### Index Berekenen met Modulo

```csharp
int width = 5;
int height = 3;
int[] grid = new int[width * height]; // 15 elementen

// Van index naar x,y positie
int index = 7;
int x = index % width;    // 7 % 5 = 2
int y = index / width;    // 7 / 5 = 1 (integer deling)

// Van x,y positie naar index
int x = 2;
int y = 1;
int index = y * width + x;  // 1 * 5 + 2 = 7
```

### Modulo Uitleg

De modulo operator `%` geeft de **rest** van een deling:

```csharp
0 % 5 = 0   // 0 / 5 = 0 rest 0
1 % 5 = 1   // 1 / 5 = 0 rest 1
2 % 5 = 2   // 2 / 5 = 0 rest 2
5 % 5 = 0   // 5 / 5 = 1 rest 0  ← wrapt terug naar 0!
7 % 5 = 2   // 7 / 5 = 1 rest 2
```

---

## Deel 2: Level Data Structuur (15 min)

### Tile Types

Definieer je tile types als getallen:

```csharp
public class TileTypes
{
    public const int EMPTY = 0;
    public const int WALL = 1;
    public const int DOT = 2;
    public const int POWER_PELLET = 3;
    public const int PLAYER_SPAWN = 4;
    public const int GHOST_SPAWN = 5;
}
```

Of gebruik een enum:

```csharp
public enum TileType
{
    Empty = 0,
    Wall = 1,
    Dot = 2,
    PowerPellet = 3,
    PlayerSpawn = 4,
    GhostSpawn = 5
}
```

### Level Data

```csharp
public class LevelData : MonoBehaviour
{
    public int width = 7;
    public int height = 5;

    // Level als 1D array (0=empty, 1=wall, 2=dot, etc.)
    public int[] tiles = new int[]
    {
        1, 1, 1, 1, 1, 1, 1,  // Rij 0 (boven)
        1, 2, 2, 2, 2, 2, 1,  // Rij 1
        1, 2, 1, 3, 1, 2, 1,  // Rij 2 (midden)
        1, 2, 2, 4, 2, 2, 1,  // Rij 3
        1, 1, 1, 1, 1, 1, 1   // Rij 4 (onder)
    };
}
```

---

## Deel 3: Grid Generator (25 min)

### Basis Grid Generator Script

```csharp
using UnityEngine;

public class GridGenerator : MonoBehaviour
{
    [Header("Grid Settings")]
    public int width = 7;
    public int height = 5;
    public float tileSize = 1f;

    [Header("Prefabs")]
    public GameObject wallPrefab;
    public GameObject dotPrefab;
    public GameObject powerPelletPrefab;
    public GameObject playerPrefab;

    [Header("Level Data")]
    public int[] levelData;

    void Start()
    {
        GenerateLevel();
    }

    void GenerateLevel()
    {
        for (int i = 0; i < levelData.Length; i++)
        {
            // Bereken x en y positie
            int x = i % width;
            int y = i / width;

            // Bereken world positie
            Vector3 position = new Vector3(x * tileSize, -y * tileSize, 0);

            // Spawn juiste prefab op basis van tile type
            SpawnTile(levelData[i], position);
        }
    }

    void SpawnTile(int tileType, Vector3 position)
    {
        GameObject prefab = null;

        switch (tileType)
        {
            case 0: // Empty
                // Niets spawnen
                break;
            case 1: // Wall
                prefab = wallPrefab;
                break;
            case 2: // Dot
                prefab = dotPrefab;
                break;
            case 3: // Power Pellet
                prefab = powerPelletPrefab;
                break;
            case 4: // Player Spawn
                prefab = playerPrefab;
                break;
        }

        if (prefab != null)
        {
            Instantiate(prefab, position, Quaternion.identity, transform);
        }
    }
}
```

### Grid Centreren

Om het grid te centreren rond de origin:

```csharp
void GenerateLevel()
{
    // Offset om grid te centreren
    float offsetX = (width - 1) * tileSize / 2f;
    float offsetY = (height - 1) * tileSize / 2f;

    for (int i = 0; i < levelData.Length; i++)
    {
        int x = i % width;
        int y = i / width;

        Vector3 position = new Vector3(
            x * tileSize - offsetX,
            -y * tileSize + offsetY,
            0
        );

        SpawnTile(levelData[i], position);
    }
}
```

### Level Data in Inspector

Tip: Maak level data makkelijk aan te passen in de Inspector:

```csharp
[System.Serializable]
public class LevelRow
{
    public int[] columns;
}

public class GridGenerator : MonoBehaviour
{
    public LevelRow[] rows;

    int[] FlattenLevel()
    {
        // Converteer 2D rows naar 1D array
        int[] flat = new int[width * height];
        for (int y = 0; y < rows.Length; y++)
        {
            for (int x = 0; x < rows[y].columns.Length; x++)
            {
                flat[y * width + x] = rows[y].columns[x];
            }
        }
        return flat;
    }
}
```

---

## Oefeningen (60 min)

### Oefening 1: Modulo Oefenen (10 min)

Bereken zonder code (pen en papier):

1. Een grid is 8 breed. Index 15 zit op welke x,y?
2. Een grid is 6 breed. Positie (3, 2) heeft welke index?
3. Een grid is 10 breed en 5 hoog. Hoeveel elementen heeft de array?
4. Index 0, 10, 20, 30 zitten allemaal op welke x-positie?

**Antwoorden:**

1. x = 15 % 8 = 7, y = 15 / 8 = 1 → (7, 1)
2. index = 2 \* 6 + 3 = 15
3. 10 \* 5 = 50 elementen
4. Allemaal x = 0 (eerste kolom)

### Oefening 2: Simpel Grid (20 min)

1. Maak een nieuwe scene `GridTest`
2. Maak 2 prefabs: `Wall` (vierkant sprite, gekleurd) en `Dot` (klein cirkel sprite)
3. Maak het `GridGenerator` script
4. Maak een 5x5 level met muren rondom en dots binnenin:
   ```
   1, 1, 1, 1, 1,
   1, 2, 2, 2, 1,
   1, 2, 2, 2, 1,
   1, 2, 2, 2, 1,
   1, 1, 1, 1, 1
   ```
5. Test of het grid correct genereert

### Oefening 3: Uitgebreid Grid (30 min)

Breid je grid uit:

1. Voeg een `PowerPellet` prefab toe (groter dan dot, andere kleur)
2. Voeg een `PlayerSpawn` prefab toe
3. Maak een groter level (minimaal 9x9)
4. Ontwerp een simpel doolhof met:
   - Muren aan de buitenkant
   - Minstens 2 power pellets
   - Een player spawn punt
   - Paden met dots

**Bonus Challenges:**

- Voeg een `GhostSpawn` tile type toe
- Maak een functie `ClearLevel()` die alle gespawnde tiles verwijdert
- Maak een button die het level regenereert

---

## Samenvatting

| Concept        | Formule/Code                         |
| -------------- | ------------------------------------ |
| Index → X      | `x = index % width`                  |
| Index → Y      | `y = index / width`                  |
| X,Y → Index    | `index = y * width + x`              |
| Array grootte  | `width * height`                     |
| Grid centreren | Offset = `(size - 1) * tileSize / 2` |

### Quick Reference

```csharp
// Loop door heel grid
for (int i = 0; i < grid.Length; i++)
{
    int x = i % width;
    int y = i / width;
    Vector3 pos = new Vector3(x, -y, 0);
}

// Loop met x en y
for (int y = 0; y < height; y++)
{
    for (int x = 0; x < width; x++)
    {
        int index = y * width + x;
        int tileType = grid[index];
    }
}
```

---

## Volgende Les

In **Les 2.2** gaan we jullie concept verder uitwerken in een Game Design Document!
