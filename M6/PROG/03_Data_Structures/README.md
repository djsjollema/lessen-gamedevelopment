# Les 3 - Data Structures in Unity

## Doel

Kort overzicht voor beginnende game developers: wanneer gebruik je Class, Struct, Enum of ScriptableObject? Praktische voorbeelden en 2 korte oefeningen.

## Tijd (45 min)

- Korte intro Stack vs Heap (7 min)
- Classes vs Structs (10 min)
- Oefening 1 (5 min)
- Enums & ScriptableObjects (10 min)
- Oefening 2 (5 min)
- Huiswerk uitleg (8 min)

![stack vs heap](../src/03_stack_heap.png)

## Stack vs Heap (kort)

- **Stack:** snelle, tijdelijke opslag voor value types (lokale variabelen, structs). Wordt automatisch opgeruimd.
- **Heap:** opslag voor reference types (classes, ScriptableObjects). Langere levensduur, beheerd door Garbage Collector.

Kort voorbeeld:

```csharp
int a = 5;                 // value - stack
Vector3 v = new Vector3(); // struct - vaak op stack
Player p = new Player();   // class - heap
```

Belangrijk: structs zijn snel en licht, maar worden steeds gekopieerd. Classes zijn flexibeler (null, inheritance) maar kosten heap-overhead. (garbage collection)

![garbage](https://media3.giphy.com/media/v1.Y2lkPTc5MGI3NjExcmlmZTk3YWd3MjFiYzFjbGVpbGxnY2U4b3J3OGszMDdmaXRqZTlnYiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/19D9Pj5eoKUPtEsLGf/giphy.gif)

## Classes

- Reference type, gebruik bij: complexe objecten, inheritance, MonoBehaviours, wanneer je mutable gedeelde state wilt. Gebruik van functies in de class.

```csharp
public class Player {
    public string name;
    public int health;
    void Attack(){
        //code
    }
}
```

## Structs

- Value type, gebruik bij: kleine data (posities, stats), performance-kritische, immutable waar mogelijk. Passieve data.

```csharp
public struct PlayerStats {
    public int health;
    public float speed;
}
```

Oefening 1 (5 min):
Welk type kies je?

1. Powerup state van een tower in een towerdefense game.
2. Enemy AI component voor het bepalen en uitvoeren van het gedrag.
3. XYZ-coördinaten in een 3d omgeving.
4. Management van actieve powerups

## Enums

- Gebruik voor vaste opties (weapon types, game states). Maakt code leesbaarder. Voorkomen van magic numbers. Enums zijn voor de code gewoon integers. De waardes veranderen nooit.

```csharp
public class GameSettings : MonoBehaviour
{
    public int currentDifficulty;
    public enum Difficulty { Easy, Medium, Hard };
    void Start()
    {
        SetDifficulty(1);  // Zet de moeilijkheidsgraad op 1? magic number, wat betekent 1?
        SetDifficulty((int)Difficulty.Easy); //gebruiken van een enum
    }
    void SetDifficulty(int difficulty)
    {
        currentDifficulty = difficulty;
        Debug.Log("difficulty is set to : " + currentDifficulty);
    }
}
```

## ScriptableObjects (kort)

- Asset-based reference type, ideaal voor gedeelde configuratie/gegevens (items, level data, tuning)
- Voordelen: deelbaar tussen prefabs, zichtbaar in Inspector, persistente asset (ook als de game niet speelt)
- Niet bedoeld als per-instance runtime-state container (dat leidt tot onverwachte gedeelde wijzigingen) Dus niet geschikt om veranderende data bij te houden.

Kort voorbeeld:

```csharp
[CreateAssetMenu(menuName = "Game/Weapon")]
public class WeaponData : ScriptableObject { public string name; public int damage; }
```

### ScriptableObjects vs Structs (kort)

- ScriptableObject: één gedeelde asset, reference type op heap, goed voor templates/configs.
- Struct: kleine value container, wordt gekopieerd, snel voor veel kleine instances.

Gebruik ScriptableObject als je één bron van waarheid wil (bijv. wapen-template). Gebruik struct voor per-entity kleine data (bijv. positie, simpele stats).

Oefening 2 (5 min):
Refactor de volgende (kort):

```csharp
public class Enemy : MonoBehaviour {
  public int enemyType; // 0=melee,1=ranged
  public float[] stats; // health,damage,speed
}
```

## Huiswerk (kort)

- Maak 4 Weapon ScriptableObjects (verschillende damage, speed, durability).
- Maak een `WeaponStats` struct die je gebruikt om de ????.
- Toon in een kleine scene: 1 prefab die een ScriptableObject gebruikt en zijn struct-gegevens toont in de Inspector/console.

Lever in: korte GitHub PR met code + 1 screenshot.

## Tips (1 regel)

- Structs = snel & klein; Classes/ScriptableObjects = deelbaar & flexibel. Kies bewust of je wilt delen of kopiëren.

## Links

- Unity scripting docs: https://docs.unity3d.com/ScriptReference/
- ScriptableObject guide: https://unity.com/how-to/architect-game-code-scriptable-objects
  - Je inheritance nodig hebt
