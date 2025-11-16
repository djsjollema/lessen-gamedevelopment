# M2 GDV les 1 (CODE) Herhaling Basis C#

Doel: korte en duidelijke herhaling van belangrijke programmeerconcepten in de context van Unity en C#.

Onderwerpen:

1. Variabelen en datatypes
2. Functies, argumenten en return values
3. If en switch statements
   Nieuw onderwerp:
4. Lists en Arrays

---

## 1) Variabelen en datatypes

- Variabelen zijn namen voor opslag van waarden.
- Veelgebruikte datatypes in Unity/C#:
  - `int` (gehele getallen), `float` (kommagetallen, e.g. 3.14f), `bool` (true/false), `string` (tekst)
  - `Vector2`, `Vector3`, `Quaternion` (Unity structs voor positie/rotatie)
- Declaratievoorbeeld:

```csharp
int score = 0;
float speed = 5.5f;
string playerName = "Hero";
bool isAlive = true;
```

Korte uitleg:

- `int` en `float` verschillen in precisie en gebruik; floats veel in games voor beweging.
- `string` is een reference type; primitives (int/float/bool) zijn value types.

Meerkeuzevragen (2x):

1. Welke datatype gebruik je voor een teller van behaalde punten?
   A) `float`
   B) `string`
   C) `int`
   D) `bool`

2. Welk datatype is geschikt voor de tekstnaam van een speler?
   A) `int`
   B) `string`
   C) `bool`
   D) `float`

---

## 2) Functies, argumenten en return values

- Functie (methode) is een blok code dat een taak uitvoert.
- Argumenten (parameters) zijn de inputs; return value is wat de functie teruggeeft.
- Voorbeeld:

```csharp
public int Add(int a, int b)
{
    return a + b;
}

void PrintName(string name)
{
    Debug.Log(name);
}
```

- `void` betekent: geen return value.

Korte uitleg:

- Gebruik functies om code te organiseren en herhaling te vermijden.
- Kies duidelijke parameter- en functienamen.

Meerkeuzevragen (2x): 3. Welke return-type gebruik je als een functie niets hoeft terug te geven?
A) `int`
B) `string`
C) `void`
D) `bool`

4. Wat doet deze functie?

```csharp
public float Multiply(float x, float y)
{
    return x * y;
}
```

A) Print twee getallen
B) Maakt een vector
C) Geeft de uitkomst van x maal y terug
D) Zet x en y naar 0

---

## 3) If en switch statements

- `if` gebruik je voor conditionele logica:

```csharp
if (health <= 0)
{
    Die();
}
else if (health < 20)
{
    PlayLowHealthWarning();
}
else
{
    // normaal gedrag
}
```

- `switch` is handig bij meerdere vergelijkbare cases:

```csharp
switch (weaponType)
{
    case "Melee":
        // melee logic
        break;
    case "Ranged":
        // ranged logic
        break;
    default:
        // fallback
        break;
}
```

Korte uitleg:

- `if` is meer algemeen en geschikt voor ranges en complexe voorwaarden.
- `switch` is overzichtelijker bij veel vaste opties.

Meerkeuzevragen (2x): 5. Wanneer gebruik je `switch` in plaats van meerdere `if/else`?
A) Voor continue reeksen met floats
B) Als je veel, vooraf bekende cases hebt
C) Voor random getallen
D) Als je altijd `else` wilt vermijden

6. Welke statement voert 1x code uit als de condition true is?
   A) `for`
   B) `while`
   C) `if`
   D) `switch`

---

## 4) Lists en Arrays (duidelijke uitleg met voorbeelden)

Arrays:

- Arrays zijn vaste-lengte collecties met elementen van hetzelfde type.
- Netjes en snel; handig als de grootte bekend en onveranderd is.
- C# voorbeeld:

```csharp
int[] scores = new int[5];
scores[0] = 10;
// of direct
int[] enemies = new int[] { 1, 2, 3 };

// Itereren
for (int i = 0; i < enemies.Length; i++)
{
    Debug.Log(enemies[i]);
}
```

Lists (`System.Collections.Generic.List<T>`):

- Dynamische grootte: je kunt items toevoegen/verwijderen tijdens runtime.
- Handiger voor variabele collecties.
- C# voorbeeld (Unity):

```csharp
using System.Collections.Generic;

public class Inventory : MonoBehaviour
{
    [SerializeField] private List<string> items = new List<string>();

    void Start()
    {
        items.Add("Sword");
        items.Add("Potion");
    }

    void PrintItems()
    {
        foreach (var it in items)
            Debug.Log(it);
    }
}
```

Belangrijkste verschillen en tips:

- Gebruik `array` als:
  - Je exacte lengte kent en die niet verandert.
  - Je maximale performance wilt (marginaal sneller voor vaste grootte).
- Gebruik `List<T>` als:
  - Je items wilt toevoegen, verwijderen of de lengte variabel is.
  - Je gemak wilt (methodes als `Add`, `Remove`, `Insert`).
- Unity Inspector: `List<T>` en arrays zijn beide serialiseerbaar en zichtbaar in Inspector als ze `public` of `[SerializeField] private` zijn (let op: sommige oude Unity-versies verschilden).

Voorbeeld: array vs list

```csharp
// Array
[SerializeField] private GameObject[] spawnPoints;

// List
[SerializeField] private List<GameObject> enemies = new List<GameObject>();

void SpawnAll()
{
    // array
    for (int i = 0; i < spawnPoints.Length; i++)
        Instantiate(prefab, spawnPoints[i].transform.position, Quaternion.identity);

    // list
    foreach (var e in enemies)
        e.SetActive(true);
}
```

---

## Praktische Oefening — Combineer variabelen, functie, if-statements en een List

Opdracht: maak een nieuw C# script `PlayerExample.cs` (attach aan een GameObject) dat de volgende functionaliteit heeft:

- Declaraties:

  - Een `int health` (startwaarde 100)
  - Een `float speed` (bijv. 5f)
  - Een `string playerName`
  - Een `List<string> inventory` om opgepakte items in op te slaan

- Functie:

  - Implementeer een publieke methode `bool ApplyDamage(int damage)` die de `health` vermindert en `true` teruggeeft als de speler nog leeft, `false` als `health <= 0`.

- If-statements:

  - Gebruik een `if` om te controleren of `health` onder bepaalde drempels valt (bijv. <50 en <=0) en log een passende boodschap met `Debug.Log()`.

- List gebruik:
  - Voeg een methode `void PickUpItem(string item)` die het item toevoegt aan `inventory`.
  - Voeg een methode `void PrintInventory()` die alle items uit de `inventory` via `Debug.Log` print.

Code-skeleton:

```csharp
using System.Collections.Generic;
using UnityEngine;

public class PlayerExample : MonoBehaviour
{
        // variabelen
        public int health = 100;
        public float speed = 5f;
        public string playerName = "Player";
        private List<string> inventory = new List<string>();

        // functie: past damage toe en retourneert of speler leeft
        public bool ApplyDamage(int damage)
        {
                health -= damage;
                if (health <= 0)
                {
                        Debug.Log(playerName + " is dead.");
                        return false;
                }

                if (health < 50)
                        Debug.Log(playerName + " is wounded (" + health + ").");

                return true;
        }

        // list: items oppakken en tonen
        public void PickUpItem(string item)
        {
                inventory.Add(item);
                Debug.Log(item + " picked up.");
        }

        public void PrintInventory()
        {
                Debug.Log("Inventory for " + playerName + ":");
                foreach (var it in inventory)
                        Debug.Log("- " + it);
        }
}
```

Acceptatiecriteria / wat aflevering moet tonen:

- Het script compileert zonder fouten in Unity.
- `ApplyDamage` vermindert `health`, logt juiste berichten en returned correcte boolean.
- `PickUpItem` voegt items toe aan de `List` en `PrintInventory` toont ze.
- Voeg in een korte README of screenshot toe waarin je laat zien dat je script werkt (bijv. Console output na ApplyDamage en PrintInventory).

Hints:

- Zet `playerName` en `health` als public of `[SerializeField] private` zodat je ze in de Inspector kunt aanpassen.
- Test via `Start()` of door een tijdelijk debug-script dat `ApplyDamage` en `PickUpItem` aanroept.

---

## Oplevering / huiswerk

- Optioneel: maak een korte Unity-scene die één array en één list toont in de Inspector en laat zien dat je items kunt toevoegen aan de list via code (of via Inspector) en dat de array vaste lengte heeft.
- Lever eventueel een screenshot of korte notitie in tijdens de volgende les.

---

Als je wilt, voeg ik nu:

- Een korte quiz-oplossing met uitleg per vraag (in comments), of
- Een voorbeeld Unity-scene en scripts als startpunt (maak ik bestanden aan in de repo).

Welke van de twee heeft je voorkeur?
