# Les 7 : Early Return Patterns

## Wat is Return?

`return` is een keyword dat een functie **onmiddellijk stopt en een waarde kan teruggeven**.

**Basis voorbeelden:**

```csharp
// return in void functie - stopt de functie
public void PrintMessage()
{
    Debug.Log("Start");
    return;  // Functie stopt hier
    Debug.Log("Dit wordt nooit uitgevoerd");
}

// return met waarde - stopt en geeft waarde terug
public int GetNumber()
{
    return 42;  // Functie stopt, retourneert 42
}

// Early return - stop vroeg als iets fout is
public void Attack(Enemy target)
{
    if (target == null) return;  // Stop functie als target niet bestaat
    if (!target.IsAlive) return; // Stop functie als target dood is

    // Nu kunnen we veilig aanvallen
    target.TakeDamage(10);
}
```

**Kernidee**: `return` stopt direct - code NA de `return` wordt NIET uitgevoerd.

---

## Wat is Continue?

`continue` is een keyword dat **alleen in loops** werkt. Het slaat de rest van de huidige iteratie over en gaat direct naar de volgende iteratie.

**Basis voorbeelden:**

```csharp
// continue in foreach - skip huidige item
public void ProcessEnemies(List<Enemy> enemies)
{
    foreach (Enemy enemy in enemies)
    {
        if (enemy == null) continue;      // Skip als null
        if (!enemy.IsAlive) continue;     // Skip als dood

        // Nu verwerken we alleen levende enemies
        enemy.TakeDamage(10);
    }
}

// continue in for loop - skip huidige index
public void PrintNumbers()
{
    for (int i = 0; i < 10; i++)
    {
        if (i == 5) continue;  // Sla 5 over, ga naar 6
        Debug.Log(i);          // Print 0,1,2,3,4,6,7,8,9
    }
}

// continue vs break
public void FindEnemy(List<Enemy> enemies)
{
    foreach (Enemy enemy in enemies)
    {
        if (enemy == null) continue;    // continue = skip, ga volgende
        if (enemy.Name == "Boss") break; // break = stop hele loop

        Debug.Log(enemy.Name);
    }
}
```

**Kernidee**: `continue` slaat DEZE iteratie over, maar gaat verder met de VOLGENDE iteratie. `break` stopt de loop helemaal.

---

## Wat is Break?

`break` is een keyword dat **loops onmiddellijk beëindigt**. In tegenstelling tot `continue` (volgende iteratie) of `return` (hele functie), stopt `break` alleen de huidige loop.

**Basis voorbeelden:**

```csharp
// break in foreach - stop als we gevonden hebben wat we zoeken
public Enemy FindEnemyByName(List<Enemy> enemies, string name)
{
    foreach (Enemy enemy in enemies)
    {
        if (enemy == null) continue;      // Skip deze
        if (enemy.Name == name)
        {
            return enemy;                 // Gevonden! Functie stopt
        }
    }
    return null;                          // Niet gevonden
}

// break in for loop - stop vroeg
public void SearchNumbers()
{
    for (int i = 0; i < 100; i++)
    {
        if (i == 42)
        {
            Debug.Log("Gevonden!");
            break;                         // Stop loop, ga naar code NA loop
        }
        Debug.Log(i);
    }
    Debug.Log("Loop klaar");               // Dit WORDT nog uitgevoerd
}

// continue vs break vs return
public void ProcessEnemies(List<Enemy> enemies)
{
    foreach (Enemy enemy in enemies)
    {
        if (enemy == null) continue;       // Skip deze, volgende iteratie
        if (!enemy.IsAlive) break;         // Stop loop, ga naar code NA loop
        if (enemy.IsBoss) return;          // Stop hele functie

        enemy.TakeDamage(10);
    }

    Debug.Log("Take a break!");             //na een break wordt dit direct uitgevoerd
}
```

**Kernidee**:

- `continue` = skip deze iteratie, volgende iteratie
- `break` = stop de loop, ga naar code NA de loop
- `return` = stop de hele functie

---

## Het Probleem: Nested Conditions

Wanneer je veel if-statements hebt, ontstaan **"pyramids of doom"**:

![pyramid](https://media.giphy.com/media/v1.Y2lkPWVjZjA1ZTQ3NHloOGZxdXN2OWE4bmFrYWdpcXUycTA5aWIwMWphN2NraWl0N28yYyZlcD12MV9naWZzX3JlbGF0ZWQmY3Q9Zw/l3g00p6L9P1CEVX5C/giphy.gif)

```csharp

public void ProcessPlayer(Player player)
{
    if (player != null)
    {
        if (player.IsAlive)
        {
            if (player.Health > 0)
            {
                if (player.Inventory.HasWeapon())
                {
                    if (player.CanAttack())
                    {
                        // Eindelijk! We kunnen hier iets doen!
                        player.Attack();
                    }
                }
            }
        }
    }
}
```

**Problemen**:

- Moeilijk te lezen
- Lastig om logica te volgen
- Makkelijk bugs introduceren
- Code rekt zich uit over veel regels

---

## De Oplossing: Reversed If (Early Return)

**Idee**: Controleer eerst wat FOUT is, en return vroeg. Dan is de rest een "happy path" waarin je alles wat je wil doen mag doen.

```csharp
// GOED - Flat structure
public void ProcessPlayer(Player player)
{
    // Early returns: check alle foute condities eerst
    if (player == null) return;
    if (!player.IsAlive) return;
    if (player.Health <= 0) return;
    if (!player.Inventory.HasWeapon()) return;
    if (!player.CanAttack()) return;

    //Hier mag je nu doen wat je wil doen!
    player.Attack();
}
```

**Voordelen**:

- Vlak en leesbaar
- Logica is duidelijk
- Minder snel bugs
- Makkelijk uit te breiden

---

## "Early Return Patterns":

Bij programmen zijn er veel voorkomende patronen te herkennen. Bij het gebruiken van "Early returns" zijn er dus ook eenaantal herkenbare patronen te vinden.

### Patroon 1: Guard Clauses

**Idee**: Check foute condities aan het begin, return direct.

**Vergelijking:**

```csharp
// I.p.v een Pyraid of doom - "One big if"
public bool CanPlayerJump(Player player)
{
    if (player != null && !player.IsInAir && !player.IsStunned && player.Stamina >= 10)
    {
        return true;
    }
    return false;
}
```

vs

```csharp
// GOED - Guard clauses
public bool CanPlayerJump(Player player)
{
    if (player == null) return false;
    if (player.IsInAir) return false;
    if (player.IsStunned) return false;
    if (player.Stamina < 10) return false;

    return true;
}
```

**Voordeel**: Elk condition staat op zijn eigen regel = veel duidelijker!

---

### Patroon 2: Early Exit in Loops

**Vergelijking**

```csharp
// SLECHT - Nested loop
public Enemy FindNearestEnemy(List<Enemy> enemies)
{
    Enemy nearest = null;
    for (int i = 0; i < enemies.Count; i++)
    {
        if (enemies[i] != null)
        {
            if (enemies[i].IsAlive)
            {
                if (nearest == null || Vector3.Distance(transform.position, enemies[i].position) <
                    Vector3.Distance(transform.position, nearest.position))
                {
                    nearest = enemies[i];
                }
            }
        }
    }
    return nearest;
}
```

```csharp
// GOED - Early continue
public Enemy FindNearestEnemy(List<Enemy> enemies)
{
    Enemy nearest = null;

    foreach (Enemy enemy in enemies)
    {
        if (enemy == null) continue;           // Skip invalid
        if (!enemy.IsAlive) continue;          // Skip dead

        float distance = Vector3.Distance(transform.position, enemy.position);

        float nearestDistance;
        if (nearest == null)
        {
            nearestDistance = float.MaxValue;
        }
        else
        {
            nearestDistance = Vector3.Distance(transform.position, nearest.position);
        }

        if (distance < nearestDistance)
        {
            nearest = enemy;
        }
    }

    return nearest;
}
```

**Voordeel**: Geeft een oerzichtelijker beeld van wat er gebeurt en in welke volgorde

---

## Tips & Tricks

### Tip 1: Inverting Boolean Conditions

```csharp
// Wrong
if (!isInvincible) { /* take damage */ }

// Better - reverse it
if (isInvincible) return;
/* take damage */
```

### Tip 2: Use Continue in Loops

```csharp
// Nested
foreach (Enemy enemy in enemies)
{
    if (enemy.IsAlive)
    {
        // process
    }
}

// Early continue
foreach (Enemy enemy in enemies)
{
    if (!enemy.IsAlive) continue;
    // process
}
```

### Tip 3: Combine Simple Checks with && Only

```csharp
// Too complex
if (a > 0 && b < 100 && c == "valid" && d.IsReady() && !e.IsError())
{
    // Very hard to read
}

// Use early returns instead
if (a <= 0) return;
if (b >= 100) return;
if (c != "valid") return;
if (!d.IsReady()) return;
if (e.IsError()) return;

```

---

---

## Refactoring Challenge

### Opdracht 1: Simplify This

```csharp
public bool IsPlayerReadyToAttack(Player player)
{
    if (player != null)
    {
        if (player.IsAlive)
        {
            if (player.AttackCooldown <= 0)
            {
                if (player.Target != null)
                {
                    if (player.Target.IsAlive)
                    {
                        if (Vector3.Distance(player.transform.position, player.Target.transform.position) < 5f)
                        {
                            return true;
                        }
                    }
                }
            }
        }
    }
    return false;
}
```

---

## Checklist: Code Review

```
Early Return Checklist

[ ] Null checks zijn early returns
[ ] Guard clauses komen EERST
[ ] Geen "pyramid of doom"
[ ] Elke condition op eigen regel
[ ] Happy path is leesbaar
[ ] Boolean conditions niet dubbel negatief
[ ] Loops gebruiken continue voor invalid items
[ ] Max nesting level = 2
[ ] Makkelijk te testen (flat structure)
```

---

## Belangrijkste punten

**Reversed If Statements** = Check wat FOUT is eerst, dan return.
Dit maakt je code plat, leesbaar en maintainable.

**Gouden Regel**: Hoe minder nesting, hoe beter je code!

---
