# Les 3 - Data Structures in Unity

## Doel

Jullie leren wat "data structuren" zijn en maken kennis met een specifieke structuren. Je leert wanneer je welke het beste kunt gebruiken: wanneer gebruik je Class, Struct, Enum of ScriptableObject?

## Inhoud van de les

- Korte intro Stack vs Heap
- Classes vs Structs
- Oefening 1
- Enums & ScriptableObjects
- Oefening 2
- Huiswerk uitleg

## Stack vs Heap

Het RAM geheugen van je computer heb je nodig om je computer instructies te laten onthouden zodat deze ook goed uitgevoerd kunnen worden. Het geheugen kent 2 verschillende manieren van hoe deze omgaan met data.

![stack vs heap](../src/03_stack_heap.png)

- **Stack:** snelle, tijdelijke opslag voor **"value types"** (lokale variabelen, structs). Wordt automatisch opgeruimd volgens het first in last out (FILO) principe.
- **Heap:** opslag voor **"reference types"** (classes, ScriptableObjects). Langere levensduur, beheerd door Garbage Collector. Slim systeem dat zorgt dat gegevens automatisch worden verwijderd bijvoorbeeld als er weinig geheugen over is.

Kort voorbeeld:

```csharp
int a = 5;                 // value - stack
Vector3 v = new Vector3(); // struct - vaak op stack
Player p = new Player();   // class - heap
```

Belangrijk: structs zijn snel en licht, maar worden steeds gekopieerd. Classes zijn flexibeler (null, inheritance) maar kosten heap-overhead. (garbage collection)

![garbage](https://media3.giphy.com/media/v1.Y2lkPTc5MGI3NjExcmlmZTk3YWd3MjFiYzFjbGVpbGxnY2U4b3J3OGszMDdmaXRqZTlnYiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/19D9Pj5eoKUPtEsLGf/giphy.gif)

---

## 10 veel voorkomende Value Types in Unity

1. **int** — gehele getallen (-2147483648 tot 2147483647)
2. **float** — kommagetallen met enkele precisie (3.14f)
3. **bool** — true/false waarden
4. **double** — kommagetallen met dubbele precisie (7.5d)
5. **byte** — kleine gehele getallen (0 tot 255)
6. **short** — gehele getallen (-32768 tot 32767)
7. **long** — grote gehele getallen (-9223372036854775808 tot 9223372036854775807)
8. **char** — één karakter ('a', 'Z', '5')
9. **decimal** — zeer nauwkeurige kommagetallen (voor financiële berekeningen)
10. **uint** — positieve gehele getallen (0 tot 4294967295)

---

## 10 veel voorkomende structs in Unity

1. **Vector2** — 2D vector met x en y coördinaten (bijv. voor 2D-spellen)
2. **Vector3** — 3D vector met x, y en z coördinaten (bijv. voor posities en rotaties)
3. **Quaternion** — rotatiedata in 3D ruimte (efficiënter dan Euler-hoeken)
4. **Color** — RGBA kleuren (rood, groen, blauw, alpha/doorzichtigheid)
5. **Bounds** — rechthoekig volume gedefinieerd door center en extents
6. **Rect** — rechthoek gedefinieerd door positie en grootte
7. **Matrix4x4** — 4x4 matrix voor transformaties
8. **RaycastHit** — informatie uit een raycast (wat geraakt werd)
9. **ContactPoint** — contactpunt tussen twee colliders (gebruikt bij Physics callbacks)
10. **Plane** — oneindig vlak in 3D ruimte gedefinieerd door normal en afstand

---

## De 10 Meest Gebruikte Classes in Unity

1. **GameObject** — basis object in Unity (alles wat in een scene staat)
2. **Transform** — positie, rotatie en schaal van een GameObject
3. **MonoBehaviour** — basis class voor alle scripts die je schrijft
4. **Rigidbody** — physics component voor realistische beweging
5. **Collider** — geometry voor collision detection (BoxCollider, SphereCollider, etc.)
6. **Camera** — kijkpunt van de speler in de wereld
7. **Light** — lichtbron in de scene
8. **Canvas** — container voor UI-elementen
9. **Image** — 2D plaatje weergeven in UI
10. **AudioSource** — geluid afspelen in de wereld of voor UI

---

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
